---
Title: Installation and Usage of feh
Author: 邱彼郑楠
Date: 2025-06-11
---

# Installation

1. Install some dependencies:

```bash
apt install libimlib2-dev
apt install libcurl4-openssl-dev
apt install libxt-dev
```

2. Clone the repository from GitHub:

```git
git clone https://github.com/derf/feh.git
```

3. Install with `make`:

```bash
export flag=bool
make && make install
```

