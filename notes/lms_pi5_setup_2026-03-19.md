# LMS + Pi5 Music System — Complete Setup Guide

**Date:** 2026-03-19
**Scope:** Weekend project. Isolated from business work.

## Architecture

```
Squeezer (Android)
    ↓ (control)
LMS Server (openclaw-box:9000)
    ↓ (stream)
Squeezelite (Pi5)
    ↓ (HDMI)
CORSAHD Audio Extractor
    ├── HDMI → Sony Bravia (video/passthrough)
    └── Optical/SPDIF → ONN Ultra soundbar (audio)
```

## Equipment

| Device | Spec |
|--------|------|
| LMS Server | openclaw-box (Intel i7-10700T, 62GB RAM, Ubuntu) |
| Player | Raspberry Pi 5, 8GB |
| Audio extractor | CORSAHD 8K HDMI 2.1 Audio Extractor (2-in-1-out, SPDIF + 3.5mm) |
| Soundbar | ONN Ultra (optical + HDMI + 3.5mm) |
| TV | Sony Bravia (HDMI from extractor) |
| Controller | Squeezer app (Android) |
| Pi5 network | WiFi |
| Pi5 OS | Raspberry Pi OS Lite 64-bit (Bookworm) |

---

## Part 1: Flash Pi5 SD Card

**On your computer (Mac/PC), using Raspberry Pi Imager:**

1. Download Raspberry Pi Imager: https://www.raspberrypi.com/software/
2. Insert SD card (32GB+ recommended)
3. Open Imager:
   - Device: Raspberry Pi 5
   - OS: **Raspberry Pi OS Lite (64-bit)** (under "Raspberry Pi OS (other)")
   - Storage: your SD card
4. Click the **gear icon** (or Edit Settings) before writing:
   - **Hostname:** `pi5-music`
   - **Enable SSH:** Yes (use password authentication)
   - **Username:** `david` (or whatever you prefer)
   - **Password:** (set something secure)
   - **Configure WiFi:** Yes
     - SSID: your WiFi network name
     - Password: your WiFi password
     - Country: US
   - **Locale:** America/Chicago, us keyboard
5. Write to SD card. Wait for verification.

---

## Part 2: Install LMS on openclaw-box

**Run on openclaw-box (needs sudo):**

```bash
# Install LMS (already downloaded to /tmp)
sudo dpkg -i /tmp/lyrionmusicserver_9.1.0_amd64.deb

# Fix any missing dependencies
sudo apt-get install -f -y
```

**Verify LMS is running:**

```bash
# Check service status
sudo systemctl status lyrionmusicserver

# Should be active (running)
```

**Access web UI:**
- From openclaw-box: http://localhost:9000
- From any device on the network: http://<openclaw-box-ip>:9000

**If LMS isn't accessible from other devices**, the firewall may be blocking port 9000:

```bash
sudo ufw allow 9000/tcp   # if ufw is active
sudo ufw allow 9090/tcp   # CLI port (used by Squeezer)
sudo ufw allow 3483/tcp   # player discovery
sudo ufw allow 3483/udp   # player discovery
```

