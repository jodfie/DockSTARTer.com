# Youtube DL Server

[Youtube-dl Server](https://youtube-dl.org/) is a  command-line program to download videos from YouTube.com and a few more sites.

This is a override to start a container of Youtube-dl with a web GUI and REST interface.

The GIT Repository for Youtube-dl-server is located at [https://github.com/nbr23/youtube-dl-server](https://github.com/nbr23/youtube-dl-server)

## Example Docker Compose Override

```yaml
version: "3.4"
services:
  youtube-dl:
    container_name: youtube-dl
    hostname: ${DOCKERHOSTNAME}
    image: nbr23/youtube-dl-server
    ports:
        - 8083:8080
    environment:
        - PGID=${PGID}
        - PUID=${PUID}
        - TZ=${TZ}
        - YDL_OUTPUT_TEMPLATE=/downloads/%(title)s [%(id)s].%(ext)s
        - YDL_OUTPUT_TEMPLATE_PLAYLIST=/downloads/%(title)s [%(id)s].%(ext)s
    volumes:
        - /etc/localtime:/etc/localtime:ro
        - ${DOCKERCONFDIR}/youtube-dl:/youtube-dl
        - ${DOWNLOADSDIR}/youtube-dl:/downloads
    restart: unless-stopped
    logging:
        driver: json-file
        options:
            max-file: ${DOCKERLOGGING_MAXFILE}
            max-size: ${DOCKERLOGGING_MAXSIZE}
```
