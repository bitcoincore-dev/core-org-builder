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

[![Build Status](https://travis-ci.org/bitcoincore-dev/org-builder.svg?branch=master)](https://travis-ci.org/bitcoincore-dev/org-builder)


Install [docker](https://docs.docker.com/get-docker/)	
Install [make](https://www.gnu.org/software/make/)


**then**

```
git clone https://github.com/bitcoincore-dev/org-builder.git ~
git clone https://github.com/bitcoin-dot-org/Bitcoin.org.git ~

cd org-builder

make image
make server

OR

SITE=~/Bitcoin.org make image
SITE=~/Bitcoin.org make server
```

--

## License

Distributed under the [MIT License](https://raw.githubusercontent.com/RandyMcMillan/pages-gem/master/LICENSE){: .btn .btn--primary}.
