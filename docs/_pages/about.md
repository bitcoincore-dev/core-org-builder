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
git clone https://github.com/bitcoin-core/bitcoincore.org.git ~/bitcoincore.org

cd core-org-builder

make image
make server

OR

SITE=~/bitcoincore.org make image
SITE=~/bitcoincore.org make server
```

--

## License

Distributed under the [MIT License](https://raw.githubusercontent.com/bitcoincore-dev/org-builder/master/LICENSE){: .btn .btn--primary}.
=======

