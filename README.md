<!-- README.md(EN)와 README.ko.md(KO)는 함께 고친다 -->
**English** | [한국어](README.ko.md)

# LifeOS

A personal tracking app that gathers to-dos, a calendar, a timetable, habits, goals, projects, money management, meal plans and a fridge, a wardrobe, health and exercise, study, research notes, and reading and movie logs in one app.

- There is no sign-up. Your records are stored only on the device where you install it.
- You use it on an Android phone and an Ubuntu PC. A Windows version is in preparation.
- The screens are in Korean, and dates are counted in Korean time regardless of the device's time zone.

<p align="center"><img src="docs/today-pc.png" alt="Today screen on a PC" width="100%"></p>
<p align="center">
  <img src="docs/today-phone.png" alt="Today screen on a phone" width="32%">
  <img src="docs/money-phone.png" alt="Money management on a phone" width="32%">
  <img src="docs/fridge-phone.png" alt="Meal plan and fridge on a phone" width="32%">
</p>
<p align="center"><sub>The records in the pictures are examples.</sub></p>

## Download

Get the file for your device from [Get the latest version](../../releases/latest).

| Device | File |
| --- | --- |
| Android 8 or later | `LifeOS-public-<version>.apk` |
| Ubuntu 22.04 or later, amd64 (checked on 24.04) | `lifeos-public_<version>_amd64.deb` |
| Windows | In preparation |

The SHA-256 of each file is written in the release description. On a PC you can check that a downloaded file is intact with `sha256sum <file name>`.

## Installing on Android

1. Download the APK in your phone's browser and open it.
2. If a window blocks the installation, tap **Settings**, turn on **Allow from this source** for the app that opened the file (Chrome or My Files), then go back and install.
   - To turn it on beforehand on a Galaxy: Settings › Apps › ⋮ (More) › Special access › Install unknown apps › Chrome (or My Files) › Allow from this source
3. If **Auto Blocker** (the automatic security-risk block) stops you on a Galaxy, temporarily turn off Settings › Security and privacy › Auto Blocker, install, then turn it back on. While this feature is on, you cannot update to a new version either, so turn it off briefly when you update, too.
4. Because the app did not come from the Play Store, Play Protect may show a warning. Read it and decide whether to continue installing.

You can place the **LifeOS 할 일** (TODO), **LifeOS 달력** (calendar) and **LifeOS 예산** (budget; wide, small, one line) widgets on the home screen.

### Permissions the app uses

Android asks separately for the text-message, notification, health and microphone permissions when you use that feature. Even if you do not allow them, the other features work as usual.

| Permission | Where it is used |
| --- | --- |
| Read notifications, read text messages | Money management › Settings › Auto record. It reads payment notifications and payment text messages from card, pay and bank apps and records them as spending. It does not read anything until you turn it on yourself, and what it reads is not sent off the phone. |
| Show notifications | Notifications that let you pick a category when a payment is detected, and budget alerts |
| Read health data (Health Connect) | **Import from Samsung Health** in Health. It only reads steps, sleep, exercise, distance, calories, heart rate, oxygen saturation, weight, body fat and height. |
| Microphone | Recording in Study › OPIc practice |
| Biometric authentication | **Authenticate when opening the app** in Money management › Settings (fingerprint or screen lock) |
| Internet | Weather, exchange rates, stock prices |

If you try to turn on reading notifications and it is blocked as a "restricted setting", tap Settings › Apps › LifeOS › ⋮ › **Allow restricted settings**, then turn it on again. This is a restriction Android puts on apps downloaded from the web.

## Installing on Ubuntu

```sh
sudo apt install ./lifeos-public_<version>_amd64.deb
```

- Open **LifeOS** from the app list. The first time you open it, it creates and starts the user service `lifeos-desktop.service`, which holds your records. This service starts every time you log in.
- Opening <http://127.0.0.1:8787> in a browser on the same PC shows the same records.
- Open the **desktop TODO** by right-clicking the LifeOS icon or from the menu button above the app window. If you turn on **Run the desktop TODO at login** in the same menu, it appears every time you log in.
- Records are stored in `~/.local/share/lifeos`.
- **If you use `~/.todo.txt`, check before installing.** LifeOS also writes your to-dos to this file. If this file exists the first time you open it, LifeOS imports its contents as to-dos and copies the original to `~/.local/share/lifeos/backups/`, and after that it overwrites the file with LifeOS's to-dos.
- The **AI** page needs Codex or Claude Code to be installed and signed in on this PC. When you ask the AI something, your request and the records it needs go to that service (OpenAI, Anthropic). You cannot use the AI on Android.

### Uninstalling

```sh
systemctl --user disable --now lifeos-desktop.service
rm -f ~/.config/systemd/user/lifeos-desktop.service ~/.config/autostart/lifeos-widget.desktop
systemctl --user daemon-reload
sudo apt remove lifeos
```

To delete the records as well, take a JSON backup first, then delete the `~/.local/share/lifeos` folder.

## Records and backups

- There is no sync between devices. The records on your phone and your PC are separate.
- **Backup**: get a records file with Settings/Backup › **JSON backup**. Do it from time to time.
- **Moving and restoring**: in LifeOS on another device, choose that file with Settings/Backup › **Import JSON**, check the contents, then tap **Restore the checked backup**. All the records on that device are replaced with the backup's contents.
- If you uninstall the Android app or clear its app data, the records are erased as well, and they are not kept in a Google backup either. When you change phones, move them with a JSON backup.

## Switching to a new version

- Download the new file from [Releases](../../releases) and install it as you did at first; it installs over the old one and your records stay as they are.
- On Ubuntu, open LifeOS again after installing and it switches to the new version.
- The version you are using appears at the bottom of the menu as `LifeOS <version> 배포판` (distributed edition).

## What leaves your device

LifeOS has no accounts, no ads and no usage statistics. It uses the internet only in the cases below.

| Feature | Sent to | What is sent |
| --- | --- | --- |
| Weather | Open-Meteo | The name you typed when looking up a location; the coordinates of that location when fetching the weather |
| Exchange rates | Frankfurter | The currency |
| Stock prices | Naver Securities | The ticker |
| AI (Ubuntu) | OpenAI (Codex) or Anthropic (Claude Code) | Your request and the records it needs |

## Terms of use

- Anyone can install and use the LifeOS distributed edition for free.
- It is provided as is, and we are not responsible for lost records or other problems that arise from using it. Take a JSON backup of important records.
- Do not modify the files in this repository, re-upload them elsewhere, or sell them. Sharing the link to this page is fine.
- The open-source software inside the app follows each project's own license. The list and full texts are in `THIRD-PARTY-NOTICES.txt` attached to every release.

## Contact

Leave bugs and requests in [Issues](../../issues). Please do not write personal records or payment details.
