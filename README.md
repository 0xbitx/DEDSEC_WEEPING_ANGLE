
<p align="center">
<img src="https://github.com/user-attachments/assets/9506f946-7b21-45fb-8f66-65b4897db5d0", width="400", height="400">
</p>

<h1 align="center">Weeping Angel</h1>
<h4 align="center">Weeping Angel - Post-exploitation Framework for linux system</h4>

### DESCRIPTION
Weeping Angel is a post-exploitation and adversary emulation framework designed to aid Red Teams and penetration testers. As a Linux-based tool built for ethical penetration testing and cybersecurity research, Weeping Angel leverages Google Calendar as a stealthy Command and Control (C2) server to manage connections with targets through event-based communication.

The tool injects a polymorphic dropper into regular Python code, ensuring each instance is unique by modifying variables, functions, and signatures to evade detection. This adaptive approach means every build incorporates fresh code changes, making it difficult for security tools to identify patterns. Inspired by APT41 techniques and evasion strategies, Weeping Angel
 provides a robust framework for exploring advanced C2 methodologies in controlled, ethical environments.

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

1. Create a Google Cloud Project and Service Account

    Go to: https://console.cloud.google.com

    From the sidebar, go to IAM & Admin → Service Accounts

    Click + Create Project
     * Project name: (e.g.,) rat-calendar-c2
     * Click Create

    Click + Create Service Account
     * Service account name: e.g. test-c2
     * Description: (optional)
     * Click Create and Continue

    Grant this service account access:
      * Role: Owner
      * Click Continue → Done

    Click your newly created service account
      * Go to the Keys tab
      * Click Add Key → Create New Key
      * Select JSON, then click Create
      * Save the file as: c2_creds.json in your directory

3. Share Google Calendar with Service Account

    Visit: https://calendar.google.com

    On the left, click the 3-dot menu beside your calendar → Settings and sharing

    Scroll to Share with specific people
     * Click + Add people and groups
     * Paste your Service Account email
     * Example: test-c2@your-project-id.iam.gserviceaccount.com
     * Set permission to: Make changes and manage sharing
     * Click Send

5. Enable Google Calendar API

     * Go to: https://console.cloud.google.com/apis/library
     * Search for: Google Calendar API
     * Click it → Click Enable
     
6. Enable Google Drive API

  	* Go to: https://console.cloud.google.com/apis/library
    * Search for: Google Drive API
    * Click it → Click Enable
    * Go to "Credentials" and Click ( + Create credentials) and select (OAuth client ID).
  		- select: Desktop app
  		- name: data exfiltration config
  
    * Download the credentials.json file and place it in Dedsec directory as data_exfil.json
     * APIs & Services → OAuth consent screen → Audience → Add users
     * type your email address and save

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
