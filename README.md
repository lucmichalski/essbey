# OPENVPN

    $> export CIPHER="AES-256-CBC"
    $> docker-compose run --rm openvpn ovpn_genconfig -u udp://VPN.SERVERNAME.COM:PORT -2 -C $CIPHER -n <pihole_ip> -e 'management 0.0.0.0 5555' -e 'push "redirect-gateway def1 bypass-dhcp"' -e 'management 0.0.0.0 5555' -e 'push "comp-lzo no"'
    $> docker-compose run --rm openvpn ovpn_initpki
    $> sudo chown -R $(whoami): ./config/openvpn
    $> docker-compose up -d openvpn

    $> export CLIENTNAME="your_client_name"
    $> docker-compose run --rm openvpn easyrsa build-client-full $CLIENTNAME
    $> docker-compose run --rm openvpn ovpn_getclient $CLIENTNAME > $CLIENTNAME.ovpn

[link](https://github.com/kylemanna/docker-openvpn/issues/496) if cannot create client file

# Certificates

    $> cd config/traefik/certs
    $> DOMAIN_CERT=your_domain/s sh ../create-website-cert.sh
    $> docker rm -f mkcert

# Sftp

    $> echo -n "your-password" | docker run -i --rm atmoz/makepasswd --crypt-md5 --clearfrom=-

# Nginx server names issue

    Visit https://superuser.com/questions/1093419/alias-for-ips-in-the-home-lan-network
# Start

    $> docker-compose up -d
