
<p align="center">
<img src="https://github.com/user-attachments/assets/9506f946-7b21-45fb-8f66-65b4897db5d0", width="400", height="400">
</p>

<h1 align="center">Weeping Angel</h1>
<h4 align="center">Weeping Angel - Post-exploitation Framework for linux system</h4>

### DESCRIPTION
Weeping Angel is a post-exploitation and adversary emulation framework designed to aid Red Teams and penetration testers. As a Linux-based tool built for ethical penetration testing and cybersecurity research, Weeping Angel leverages Google Calendar as a stealthy Command and Control (C2) server to manage connections with targets through event-based communication.

The tool injects a polymorphic dropper into regular Python code, ensuring each instance is unique by modifying variables, functions, and signatures to evade detection. This adaptive approach means every build incorporates fresh code changes, making it difficult for security tools to identify patterns. Inspired by APT41 techniques and evasion strategies, Weeping Angel
 provides a robust framework for exploring advanced C2 methodologies in controlled, ethical environments.

<h2 align="center">TOOL BANNER</h2>

<p align="center">
<img src="https://github.com/user-attachments/assets/e2f3e0f8-e51c-4488-b03b-c98dd7349a0c", width="1000", height="1000">
<img src="https://github.com/user-attachments/assets/3a0ac814-50be-4ded-88be-072744b1c8a2", width="1000", height="1000">
<img src="https://github.com/user-attachments/assets/0fb2e86c-7f75-4f23-ba77-86ee4cd8415b", width="1000", height="1000">
</p>

### Key Features:
* **Polymorphic Injection**: Automatically modifies code (e.g., variables and functions) in each build to create unique signatures, making it harder for antivirus tools to detect.

* **Junk Code Injection**: Injects randomized code blocks and redundant logic into payloads during generation, creating unique structural signatures while preserving original functionality to evade static analysis and signature-based detection.

* **Per-Machine Unique Signatures**: Each payload deployed to a victim machine receives a unique ELF binary signature by modifying padding bytes in the executable header, ensuring every instance has a different cryptographic fingerprint.
  
* **Google Calendar C2**: Uses Google Calendar events as a covert channel for backdoor communication, allowing remote command execution on Linux targets.
  
* **Dropper Builder**: Injects a custom dropper into any legitimate Python script, transforming it into a backdoor payload.
  
* **Linux Backdoor Deployment**: Focuses on Linux systems, with features for persistent execution and event-based polling.
  
* **Signature Evasion**: Changes ELF file signatures on-the-fly during deployment, making hash-based detection ineffective across different infected machines.
  
* **Customizable Beacon Interval**: Features configurable, randomized check-in intervals (with adjustable minimum and maximum in seconds) to disrupt predictable timing patterns and make detection by network monitoring systems more difficult.
  
* **File & Payload Management**: Commands to download files from the C2 server to the victim machine and update payloads in memory.
  
* **Dynamic Script Execution**: Execute arbitrary Python scripts delivered from the attacker's C2 on the victim machine.

* **Extensible Payload Framework**: Load custom Python exploit modules from a community-driven repository or local library. Users can create, import, and execute third-party payloads (e.g., privilege escalation, data exfiltration, persistence mechanisms) on target machines without modifying the core backdoor code. Supports hot-swappable modules via the C2 channel.

* **Comprehensive Data Exfiltration Suite**:
     - dump_browser: Extracts browser data including saved passwords, cookies, and browsing history.
     - dump_token: Extracts Discord, Chrome, and other application authentication tokens.
     - dump_camera <count>: Takes 1-20 photos using the victim's webcam.
     - dump_audio <duration>: Records audio from the microphone for 1-60 seconds.
     - dump_wifi: Extracts saved WiFi credentials (SSIDs and passwords).
     - dump_history: Extracts command history from terminal shells (Bash, Zsh, Fish).
     - keylog <start|stop|dump|status>: Full control of a keystroke logger.

* **Google Drive Data Exfiltration**:
     - **Structured folder hierarchy** for different data types
     - **Automatic file organization** by victim machine ID
     - **Timestamped filenames** for forensic tracking
     - **Covert channel** blending with legitimate Google Drive traffic


### SETUP
Setup (Google Calendar C2)

Follow the steps below to configure your Google Cloud project and enable Google Calendar API for C2 communication.

Part 1 — Google Cloud Project & Service Account (for Calendar C2)

    Create a new Google Cloud Project

   * Go to: https://console.cloud.google.com
 
 		* From the top bar, click the project dropdown → New Project
 
 		* Project name: rat-calendar-c2
 
 		* Click Create

    Create a Service Account (used by your C2 + implant)

   * Sidebar: IAM & Admin → Service Accounts

   * Click + Create Service Account

   * Name: test-c2

   * Click Create and Continue

   * Role: Owner (or at minimum: Calendar Editor + Drive Editor)

   * Click Continue → Done

    Generate Service Account Key

   * Click your new service account

   * Go to Keys tab → Add Key → Create New Key

   * Select JSON → Create

   * Save file as: c2_creds.json in your C2 directory

    Enable Google Calendar API

   * Go to: https://console.cloud.google.com/apis/library

   * Search: Google Calendar API

   * Select it → Click Enable

Part 2 — Share Calendar with Service Account

   * Visit: https://calendar.google.com

   * On the left, find your calendar → click 3-dot menu → Settings and sharing

   * Scroll to "Share with specific people"

   * Click + Add people

   * Paste your Service Account email

   * Looks like: test-c2@your-project-id.iam.gserviceaccount.com

 		* Set permission to: Make changes and manage sharing
 
 		* Click Send

Part 3 — Google Drive API (for data exfiltration)

   * Enable Google Drive API

   * Go to: https://console.cloud.google.com/apis/library

   * Search: Google Drive API → Enable

    Configure OAuth Consent Screen (required for Drive user auth)

   * Sidebar: APIs & Services → OAuth consent screen

   * User Type: External → Create

   * App name: c2-server

   * User support email: your Gmail

   * Developer contact: your Gmail

   * Click Save and Continue (skip scopes for now)

   * Audience → Add users → enter your Gmail address → Save

   * Click Back to Dashboard

    Create OAuth Client ID (for Drive exfil)

   * Sidebar: APIs & Services → Credentials

   * Click + Create Credentials → OAuth Client ID

   * Application type: Desktop app

   * Name: data exfiltration config

   * Click Create

   * Download the JSON file → rename to data_exfil.json

   * Place it in your Dedsec directory


### Tool Structure:
After completing all steps, your directory should contain:
```code    
DEDSEC_WEEPING_ANGLE/
├── c2_creds.json        # Service account key for Calendar C2
├── data_exfil.json      # OAuth credentials for Drive exfiltration
└── dedsec_weeping_angle     # dedsec tool
```
    
### INSTALLATION
    git clone https://github.com/0xbitx/DEDSEC_WEEPING_ANGLE.git
    cd DEDSEC_WEEPING_ANGLE
    chmod +x dedsec_weeping_angle
    sudo ./dedsec_weeping_angle
    
### TESTED ON FOLLOWING
* Kali Linux 
* Parrot OS 
  
## Legal Disclaimer

This tool is intended for educational and security research purposes only. Unauthorized usage may be illegal in your jurisdiction. The author is not responsible for any misuse of this tool.
