SHELL := /bin/bash

PWD 									?= pwd_unknown

THIS_FILE								:= $(lastword $(MAKEFILE_LIST))
export THIS_FILE
TIME									:= $(shell date +%s)
export TIME

ifeq ($(alpine),)
ALPINE_VERSION							:= 3.11.6
else
ALPINE_VERSION							:= $(alpine)
endif
export ALPINE_VERSION

#GIT CONFIG
GIT_USER_NAME							:= $(shell git config user.name)
export GIT_USER_NAME
GIT_USER_EMAIL							:= $(shell git config user.email)
export GIT_USER_EMAIL
GIT_SERVER								:= https://github.com
export GIT_SERVER
GIT_PROFILE								:= bitcoincore-dev
export GIT_PROFILE
GIT_BRANCH								:= $(shell git rev-parse --abbrev-ref HEAD)
export GIT_BRANCH
GIT_HASH								:= $(shell git rev-parse HEAD)
export GIT_HASH
GIT_REPO_ORIGIN							:= $(shell git remote get-url origin)
export GIT_REPO_ORIGIN
GIT_REPO_NAME							:= $(PROJECT_NAME)
export GIT_REPO_NAME
GIT_REPO_PATH							:= $(HOME)/$(GIT_REPO_NAME)
export GIT_REPO_PATH

ifeq ($(nocache),true)
NOCACHE								:= --no-cache
else
NOCACHE								:=	
endif
export NOCACHE

ifeq ($(verbose),true)
VERBOSE									:= --verbose
else
VERBOSE									:=	
endif
export VERBOSE

ifeq ($(port),)
PUBLIC_PORT								:=80
else
PUBLIC_PORT								:=$(port)
endif
export PUBLIC_PORT

.PHONY: help
help: test
	@echo ''
	@echo '	[USAGE]:	make [BUILD] run [EXTRA_ARGUMENTS]	'
	@echo ''
	@echo '		make help'
	@echo '		make report'
	@echo '		make image server nocache=false verbose=true'
	@echo ''
	@echo '	[EXAMPLES]:'
	@echo ''
	@echo '		SITE=~/bitcoincore.org make server'
	@echo '		SITE=~/bitcoincore.org make server nocache=false verbose=true'
	@echo '		SITE=~/bitcoincore.org make image server'
	@echo '		SITE=~/bitcoincore.org make image server nocache=false verbose=true'
	@echo ''

.PHONY: report
report: test
	@echo ''
	@echo '	[ARGUMENTS]	'
	@echo '      args:'
	@echo '        - HOME=${HOME}'
	@echo '        - PWD=${PWD}'
	@echo '        - SITE=${SITE}'
	@echo '        - TAG=${TAG}'
	@echo '        - ALPINE_VERSION=${ALPINE_VERSION}'
	@echo '        - GIT_USER_NAME=${GIT_USER_NAME}'
	@echo '        - GIT_USER_EMAIL=${GIT_USER_EMAIL}'
	@echo '        - GIT_SERVER=${GIT_SERVER}'
	@echo '        - GIT_PROFILE=${GIT_PROFILE}'
	@echo '        - GIT_BRANCH=${GIT_BRANCH}'
	@echo '        - GIT_HASH=${GIT_HASH}'
	@echo '        - GIT_REPO_ORIGIN=${GIT_REPO_ORIGIN}'
	@echo '        - GIT_REPO_NAME=${GIT_REPO_NAME}'
	@echo '        - GIT_REPO_PATH=${GIT_REPO_PATH}'
	@echo '        - NOCACHE=${NOCACHE}'
	@echo '        - VERBOSE=${VERBOSE}'
	@echo '        - PUBLIC_PORT=${PUBLIC_PORT}'

.PHONY: test
.SILENT:
test:
	bash -c "test -e $(SITE) && echo '' || 'SITE=$(SITE) doesnt exist!'"

DOCKER=docker
export DOCKER

ifeq ($(SITE),)
    #SITE       :=  $(PWD)
    SITE       :=$(HOME)/bitcoincore.org
    export     SITE
    TAG        := $(shell echo $(notdir $(SITE)) | awk '{print tolower($$0)}')
else
    SITE       := $(SITE)
    TAG        := $(shell echo $(notdir $(SITE)) | awk '{print tolower($$0)}')
endif
    export     SITE
    export     TAG

.PHONY: init
init:
	curl https://raw.githubusercontent.com/bitcoin-core/bitcoincore.org/master/Gemfile -o gemfile.temp
	temp=$(<gemfile.temp) && modified="${temp//2.5.5/2.5.8}" && echo $(modified) > bitcoincore.org.gemfile

# Build the docker image or create your own Dockerfile
.PHONY: image
image:test image_alpine init
	${DOCKER} build -t ${TAG} .
.PHONY: image_alpine
image_alpine:
	${DOCKER} build $(VERBOSE) $(NOCACHE) -t ${TAG} . -f Dockerfile.alpine
.PHONY: shell
shell:
	${DOCKER} run --rm -it \
		-p $(PUBLIC_PORT):4000 \
		-u `id -u`:`id -g` \
		-v ${PWD}/docs:/src/gh/pages-gem \
		-v `realpath ${SITE}`:/src/site \
		-w /src/site \
		${TAG} \
		/bin/bash
.PHONY: server serve
serve: server
server: image
	test -d "${SITE}" || \
		(echo -E "EXAMPLE USAGE: SITE=~/bitcoincore.org make server"; exit 1) && \
	${DOCKER} run --rm -it \
		-p $(PUBLIC_PORT):4000 \
		-u `id -u`:`id -g` \
		-v ${PWD}/docs:/src/gh/pages-gem \
		-v `realpath ${SITE}`:/src/site \
		-w /src/site \
		${TAG}
	|| echo 'Image(s) for "$(TAG)" does not exist.'
#######################
.PHONY: clean
clean:
	@echo 'clean'
	bash -c 'docker rmi -f $(TAG)'
	@docker rmi -f $(TAG) \
	&& echo 'Image(1) for "$(TAG)" removed.' \
	&& echo 'Image(2) for "$(TAG)" removed.' \
	|| echo 'Image(3) for "$(TAG)" already removed.'
#######################