**First-time setup in web UI:**
1. Open http://<openclaw-box-ip>:9000
2. Follow the setup wizard
3. Skip music library scan for now (we're using TuneIn streaming, not local files)
4. Finish wizard

---

## Part 3: Set Up Pi5

**Physical setup:**
1. Insert flashed SD card into Pi5
2. Connect Pi5 HDMI output → CORSAHD extractor HDMI input
3. Connect CORSAHD HDMI output → Sony Bravia HDMI input
4. Connect CORSAHD optical/SPDIF output → ONN Ultra optical input
5. Power on Pi5
6. Wait 1-2 minutes for first boot

**Find Pi5 on the network:**

From openclaw-box:
```bash
# Option 1: mDNS (if avahi is working)
ping pi5-music.local

# Option 2: scan the network
# Replace 192.168.x.0 with your actual subnet
nmap -sn 192.168.1.0/24 | grep -i pi

# Option 3: check your router's DHCP client list
```

**SSH into Pi5:**

```bash
ssh david@pi5-music.local
# or
ssh david@<pi5-ip-address>
```

---

## Part 4: Install Squeezelite on Pi5

**Run on the Pi5 (via SSH):**

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Squeezelite
sudo apt install -y squeezelite

# Verify it installed
squeezelite -?
```

**Configure Squeezelite to use HDMI output:**

```bash
# List audio devices
squeezelite -l
```

Look for the HDMI output device. It will be something like `sysdefault:CARD=vc4hdmi0` or similar.

```bash
# Edit the Squeezelite config
sudo nano /etc/default/squeezelite
```

Set these values:
```
SL_SOUNDCARD="sysdefault:CARD=vc4hdmi0"
SB_PLAYER_NAME="Pi5-Music"
SB_SERVER_IP="<openclaw-box-ip>"
```

**If the HDMI device name is different** from what `squeezelite -l` shows, use the exact name from that output.

**Restart Squeezelite:**

```bash
sudo systemctl restart squeezelite
sudo systemctl enable squeezelite   # start on boot
```

**Force HDMI audio output (if needed):**

```bash
# Edit Pi5 boot config
sudo nano /boot/firmware/config.txt

# Ensure this line exists (uncomment if needed):
dtoverlay=vc4-kms-v3d

# Force HDMI audio
sudo raspi-config
# → System Options → Audio → HDMI
```

Reboot:
```bash
sudo reboot
```

---

## Part 5: Verify Pi5 Shows Up in LMS

1. Open LMS web UI: http://<openclaw-box-ip>:9000
2. Look in the bottom-right for player selection
3. **Pi5-Music** should appear as a player
4. If it doesn't:
   - Check Squeezelite is running on Pi5: `sudo systemctl status squeezelite`
   - Check Pi5 can reach LMS: `ping <openclaw-box-ip>` from Pi5
   - Check LMS discovery ports are open (3483 tcp+udp)

---

## Part 6: Configure TuneIn in LMS

1. In LMS web UI → **Settings** (bottom-right gear icon)
2. Go to **Plugins** tab
3. Find **TuneIn Radio** — it should be installed by default
4. If not installed: check "Active Plugins" list, enable it, restart LMS
5. Once active: go to **My Apps** or **Radio** in the main UI
6. **TuneIn** should appear as a source
7. Browse or search for stations

---

## Part 7: Install Squeezer on Android

1. Install from Google Play: search "Squeezer" by Kurt Bonne
2. Open Squeezer
3. Settings → Server: enter `<openclaw-box-ip>:9090`
4. Squeezer should discover the LMS server and show **Pi5-Music** as a player
5. Browse to TuneIn → select a station → play

---

## Part 8: Test End-to-End

| Step | Expected Result |
|------|----------------|
| Open Squeezer on Android | Connects to LMS, shows Pi5-Music player |
| Browse to TuneIn → pick a station | Station appears in Now Playing |
| Hit Play | Audio plays through ONN Ultra speakers |
| Adjust volume in Squeezer | Volume changes on ONN Ultra |
| Switch ONN Ultra input to TV (Sony Bravia) | TV audio works normally |
| Switch back to optical/extractor input | Music resumes from Pi5 |

---

## Restart / Recovery

**LMS (on openclaw-box):**
```bash
sudo systemctl restart lyrionmusicserver
sudo systemctl status lyrionmusicserver
# Web UI: http://localhost:9000
```

**Squeezelite (on Pi5):**
```bash
sudo systemctl restart squeezelite
sudo systemctl status squeezelite
# Logs: journalctl -u squeezelite -f
```

**If Pi5 loses connection to LMS:**
1. Check WiFi: `iwconfig` on Pi5
2. Check LMS is running on openclaw-box
3. Restart Squeezelite: `sudo systemctl restart squeezelite`

**If no audio from ONN Ultra:**
1. Check CORSAHD extractor input selection
2. Check ONN Ultra is on correct input (optical or HDMI)
3. Check Pi5 audio output: `aplay -l` (should show HDMI device)
4. Test audio directly: `speaker-test -D sysdefault:CARD=vc4hdmi0 -c 2`

---

## Issues Log

_(Record any issues encountered during setup here)_

---

## Notes

- Pi5 is also planned for future voice interaction with Aaron (OpenClaw node). Full Pi OS supports this.
- LMS was rebranded to "Lyrion Music Server" — same software, same community, new name.
- LMS version installed: 9.1.0 (February 2026)
- No Docker, no extra services. Simple systemd services on both boxes.
- Music is David's domain — no cron jobs, no automation. Manual control via Squeezer only.
