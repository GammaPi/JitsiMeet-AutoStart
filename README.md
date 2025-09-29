# JitsiMeet-AutoStart

**JitsiMeet-AutoStart** is a lightweight, single-page utility for **unattended systems** that need to automatically join a Jitsi meeting with the camera enabled. Perfect for kiosks, monitoring setups, or any scenario where a system should automatically connect and display video without user interaction.

<img width="1110" height="748" alt="image" src="https://github.com/user-attachments/assets/5598aa55-442e-4198-ac44-99bebac4658a" />


## Features

1. **Automatic Meeting Join**
   * Immediately joins the configured Jitsi room.
   * Microphone starts muted.
   * Video will be enabled if a camera exists and there are more than one participants. (Camera indicator light becomes an indicator of someone is in the meeting room,)
   * Hides room name.

2. **Persistent Configuration**
   The browser remembers the **server URL** and **room ID** using persistent storage. Once set, the system will rejoin the same meeting automatically after reboots or reloads.

3. **Auto-Reconnect**
   If the Jitsi instance goes offline, the page periodically checks availability and automatically refreshes to rejoin when the server comes back online.

4. **No Deployment Required**
   Works as a single HTML file—just open it in a browser on the unattended system and it runs.

---

## Typical Use Cases

* **Conference room kiosks** — screens that should always display a specific meeting.
* **Remote monitoring setups** — unattended systems automatically show video when powered on.
* **Event streaming booths** — auto-connect camera feeds without operator intervention.

---

## Server Reachability Check

When "Offline Reload" is checked the script automatically reloads the webpage if your Jitsi server is offline.

To achieve this, the script will ping the following path:

```
https://<server_url>/ping
```

Since many Jitsi instances block CORS by default, you **must** configure a `/ping` endpoint that is publicly accessible and disable CORS for this path.

### Example Nginx Configuration

```nginx
location = /ping {
    add_header 'Access-Control-Allow-Origin' '*';
    proxy_pass http://<LOCAL_JITSI_URL>/base.html;
}
```

This lightweight endpoint allows the script to detect server availability and handle automatic reconnects reliably.

---

## Quick Start

1. **Download** the HTML file.
2. **Open it in a browser** on your unattended system.
3. **Enter your server URL and room ID** in the interface.
4. The system will now:

   * Auto-join the meeting
   * Enable the camera (mic muted)
   * Reconnect automatically if the server goes down

---


## Credit

I (proudly?!) generated this project by instructing ChatGPT.
