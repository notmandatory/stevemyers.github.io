---
layout: post
title:  "BitcoinXT gitian-debian build package systemd change"
date:   2015-08-27 09:34:00
categories: blog bitcoin
---
I just completed a commit to a new open source project, [BitcoinXT](https://bitcoinxt.software/). The commit is a set of changes to a script that creates a debian package file which installs a set of binaries created via the [gitian](https://gitian.org/) method. The overall scope was small but a good opportunity for me to learn how systemd services and the debian packaging system work.  It was also a fun starter project due to the great feedback from [Mike Hearn](https://github.com/mikehearn) and other committers on the team. You can see how the change evolved through the comments on the github pull request ([bitcoinxt/pull/46](https://github.com/bitcoinxt/bitcoinxt/pull/46)).
