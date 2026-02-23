# Anti-Hijack AI Monitor (macOS)

Defensive monitor that helps detect signs of DNS/Proxy/Hosts/Gateway/TLS tampering that can affect Safari or any browser.

## What it detects
- DNS resolver changes + heuristic DNS risk hints
- System proxy changes (HTTP/HTTPS proxies)
- `/etc/hosts` modifications
- Default gateway changes + gateway MAC changes (ARP spoof/MITM signal)
- TLS certificate fingerprint changes for pinned domains
- **AI anomaly scoring** (baseline learning + robust z-score over history)

## Install / Run
macOS already includes Python 3 on most systems, otherwise install it.

### Run once (create/update baseline)
```bash
python3 anti_hijack_ai_monitor.py --once
```

### Watch mode (every 30 seconds)
```bash
python3 anti_hijack_ai_monitor.py --watch --interval 30
```

### Watch mode with AI anomaly detection
```bash
python3 anti_hijack_ai_monitor.py --watch --interval 30 --ai
```

### Pin your own domains (comma-separated)
```bash
python3 anti_hijack_ai_monitor.py --watch --interval 30 --ai --domains "apple.com,icloud.com,yourdomain.com"
```

## Output files
- `~/.anti_hijack_ai/state.json`   (latest snapshot)
- `~/.anti_hijack_ai/history.jsonl` (time series history)
- `~/.anti_hijack_ai/alerts.log`    (alerts)

## Safety
This tool is **defensive-only** (monitoring + alerting). It does **not** attempt to disrupt, hijack, or tamper with any network.
