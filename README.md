# homelab

Docker stacks for a single Raspberry Pi 4 (4 GB). One directory per service under `stacks/`,
each with a `compose.yaml` and an `.env.example`. Design and decisions: see the project brief.

## Port map

| Service | URL on the Pi | Notes |
|---|---|---|
| Dozzle | :8888 | Logs. No auth |
| Jellyfin | :8096 | Keep this LAN port open for TVs |
| Mealie | :9925 | |
| Syncthing | :8384 (GUI), :22000, :21027/udp | Host networking |
| MeTube | :8081 | |
| Uptime Kuma | :3001 | |
| Diun | none | Notifier config in `.env` |

## Expected on-disk layout

- `/opt/homelab` this repo
- `/srv/appdata/<service>` state (back this up)
- `/srv/media` media (HDD mount point, later)
- `/srv/downloads` MeTube downloads

## First run, per service

- **Uptime Kuma:** create the admin account on first visit.
- **Jellyfin:** run the setup wizard. Library stays empty until media exists.
- **Mealie:** change the default admin login immediately (see Mealie docs for the default).
- **Syncthing:** set a GUI password immediately. It listens on all interfaces.
- **Dozzle:** no login. Anyone on the LAN can read every container's logs.
- **Diun:** add a notifier to `.env`, then `docker compose up -d`.

## Not covered yet

`bootstrap.sh` (creates the directories above with correct ownership, installs Docker and
Tailscale, copies each `.env.example` to `.env`, brings stacks up), backups, HDD mounts.
