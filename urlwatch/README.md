# Urlwatch

urlwatch is intended to help you watch changes in webpages and get notified (via e-mail, in your terminal or through various third party services) of any changes. The change notification will include the URL that has changed and a unified diff of what has changed.

## Docker-compose

```
    urlwatch:
        container_name: Urlwatch
        volumes:
            - 'LOCALFOLDER:/root/.urlwatch:rw'
        restart: unless-stopped
        image: 'jpdsc/urlwatch'
```

## urls.yaml

Configure the URLs in this file. The file can be found in
```
/root/.urlwatch
```
If the file idoes not exist; create it inside the above folder. Example below on the contents.

```
---

url: "https://github.com/thp/urlwatch/releases/latest"
filter:
- xpath: '(//div[contains(@class,"release-timeline-tags")]//h4)[1]/a'
- html2text: re

---

url: "https://github.com/shadowsocks/shadowsocks-libev/releases/latest"
filter:
- css: 'div.f1>a'
- html2text: re

---
```

## urlwatch.yaml
This file is generated after the first CRON ran (30 minutes).
Here you can change the configuration of urlwatch. Consult the documentation in the reference section for explanation.


## Cron
By default, 30 minutes CRON is added. To change, use "crontab -e" and edit the line.

## References

Documentation: https://urlwatch.readthedocs.io/
