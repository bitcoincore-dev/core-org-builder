---
title: "core-org-builder"
layout: home
permalink: /
author_profile: false

---

<html>
<head>
  <link rel="stylesheet" href="/assets/css/style.css">
</head>
</html>

[![CI](https://github.com/bitcoincore-dev/core-org-builder/actions/workflows/push.yml/badge.svg)](https://github.com/bitcoincore-dev/core-org-builder/actions/workflows/push.yml)
=======

### Install [docker](https://docs.docker.com/get-docker/)		
### Install [make](https://www.gnu.org/software/make/)

```
git clone https://github.com/bitcoincore-dev/core-org-builder.git ~/core-org-builder
git clone https://github.com/bitcoincore-dev/bitcoincore.org.git ~/bitcoincore.org
cd core-org-builder

make image
make server port=4444 #serve ./docs
SITE=~/bitcoincore.org make server port=1234 #serve bitcoincore.org
```

## License

Distributed under the [MIT License](https://raw.githubusercontent.com/bitcoincore-dev/core-org-builder/master/LICENSE){: .btn .btn--primary}.
