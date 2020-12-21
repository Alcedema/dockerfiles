# Urlwatch

urlwatch is intended to help you watch changes in webpages and get notified (via e-mail, in your terminal or through various third party services) of any changes. The change notification will include the URL that has changed and a unified diff of what has changed.

## Current version

```
21/12/2020
2.22
- Added 'wait_until' option to browser jobs to configure how long
  the headless browser will wait for pages to load.
- Jobs now have an optional `treat_new_as_changed` (default `false`)
  key that can be set, and will treat newly-found pages as changed,
  and display a diff from the empty string (useful for `diff_tool`
  or `diff_filter` with side effects)
- New reporters: `discord`, `mattermost`
- New key `user_visible_url` for URL jobs that can be used to show
  a different URL in reports (useful if the watched URL is a REST API
  endpoint, but the report should link to the corresponding web page)
- The Markdown reporter now supports limiting the report length via the
  `max_length` parameter of the `submit` method. The length limiting logic is
  smart in the sense that it will try trimming the details first, followed by
  omitting them completely, followed by omitting the summary. If a part of the
  report is omitted, a note about this is added to the report. (PR#572, by
  Denis Kasak)
```

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
If the file idoes not exist; create it inside the above folder or download it here: https://github.com/jpdsceu/dockerfiles/blob/master/urlwatch/files/urls.yaml. Example below on the contents.

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
This file is generated after the first CRON ran (30 minutes) or downloaded here: https://github.com/jpdsceu/dockerfiles/blob/master/urlwatch/files/urlwatch.yaml
Here you can change the configuration of urlwatch. Consult the documentation in the reference section for explanation.


## Cron
By default, 30 minutes CRON is added. To change, use "crontab -e" and edit the line.
Keep in mind that when updating the image; the original CRON is used. If you have changed crontab do not forget to change it back.
I will most likely remove the automated cron and add the information in the README.md file.

## References

Documentation: https://urlwatch.readthedocs.io/

Developer and all credits to: https://thp.io/2008/urlwatch/
