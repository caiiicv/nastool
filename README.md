version: '3'
services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
    restart: always
    ports:
      - "8096:8096"
    volumes:
      - "/docker/jellyfin/config:/config"
      - "/docker/jellyfin/cache:/cache"
      - "/docker/media:/media"
  qbittorrent:
    image: linuxserver/qbittorrent:latest
    container_name: qbittorrent
    restart: always
    ports:
      - "6881:6881"
      - "6881:6881/udp"
      - "8078:8080"
    environment:
      - PUID=0
      - PGID=0
      - TZ=Europe/London
      - WEBUI_PORT=8078
    volumes:
      - "/docker/qBittorrent/config:/config"
      - "/docker/media/Downloads:/downloads"
  nastool:
    image: razeencheng/nastool:2.9.1
    container_name: nastool
    restart: always
    ports:
      - "3000:3000"
    environment:
      - PUID=0
      - PGID=0
      - UMASK=000
      - NASTOOL_AUTO_UPDATE=false
      - NASTOOL_CN_UPDATE=false
    volumes:
      - "/docker/Nastool/config:/config"
      - "/docker/media:/media"
      - "/docker/qBittorrent/Downloads:/downloads"
