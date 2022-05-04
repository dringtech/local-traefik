# local-traefik

> A bundled traefik / dnsmasq service, with an example www site

## Getting started

Have docker and docker compose installed!

Create a `.env` file with the following contents:

```sh
DOMAIN=<your preferred domain>
DNS_USERNAME=<username for dns web manager>
DNS_PASSWORD=<password for dns web manager>
```

Make sure you update the dnsmasq config with the domain name! Currently looking for a way to automate this.
An example is provided in `dnsmasq.conf-EXAMPLE`. Copy this to `dnsmasq.conf` and set the domain.

Create the dev network using `docker network create dev`.

Run `docker-compose up -d` from the root directory of the repo.

Check that you can access:

* Traefik - <`http://localhost:8080`> or `https://traefik.<YOUR DOMAIN>`
* `https://dns.<YOUR DOMAIN>` (Login with the username and password you set)

Start the test-www service using `docker-compose -f test-www.yaml up` then check you can access
`https://test-www.<YOUR DOMAIN>`. (It should say "Hello world!", of course!)

## Securing

> https://github.com/Heziode/traefik-v2-https-ssl-localhost

```
mkcert -install
```

Generate certificate for your domain and their sub-domains.

```
mkcert -cert-file certs/local-cert.pem -key-file certs/local-key.pem "<your preferred domain>" "*.<your preferred domain>"
```

## Registering resolver in MacOS Monterey

Create resolver file named for the domain you defined above e.g. `/etc/resolver/localdev.example.com`.

The contents if this file should be

```
nameserver 127.0.0.1
port 10053
```

Testing:

* Check that it appears in the list of resolvers shown by `scutil --dns`.
* Check that it resolves properly with `dig @127.0.0.1 -p 10053 www.localdev.example.com`
