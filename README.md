# dev-services

> A bundled traefik / dnsmasq service, with an example www site

## Getting started

Create a `.env` file with the following contents:

```sh
DOMAIN=<your preferred domain>
DNS_USERNAME=<username for dns web manager>
DNS_PASSWORD=<password for dns web manager>
```

Make sure you update the dnsmasq config with the domain name! Currently looking for a way to automate this.
An example is provided in `dnsmasq.conf-EXAMPLE`. Copy this to `dnsmasq.conf` and set the domain.

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
