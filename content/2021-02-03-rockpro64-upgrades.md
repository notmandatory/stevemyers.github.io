+++
template = "post.html"
title = "ROCKPro64 System, Updates"

[taxonomies]
tags = ["pine64", "linux", "bitcoin"]
categories = ["blog"]
+++

It's been a few months since I last worked on my ROCKPro64 system so today I did some overdue 
updates. The main impetus for updating was to make sure my system security isn't at risk due to 
the recently announced `sudo` vulnerability [CVE-2021-3156]. Even though I'm the only user on my 
little server it's best to not take any chances. 

The other important update I wanted to do is to bring my `bitcoind` daemon up to the latest and 
greatest version [bitcoin core 0.21.0].

[CVE-2021-3156]: https://blog.qualys.com/vulnerabilities-research/2021/01/26/cve-2021-3156-heap-based-buffer-overflow-in-sudo-baron-samedit
[bitcoin core 0.21.0]: https://bitcoin.org/en/release/v0.21.0  

1. upgrade OS packages

   ```shell
   sudo apt update
   sudo apt upgrade
   ```
   
1. verify `sudo` is patched. Per the [CVE-2021-3156] FAQ if your system is vulnerable the below 
   command will respond with an error that starts with “sudoedit:”. If your system is patched, it 
   will respond with an error that starts with “usage:”

   ```shell
   sudoedit -s / 
   ```

1. update `bitcoin` core git repo and checkout the `v0.21.0` tag

   ```shell
   cd git/bitcoin ## or where ever you keep your bitcoin core repo clone
   git fetch --all
   git checkout v0.21.0
   ```     
   
1. re-build `bitcoind` this time without the wallet, I only need a P2P node

   ```shell
   ./autogen.sh
   ./configure --without-gui --disable-wallet 
   make
   strip src/bitcoind
   strip src/bitcoin-cli
   ```
   
   Note: if I cross-compiled this ARM build on my desktop linux system it should go a lot faster,
   I will try that next time

1. install the bitcoin binaries

   ```shell
   sudo systemctl stop bitcoind
   sudo install -sv src/bitcoind src/bitcoin-cli /usr/local/bin
   sudo chown bitcoin:bitcoin /usr/local/bin/bitcoin*
   ```

1. verify the new version of bitcoind is installed
   
   ```shell
   $ /usr/local/bin/bitcoind --version
   Bitcoin Core version v0.21.0
   Copyright (C) 2009-2020 The Bitcoin Core developers
   
   Please contribute if you find Bitcoin Core useful. Visit
   <https://bitcoincore.org/> for further information about the software.
   The source code is available from <https://github.com/bitcoin/bitcoin>.
   
   This is experimental software.
   Distributed under the MIT software license, see the accompanying file COPYING
   or <https://opensource.org/licenses/MIT>
   ```
   
1. restart bitcoind and verify it started up successfully 

   ```shell
   sudo systemctl start bitcoind
   sudo systemctl status bitcoind
   sudo tail -f /var/lib/bitcoind/debug.log ## stop tail with control-C
   ```