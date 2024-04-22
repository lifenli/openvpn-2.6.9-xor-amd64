<h1>OpenVPN 2.6.9 Client package compiled with XOR patch for Ubuntu/Debian </h1>
NOTE: The XOR patch is employed to enable scramble obfuscation, catering specifically to restricted countries.

<h3>OpenVPN 2.6.9 gzip file and the Tunnelblick XOR patches can be obtained on</h3>
<a href="https://github.com/Tunnelblick/Tunnelblick/tree/master/third_party/sources/openvpn/openvpn-2.6.9">github-tunnelblick</a>

<h2>Download and Installation:</h2>

<code>wget https://github.com/lifenli/openvpn-2.6.9-xor-amd64/raw/main/openvpn-2.6.9-xor-amd64.deb
sudo dpkg -i openvpn-2.6.9-xor-amd64.deb</code>


++++++++++++++++++++++++++++++++++++++++++++++++++++

<h2>If you wish to compile it by yourself, here are the steps:</h2>
<div>
  
1. Download the gzip file for openvpn 2.6.9

  <code>wget https://github.com/Tunnelblick/Tunnelblick/raw/master/third_party/sources/openvpn/openvpn-2.6.9/openvpn-2.6.9.tar.gz </code>

2. Get the Tunnelblick versions of the Xor patch files:

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

6. configures the software build process to include support for systemd integration, asynchronous push operations, and iproute2 networking utility suite integration:

<code>./configure --enable-systemd --enable-async-push --enable-iproute2</code>

7. If it shows "libcao-ng package" not found:

<code>sudo apt-get install libcap-ng0
sudo apt-get install libcap-dev</code>

8. Reconfig for build, make and install the package:

<code>./configure --enable-systemd --enable-async-push --enable-iproute2
make
sudo make install
sudo mkdir /etc/openvpn
sudo mkdir /etc/openvpn/server
sudo mkdir /etc/openvpn/client</code>
</div>
