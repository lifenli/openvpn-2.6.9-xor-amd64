<h1>OpenVPN 2.6.9 Client package compiled with XOR patch for Ubuntu/Debian </h1>

<h3>OpenVPN 2.6.9 gzip file and the Tunnelblick XOR patch can be obtained on</h3>
<a>https://github.com/Tunnelblick/Tunnelblick/tree/master/third_party/sources/openvpn/openvpn-2.6.9 </a>

<h2>Installation:</h2>

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

3.Copy the patch files into the OpenVPN directory:

<code>cp Tunnelblick-master/third_party/sources/openvpn/openvpn-2.6.9/patches/*.diff openvpn-2.6.9 </code>

4 Apply the patches:

<code>cd openvpn-2.6.9
patch -p1 < 02-tunnelblick-openvpn_xorpatch-a.diff
patch -p1 < 03-tunnelblick-openvpn_xorpatch-b.diff
patch -p1 < 04-tunnelblick-openvpn_xorpatch-c.diff
patch -p1 < 05-tunnelblick-openvpn_xorpatch-d.diff
patch -p1 < 06-tunnelblick-openvpn_xorpatch-e.diff</code>

5 Install the prerequisites for the build:

<code>sudo apt-get install build-essential libssl-dev iproute2 liblz4-dev liblzo2-dev libpam0g-dev libpkcs11-helper1-dev libsystemd-dev resolvconf pkg-config</code>

6 - Build, make, and install OpenVPN with Xor patch:

<code>./configure --enable-systemd --enable-async-push --enable-iproute2</code>

If it shows libcao-ng package not found:

<code>sudo apt-get install libcap-ng0
sudo apt-get install libcap-dev</code>

And then run the following commands again:

<code>./configure --enable-systemd --enable-async-push --enable-iproute2
make
sudo make install
sudo mkdir /etc/openvpn
sudo mkdir /etc/openvpn/server
sudo mkdir /etc/openvpn/client</code>
</div>
