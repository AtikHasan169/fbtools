# 🤖 AutoReg Automation Bot

A robust, multi-threaded automation tool designed for seamless, high-volume account registration. Built with Selenium, this bot features smart OTP handling, proxy rotation, human-like interaction simulations, and full cross-platform support (Windows, macOS, Linux, and Android via Termux).

---

## ✨ Features

* **Multi-Threaded Workers:** Run multiple browser instances concurrently to process numbers and tasks faster.
* **Smart OTP Watchtower:** Asynchronous background processing automatically fetches and submits OTPs via API, or parks profiles for manual entry/delayed SMS recovery.
* **Termux Auto-Installer:** Android users simply run the script—the bot automatically requests storage permissions, fixes system library links, and installs all required dependencies (`tur-repo`, `chromium`, etc.).
* **Advanced Proxy Support:** Supports static proxies and zone-based rotating proxies, injecting them directly via generated Chrome extensions.
* **Human Emulation:** Configurable typing delays, randomized user-agents, and dynamic DOM interaction to avoid bot detection.
* **Data Management:** Automatically sorts successful registrations into an Excel file (`success_*.xlsx`) and logs parked or failed numbers into text files for easy recovery.
* **Cross-Platform:** Code is obfuscated and compiled for Windows, Mac, Linux, and Android CPU architectures.

---

## ⚠️ Important Prerequisite: Python Version

Because this bot is securely compiled using PyArmor, **it is strictly locked to Python 3.13.x**. 

* **Desktop Users (Windows/Mac/Linux):** You MUST have Python 3.13 installed on your machine. If you use Python 3.12 or 3.14, the bot will not run. You also need Google Chrome installed on your PC.
* **Android Users (Termux):** Termux currently defaults to Python 3.13, so you are good to go! Just make sure to run the initial setup commands below.

---

## 📂 How It Works: Input Files

The bot dynamically reads your target data from text files located in the same folder as the script. Before running the bot, set up your data here:

* **`phones.txt`** *(Required)*: A list of phone numbers to process. Put one number per line. The bot reads from this queue, processes the number, and automatically rescues it back to the file if the task fails or is interrupted.
* **`names.txt`** *(Optional)*: A list of full names (e.g., "John Doe") used for profile creation. The bot will randomly select from this pool.
* **`proxies.txt`** *(Optional)*: Your proxy network list. Format each line exactly as `host:port@username:password`. The bot will route its browsers through these IPs.
* **`countries.txt`** *(Optional)*: If you are using zone-based proxies that require a `{cc}` tag, list the 2-letter country codes here (e.g., `US`, `UK`, `BD`). The bot will automatically swap them in and rotate zones.

---

## 🚀 Installation & Usage

Setting up the bot is incredibly simple. The script includes a built-in auto-installer that handles almost everything, but brand new Termux users need to grab a few basic tools first.

### 1. Initial Setup (Termux / Android Users Only)
If this is your first time using Termux, update your system and install Python and Git before continuing:
```bash
pkg update -y && pkg upgrade -y
pkg install python -y
pkg install git -y
```

### 2. Clone the Repository
Open your terminal or command prompt and run:
```bash
git clone https://github.com/AtikHasan169/fbtools.git
cd fbtools
```

### 3. Prepare Your Data
Make sure you have added your target phone numbers to `phones.txt`. You can also configure `names.txt`, `proxies.txt`, and `countries.txt` as needed before launching the bot.

### 4. Run the Bot (Auto-Installation)
The bot features a built-in setup script. Simply run the main Python file:

```bash
python main.py
```

**What happens next?**
* **Termux (Android):** A popup will ask for storage permissions (click 'ALLOW'). The bot will then automatically fix Python library links, install `tur-repo` and `chromium`, and use `pip` to download required Python packages (`selenium`, `openpyxl`, `aiohttp`).
* **Windows/Mac/Linux:** The script will automatically verify your environment and use `pip` to install the required Python packages.

Once the initial setup is complete, the bot will automatically restart itself.

### 5. Configuration & Dashboard
Upon successful launch, the bot will display a dashboard with your current configuration. 
* Press **[ENTER]** to quickly start the bot using your saved settings.
* Type **`e`** to open the interactive configuration menu where you can adjust:
    * **Display Mode:** Headless (Hidden), Visible, or Minimized
    * **Human Delays:** Enable or disable realistic typing speeds
    * **Proxy Network:** Toggle proxies on or off
    * **Active Workers:** Set the number of concurrent browser instances
    * **Execution Style:** Continuous Loop, Standalone Tasks, or OTP Recovery Only
    * **API Auto-Fetch:** Select Watchtower auto-fetch, Manual 3-minute wait, or Instant Park
