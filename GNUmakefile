DOCKER=docker
export DOCKER
ifeq ($(SITE),)
    SITE   := .
    export SITE
    TAG        := org-builder
    export     TAG
else
    SITE       := $(SITE)
    export     SITE
    TAG        := $(shell echo $(notdir $(SITE)) | awk '{print tolower($$0)}')
    export     TAG
endif
.PHONY: image image_alpine shell server clean
# Build the docker image or create your own Dockerfile
image:image_alpine
	${DOCKER} build -t ${TAG} .
image_alpine:
	${DOCKER} build -t ${TAG} . -f Dockerfile.alpine
# make image or server first
# use SITE= to point to the container
# Example
# SITE=~/Bitcoin.org make image
# OR
# SITE=~/Bitcoin.org make server
# SITE=~/Bitcoin.org make shell
shell:
	${DOCKER} run --rm -it \
		-p 4000:4000 \
		-u `id -u`:`id -g` \
		-v ${PWD}/docs:/src/gh/pages-gem \
		-v `realpath ${SITE}`:/src/site \
		-w /src/site \
		${TAG} \
		/bin/bash
# Spawn a server. Specify the path to the SITE directory by
# exposing it using `expose SITE="../path-to-jekyll-site"` prior to calling or
# by prepending it to the make rule e.g.: `SITE=../path-to-site make server`
server: image
	test -d "${SITE}" || \
		(echo -E "specify SITE e.g.: SITE=/path/to/site make server"; exit 1) && \
	${DOCKER} run --rm -it \
		-p 4000:4000 \
		-u `id -u`:`id -g` \
		-v ${PWD}/docs:/src/gh/pages-gem \
		-v `realpath ${SITE}`:/src/site \
		-w /src/site \
		${TAG}
	|| echo 'Image(s) for "$(TAG)" does not exist.'
#######################
clean:
	@echo 'clean'
	bash -c 'docker rmi -f $(TAG)'
	@docker rmi -f $(TAG) \
	&& echo 'Image(1) for "$(TAG)" removed.' \
	&& echo 'Image(2) for "$(TAG)" removed.' \
	|| echo 'Image(3) for "$(TAG)" already removed.'
#######################
-include Makefile

