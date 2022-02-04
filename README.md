# docker-paperless

This repository contains the docker-compose and backup configurations to run oluhome media self-hosted services

## Services

* Paperless (web front-end)
* Redis (broker)
* Postgres (DB)
* Tika / Gotenberg (Office document support)
* Diun (Docker updates)

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
sudo ln -s ~/docker-paperless/systemd/oluhome-paperless-backup.service /etc/systemd/system/oluhome-paperless-backup.service
sudo ln -s ~/docker-paperless/systemd/oluhome-paperless-backup.timer /etc/systemd/system/oluhome-paperless-backup.timer
```

5. Enable and start the oluhome-paperless-backup systemd timer:

```
sudo systemctl enable oluhome-paperless-backup.timer
sudo systemctl start oluhome-paperless-backup.timer
```
6. Start containers with `docker-compose up -d`