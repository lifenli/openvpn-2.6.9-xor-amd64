<h1>OpenVPN 2.6.9 Client package compiled with XOR patch for Ubuntu/Debian </h1>
NOTE: The XOR patch is employed to enable scramble obfuscation, catering specifically to restricted countries.


<h3>OpenVPN 2.6.9 gzip file and the Tunnelblick XOR patches can be obtained on</h3>
<a href="https://github.com/Tunnelblick/Tunnelblick/tree/master/third_party/sources/openvpn/openvpn-2.6.9">github-tunnelblick</a>

<h2>Download and Install:</h2>

<code>wget https://github.com/lifenli/openvpn-2.6.9-xor-amd64/raw/main/openvpn-2.6.9-xor-amd64.deb
sudo dpkg -i openvpn-2.6.9-xor-amd64.deb</code>


++++++++++++++++++++++++++++++++++++++++++++++++++++

<h2>If you wish to compile it by yourself, here are the steps:</h2>
<div>
  
1. Download the gzip file for openvpn 2.6.9:

  <code>wget https://github.com/Tunnelblick/Tunnelblick/raw/master/third_party/sources/openvpn/openvpn-2.6.9/openvpn-2.6.9.tar.gz </code>

2. Fetch the Xor patch files for Tunnelblick, install the unzip utility, and extract the downloaded archive

<code>wget https://github.com/Tunnelblick/Tunnelblick/archive/master.zip
sudo apt-get install unzip
unzip master.zip</code>

3. Copy the patch files into the OpenVPN directory:

<code>cp Tunnelblick-master/third_party/sources/openvpn/openvpn-2.6.9/patches/*.diff openvpn-2.6.9 </code>

4. Apply the patches:

<code>cd openvpn-2.6.9
patch -p1 < 02-tunnelblick-openvpn_xorpatch-a.diff
patch -p1 < 03-tunnelblick-openvpn_xorpatch-b.diff
patch -p1 < 04-tunnelblick-openvpn_xorpatch-c.diff
patch -p1 < 05-tunnelblick-openvpn_xorpatch-d.diff
patch -p1 < 06-tunnelblick-openvpn_xorpatch-e.diff</code>

5. Install the prerequisites for the build:

<code>sudo apt-get install build-essential libssl-dev iproute2 liblz4-dev liblzo2-dev libpam0g-dev libpkcs11-helper1-dev libsystemd-dev resolvconf pkg-config</code>

6. configure the build process to include support for systemd integration, asynchronous push operations, and iproute2 networking utility suite integration:

<code>./configure --enable-systemd --enable-async-push --enable-iproute2</code>

7. If it shows "libcao-ng package" not found (skip and proceed to step 8 otherwise):

<code>sudo apt-get install libcap-ng0
sudo apt-get install libcap-dev</code>

8. Reconfigure the build process, make and install the package:

<code>./configure --enable-systemd --enable-async-push --enable-iproute2
make
sudo make install
sudo mkdir /etc/openvpn
sudo mkdir /etc/openvpn/server
sudo mkdir /etc/openvpn/client</code>
</div>
<br/>
<br/>
This repository contains a compiled OpenVPN package based on the Tunnelblick project, which is licensed under the GNU General Public License v2.0.
The compiled OpenVPN package in this repository is also licensed under the GNU General Public License v2.0.
For more information, please see refer to <a href="https://github.com/Tunnelblick/Tunnelblick/blob/master/COPYING">TunnelBlick License</a>
