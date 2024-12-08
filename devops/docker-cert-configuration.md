# Linux certificate default locations

## System-wide Trusted Certificates (for general use)

create .cert file and place in this directory.
/usr/local/share/ca-certificates/
sudo update-ca-certificates


## Web Server

/etc/ssl/certs/
/etc/ssl/private/

## For user specific Trust

~/.local/share/ca-certificates/

update-ca-certificates --fresh

## For Java Application

sudo keytool -import -file my-cert.crt -keystore /path/to/your/keystore.jks -alias my-cert

## Docker certificate path
/etc/docker/certs.d/<registry_name>/

## Where <registry_name> is the hostname or domain of the registry. For example,
## if you're using a private Docker registry hosted at my-registry.local, the certificate should be placed at:

/etc/docker/certs.d/my-registry.local/ca.crt
sudo systemctl restart docker

## Download certificate

openssl s_client -connect hub.valentine.sfr.com:443 </dev/null | sed -n -e '/-.BEGIN/,/-.END/ p' > SFRValentine.crt