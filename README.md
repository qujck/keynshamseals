# keynshamseals.org

The website of Keynsham Seals Disabled Swimming Club: plain HTML and CSS, with no build step, framework or
database.

| File | What it is |
|---|---|
| `index.html` | Home: when and where the club swims, who it is for, families' words, joining, contact |
| `50-years.html` | The 50th birthday (Sunday 18 October 2026) and the club's story since 1976 |
| `css/site.css` | The one stylesheet |
| `img/seal.svg` | Logo and favicon |
| `deploy/keynshamseals.conf` | The port-80 Apache site on qujck.com. Certbot added `keynshamseals-le-ssl.conf` (HTTPS) and the redirect from HTTP. |

## Preview

```
python3 -m http.server 8095 --bind 127.0.0.1    # then open http://localhost:8095
```

## Publish

The site is served by Apache on qujck.com from `/var/www/keynshamseals` (owned by `www-data`). The server
also hosts other live sites, so only that folder is changed.

```
rsync -a --delete --exclude .git --exclude deploy --exclude README.md ./ qujck.com:keynshamseals-upload/
ssh qujck.com 'sudo rsync -a --delete ~/keynshamseals-upload/ /var/www/keynshamseals/ && sudo chown -R www-data:www-data /var/www/keynshamseals'
```

DNS is on Cloudflare: `@` and `www` are proxied to qujck.com (`206.189.247.167`), with SSL set to Full (strict).
The origin certificate is Let's Encrypt, renewed by certbot's timer. After publishing, Cloudflare may serve
cached copies for a while; purge the cache in Cloudflare to see a change at once.

## Content

Facts come from the BBC article "'Lifeline' swimming group celebrating 50 years" (18 October 2026) and the
council's Live Well listing. The contact details are the ones on that listing, confirmed for use by the club.
