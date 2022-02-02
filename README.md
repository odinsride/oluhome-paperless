# oluhome-media

This repository contains the docker-compose and backup configurations to run oluhome media self-hosted services

## Services

* Jellyfin (Media Server)
* Transmission-OpenVPN (Downloader)
* Radarr (Movies PVR)
* Sonarr (TV PVR)
* Jackett (Indexer)
* Bazarr (Subtitles)
* Diun (Docker update notifier)

## Dependencies

* Built for Debian Bullseye
  - Can be adjusted for other Distros, primarily by configuring the proper default user groups for directories and systemd service(s)
* Docker
  - `Docker version 20.10.12, build e91ed57`
* Docker Compose
  - `docker-compose version 1.29.2, build 5becea4c`
* curl
* [Backblaze B2 CLI Tool](https://www.backblaze.com/b2/docs/quick_command_line.html) (Provided in `lib/vendor`)

## Setup

1. Clone Repository
2. Configure `.env` file with appropriate settings, example provided
3. Start containers / Stop containers (to generate config folders)
4. Symlink systemd services/timers:

```
sudo ln -s ~/docker/systemd/media-backup.service /etc/systemd/system/media-backup.service
sudo ln -s ~/docker/systemd/media-backup.timer /etc/systemd/system/media-backup.timer
```

5. Enable and start the media-backup systemd timer:

```
sudo systemctl enable media-backup.timer
sudo systemctl start media-backup.timer
```
6. Start containers with `docker-compose up -d`