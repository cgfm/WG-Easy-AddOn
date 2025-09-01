![Version](https://img.shields.io/badge/version-0.1.0-blue?style=for-the-badge)
![Architectures](https://img.shields.io/badge/arch-aarch64%20%7C%20amd64%20%7C%20armv7-5965E0?style=for-the-badge)
![Ingress](https://img.shields.io/badge/ingress-enabled-success?style=for-the-badge)
![Host Network](https://img.shields.io/badge/host%20network-true-ff69b4?style=for-the-badge)
![Supervisor](https://img.shields.io/badge/home%20assistant-add--on-41BDF5?style=for-the-badge)

# WG-Easy Add-on for Home Assistant

WG-Easy is a simple, self-hosted WireGuard VPN manager with a web UI. This add-on packages WG-Easy to run on your Home Assistant host, with Ingress support for convenient sidebar access.

## Quick Installation

[![Open your Home Assistant instance and show the add add-on repository dialog with a specific repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/_change/?redirect=supervisor_add_addon_repository%2F%3Frepository_url%3Dhttps%253A%252F%252Fgithub.com%252Fcgfm%252FWG-Easy-AddOn)

## How To Use

- Add this repository to your Home Assistant add-on store using the URL of this Git repository.
- Install the add-on named "WG-Easy" from the store.
- Configure at least `wg_host`, then start the add-on.
- Access the UI via the Home Assistant sidebar (Ingress) or directly at `http://<home-assistant-host>:51821`.

## Configuration

- wg_host: Public host (WG_HOST). Domain name or public IP that clients use to reach your server. Example "vpn.example.com" or "203.0.113.10". Required if auto-detection fails.
- password: Admin UI password. Protects the WG-Easy web UI. Leave empty to disable authentication.
- wg_port: WireGuard UDP port. Forward this on your router/firewall if clients connect from the internet. Default 51820.
- allowed_ips: Allowed IPs (client routes). Comma-separated CIDRs pushed to clients. Use "0.0.0.0/0, ::/0" for full-tunnel, or e.g. "192.168.1.0/24" for split-tunnel.
- default_dns: Default DNS servers. Comma-separated DNS servers to include in client configs. Example "1.1.1.1, 1.0.0.1".
- mtu: Interface MTU. MTU for the WireGuard interface. Lower (e.g. 1280-1420) if you experience fragmentation.
- persistent_keepalive: Persistent keepalive (seconds). Set 0 to disable; 25 is common for NAT traversal.
- max_clients: Maximum clients. Upper limit on number of peers.

## Notes

- Requires `/dev/net/tun` and `NET_ADMIN` to run WireGuard; runs with host networking.
- WireGuard keys and configuration persist under the add-on's `/data` volume.
- If `wg_host` is left empty, the add-on attempts to fall back to the host's primary IP; set your public hostname/IP explicitly for remote access.

## Ingress & Sidebar

- Ingress is enabled and the add-on registers a sidebar item titled "WG-Easy" with the `mdi:shield-key` icon.
- You can still reach the UI directly on TCP `51821` if preferred.

## Project Links

- Upstream WG-Easy: https://github.com/wg-easy/wg-easy
- Defaults: UDP 51820 (WireGuard), TCP 51821 (Web UI)

## Translations
- Available languages: English (`en`), German (`de`), French (`fr`), Spanish (`es`).
- Files live under `wg-easy/translations/` and map friendly names/descriptions for each config option in the Supervisor UI.
- Contributions welcome: add a new `<lang>.yaml` mirroring `en.yaml`.
