---
title: "org-builder"
layout: home
permalink: /
title: "bitcoincore-dev"
author_profile: false

---

<html>
<head>
  <link rel="stylesheet" href="/assets/css/style.css">
</head>
</html>

[![Build Status](https://travis-ci.org/bitcoincore-dev/org-builder.svg?branch=master)](https://travis-ci.org/bitcoincore-dev/org-builder)

Install [docker](https://docs.docker.com/get-docker/)	
Install [make](https://www.gnu.org/software/make/)


then

```
git clone https://github.com/bitcoincore-dev/org-builder.git
cd org-builder

make image
make server
OR
SITE=. make image
SITE=. make server
OR
SITE=<path_to_jekyll_project> make image
SITE=<path_to_jekyll_project> make server
```

## License

Distributed under the [MIT License](https://raw.githubusercontent.com/RandyMcMillan/pages-gem/master/LICENSE){: .btn .btn--primary}.
