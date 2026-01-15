Run dev server with fast render and cache disabled:

```bash
hugo serve --disableFastRender --ignoreCache
```

Run dev server accessible from other devices on your LAN (e.g. phone):

```bash
hugo server --disableFastRender --ignoreCache --bind 0.0.0.0
```

Notes:

- Replace `<YOUR_LAN_IP>` with your machine's local network IP (for example `192.168.1.42`).
- If you have a firewall enabled (e.g. `ufw`), allow inbound TCP on `1313`.