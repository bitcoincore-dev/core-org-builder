---
title: "org-builder / about"
author_profile: false
permalink: /about/
title: "bitcoincore-dev"
---

<html>
<head>
  <link rel="stylesheet" href="/assets/css/style.css">
</head>
</html>

## Building environment for jekyll projects

[![CI](https://github.com/bitcoincore-dev/org-builder/actions/workflows/push.yml/badge.svg)](https://github.com/bitcoincore-dev/org-builder/actions/workflows/push.yml)
=======
[![Build Status](https://travis-ci.org/bitcoincore-dev/core-org-builder.svg?branch=master)](https://travis-ci.org/bitcoincore-dev/core-org-builder)


Install [docker](https://docs.docker.com/get-docker/)	
Install [make](https://www.gnu.org/software/make/)


**then**

```
git clone https://github.com/bitcoincore-dev/core-org-builder.git ~/core-org-builder
cd ~/core-org-builder && git fetch origin 1644282724-ruby-2-7-alpine3-14
git checkout 1644282724-ruby-2-7-alpine3-14

git clone https://github.com/bitcoin-core/bitcoincore.org.git ~/bitcoincore.org

cd ~/bitcoincore.org
git remote add sjors https://github.com/Sjors/bitcoincore.org.git
git fetch sjors && git checkout 2021/12/ruby

cd ~/core-org-builder

SITE=~/bitcoincore.org make image
SITE=~/bitcoincore.org make server
```

--

## License

Distributed under the [MIT License](https://raw.githubusercontent.com/bitcoincore-dev/org-builder/master/LICENSE){: .btn .btn--primary}.
=======

