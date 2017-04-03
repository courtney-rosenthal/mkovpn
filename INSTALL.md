# mkovpn Installation

The mkovpn package uses the "Easy RSA" certificate authority (CA) package,
part of the OpenVPN distribution, to manage client certificates and keys.

The installation steps for this package are:

1. Initialize the "Easy RSA" certificate authority (CA) package.
2. Create a "BASE.ovpn" file.
3. Retrieve the "ta.key" file from the OpenVPN server.

## Initialize the "Easy RSA" certificate authority (CA) package

You can either setup an "Easy RSA" certificate authority from scratch,
or configure this package to use one that you've previously setup.

### Setup an "Easy RSA" certificate authority from scratch

Initialize the CA by running from the base directory of this project:
      
    git clone https://github.com/OpenVPN/easy-rsa.git
    cd easy-rsa/easyrsa3
    ./easyrsa init-pki
    ./easyrsa build-ca nopass

Leave off the "nopass" if you would prefer to place a passphrase on
the CA key -- which will be needed every time you create a new client
certificate.

### Configure this package to existing "Easy RSA" certificate authority

Simply edit the "mkovpn" script and adjust the "$BASEDIR_EASYRSA"
definition to point to your existing Easy RSA installation.


## Create a "BASE.ovpn" file

Copy the distributed "BASE.ovpn.example" to "BASE.ovpn" and configure
for your VPN server. In the common case, you'll just need to adjust the
"remote" directive with correct host, port, and protocol.


## Retrieve the "ta.key" file from the OpenVPN server

This package assumes that you are using a "TLS Key" for added
security. This would have been generated on your OpenVPN server with a
command such as:

    openvpn --genkey --secret ta.key

Retrieve the "ta.key" file and save it in the package base directory.
Secure the file by running:

    chmod 400 ta.key


## Generate your first client certificate

You are now ready to generate your first client certificate. Run
a command such as:

    ./mkovpn create "Test Client 1"

