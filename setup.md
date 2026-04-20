
## Setup (Google Calendar C2)

### Follow the steps below to configure your Google Cloud project and enable Google Calendar API for C2 communication.

## Part 1 — Google Cloud Project & Service Account (for Calendar C2)

### Create a new Google Cloud Project

   * Go to: https://console.cloud.google.com

<img width="1810" height="942" alt="Screenshot_20260419_220749" src="https://github.com/user-attachments/assets/0144f591-6fd0-4006-822f-c1fd5ec5427e" />

<img width="1809" height="1266" alt="Screenshot_20260419_220814" src="https://github.com/user-attachments/assets/865fda92-96cc-4bae-8d34-847a0de95546" />

   * From the top bar, click the project dropdown → New Project
     
<img width="753" height="517" alt="Screenshot_20260418_234008" src="https://github.com/user-attachments/assets/bc60130b-e2b0-4cb7-8a50-6b60ca1dafb5" />

   * Project name: rat-calendar-c2
   * Click Create

### Create a Service Account (used by your C2)

<img width="1427" height="949" alt="Screenshot_20260418_234437" src="https://github.com/user-attachments/assets/70ef143a-ef6a-4084-80fa-28e52c46f33a" />

   * Sidebar: IAM & Admin → Service Accounts
   * Click + Create Service Account

<img width="1425" height="877" alt="Screenshot_20260418_234602" src="https://github.com/user-attachments/assets/b201cb20-97c4-43f9-9095-c48a930b6107" />

   * Name: c2-server
   * Click Create and Continue

<img width="1424" height="875" alt="Screenshot_20260418_234722" src="https://github.com/user-attachments/assets/67faff30-f9a3-4948-a2c3-bc3139ae2aa9" />
<img width="1425" height="819" alt="Screenshot_20260418_234930" src="https://github.com/user-attachments/assets/4888c67b-143d-4da8-885c-4f95906b18fa" />

   * Role: Owner 
   * Click Continue → Done

### Generate Service Account Key

<img width="1427" height="885" alt="Screenshot_20260418_235009" src="https://github.com/user-attachments/assets/17e8489f-2be4-4f1d-9647-78d0cf369461" />

   * Click your new service account

     <img width="1423" height="872" alt="Screenshot_20260418_235036" src="https://github.com/user-attachments/assets/23e9a05a-54ce-4af3-a853-3af4cd69ac4d" />
     <img width="1421" height="877" alt="Screenshot_20260418_235107" src="https://github.com/user-attachments/assets/c2fde17f-4f1b-49eb-963d-e773251c8e8a" />
     
   * Go to Keys tab → Add Key → Create New Key

<img width="1421" height="877" alt="Screenshot_20260418_235127" src="https://github.com/user-attachments/assets/5186fb04-5775-44e9-9d38-1a00fb1074c2" />

   * Select JSON → Create

<img width="1419" height="903" alt="Screenshot_20260418_235150" src="https://github.com/user-attachments/assets/12550d7a-7d3b-4921-bad4-73ad69fd0d61" />

   * Save file as: c2_creds.json in your C2 directory

### Enable Google Calendar API

   * Go to: https://console.cloud.google.com/apis/library
     
<img width="1423" height="592" alt="Screenshot_20260419_000729" src="https://github.com/user-attachments/assets/7fff30da-d678-4743-8ffb-36c17d620e2f" />

   * Search: Google Calendar API

<img width="1423" height="592" alt="Screenshot_20260419_000756" src="https://github.com/user-attachments/assets/a0b6c88a-b3da-49b4-bb49-89467d73aabe" />

   * Select it → Click Enable

## Part 2 — Share Calendar with Service Account

   * Visit: https://calendar.google.com

     <img width="1427" height="1059" alt="Screenshot_20260418_235416" src="https://github.com/user-attachments/assets/9622b862-465d-4c06-8fa8-0e047635475c" />

   * On the left, find your calendar → click 3-dot menu → Settings and sharing

<img width="1372" height="838" alt="Screenshot_20260419_215802" src="https://github.com/user-attachments/assets/78362a84-e1c7-46d1-a0b7-6df3447bac91" />

   * Click + Add people and groups
 

<img width="1382" height="949" alt="Screenshot_20260419_215332" src="https://github.com/user-attachments/assets/b04f6e47-1e44-4aa2-be77-3978f938f618" />
  
   * Paste your Service Account email
   * Looks like: test-c2@your-project-id.iam.gserviceaccount.com
   * Set permission to: Make changes and manage sharing
   * Click Send

## Part 3 — Google Drive API (for data exfiltration)

## Enable Google Drive API

   * Go to: https://console.cloud.google.com/apis/library
     
<img width="1419" height="871" alt="Screenshot_20260418_235931" src="https://github.com/user-attachments/assets/f86058bf-1807-4de8-a78b-53db49224bb0" />
<img width="1421" height="657" alt="Screenshot_20260419_000001" src="https://github.com/user-attachments/assets/9b2fb074-9d70-43ae-acb9-0288e2f7ffad" />

   * Search: Google Drive API → Enable

### Configure OAuth Consent Screen (required for Drive user auth)

<img width="1409" height="987" alt="Screenshot_20260419_001648" src="https://github.com/user-attachments/assets/bf6cce6f-7199-47e1-b8e2-a7f2d4031db5" />

   * Sidebar: APIs & Services → OAuth consent screen

<img width="1409" height="987" alt="Screenshot_20260419_001722" src="https://github.com/user-attachments/assets/ce394542-377e-4d53-9568-79e6daaff1b2" />

   * click: Get started
     
 <img width="1425" height="733" alt="Screenshot_20260419_001856" src="https://github.com/user-attachments/assets/b0c61445-354d-48a3-8db0-1178ea385e1b" />
 
   * App name: c2-server
   * User support email: your Gmail -> Next

<img width="1421" height="875" alt="Screenshot_20260419_002002" src="https://github.com/user-attachments/assets/8cd6b2b8-524c-4274-ab48-6820361ba03b" />

   * Audience: External -> Next

<img width="1423" height="672" alt="Screenshot_20260419_002055" src="https://github.com/user-attachments/assets/4cde39b7-cd52-49c8-8a8c-c5355955acf7" />

   * Contact Info: your Gmail -> Next

<img width="1427" height="1059" alt="Screenshot_20260419_002226" src="https://github.com/user-attachments/assets/f820285d-65cd-48a4-980f-b4c9d1aec1ef" />

   * Audience → Add users → enter your Gmail address → Save
   * Click Back to Dashboard

### Create OAuth Client ID (for Drive exfil)

<img width="1421" height="443" alt="Screenshot_20260419_002406" src="https://github.com/user-attachments/assets/e24dd8ab-5b24-46f6-b578-a81ee7491371" />

   * Sidebar: APIs & Services → Credentials
   * Click + Create Credentials → OAuth Client ID
     
<img width="1425" height="475" alt="Screenshot_20260419_002504" src="https://github.com/user-attachments/assets/a983564b-094c-46a8-b6e0-2c46313323c9" />

   * Application type: Desktop app
   * Name: data exfiltration config
   * Click Create

<img width="1425" height="1025" alt="Screenshot_20260419_002525" src="https://github.com/user-attachments/assets/9e17cb34-6c2b-4427-b2b0-ef42920e52d1" />
     
   * Download the JSON file → rename to data_exfil.json
   * Place it in your Dedsec directory
