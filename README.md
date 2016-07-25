## Installing Puppet Enterprise on Redhat/CentOS

1. Download *nix tarball
```
#!/bin/bash

# Download pe and extract to DL_DIR

DL_DIR=/opt/pe/install
TMP_DIR=$(mktemp -d)
mkdir -p ${TMP_DIR} ${DL_DIR}/latest

# detect arch and release
DIST_ARCH_RELEASE=$(rpm -q --qf "ver=latest&dist=el&arch=%{arch}&rel=%{version}" -f /etc/redhat-release)

# build uri
PE_URI="https://pm.puppetlabs.com/cgi-bin/download.cgi?${DIST_ARCH_RELEASE}"

# download tarball
curl -L -o ${TMP_DIR}/pe-latest.tar.gz ${PE_URI}

# get filename from tarball
PE_TARBALL=$(zcat ${TMP_DIR}/pe-latest.tar.gz | head -n1 | cut -d/ -f1)
mv ${TMP_DIR}/pe-latest.tar.gz ${DL_DIR}/latest/${PE_TARBALL}.tar.gz

# extract
mkdir ${DL_DIR}/${PE_TARBALL}
tar -xvzf ${DL_DIR}/latest/${PE_TARBALL}.tar.gz -C ${DL_DIR}/${PE_TARBALL}

# tidy
rm -Rf ${TMP_DIR}
```
