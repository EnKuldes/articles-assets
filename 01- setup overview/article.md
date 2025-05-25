## 🧠 Why I Built This Homelab

This has been one of my personal projects in 2024, but I hadn’t had the time (or motivation) to properly document it — until now. 

The main reason I started this was because I had an old laptop (bought in 2014) that kept crashing. I reinstalled it about 3-4 times last year. Usually, my mom uses it for her work since she uses Excel on that. But now that it’s out of commission, I figured — why not turn it into something fun and useful instead of tossing it? There are several ideas for it, one of which is, of course, to create a gaming device out of it, but after some thought rather than just focusing it as a game center, I thought how about a media server or even my own home lab to dev some app, and here we are. So this is what I'm gonna do for this old laptop, I'm gonna create a media server to store movies, animes, or series using Jellyfin, and also just found out that I can also manage my finance/log my income/outcome using Firefly III (I have been using google spreadsheet since 2019).

## 🧰 Hardware Setup

First, I'm gonna show my specs for Asus X455LA.

- CPU: i3-4030U 1.9Ghz, with 2 Core 4 Threads
- RAM: 6GB DDR3L 1333/1600 (2GB+4GB)
- GPU: Intel HD Graphics 4400 Mobile 2GB VRAM
- 2x USB 2.0
- 1x USB 3.0
- 1x Lan Port (RJ45)
- WiFi 802.11 b/g/n 
- HDD 500GB (Upgradeable with SSD Sata 2.5")
- HDD 500GB (connected using HDD caddy, replacing my DVD RW slot)
- 1 HDD External using USB port (USB 3.0 1TB)
- Integrated Speaker+Microphone
- 1x HDMI Port
- 1x VGA Port
- 1x Audio Jack
- Card Reader (SD Card)
- 1 slot of PCIE 4x1 and 1 slot of 2x4.

This server will be using **Ubuntu Server 24.04** as the main OS, while **docker** will be used to deploy the applications. There might be some apps that are unable to run with docker and are being installed on the OS itself. 

## 🧩 Services & Applications


| Category       | App(s)                                 | Purpose                                          |
| -------------- | -------------------------------------- | ------------------------------------------------ |
| Media Server   | `Jellyfin`                           | Store and stream movies, anime, and series       |
| Finance        | `Firefly III` + `Firefly Importer` | Manage income/expenses, import from spreadsheets |
| Download Tools | `JDownloader 2`, `qBitTorrent`     | Download manager and torrent client              |
| Dashboard      | `Homarr`, `Dashdot`                | Centralized service dashboard                    |
| SQL Tools      | `CloudBeaver`/`DBeaver`            | Web-based SQL management                         |
| File Sharing   | `Samba`                              | Share files with Windows devices                 |
| Development    | `Git`                                | Version control for personal projects            |
| Admin Tools    | `Webmin`                             | Web-based system administration                  |
| Emulation      | `RomM`, `EmulatorJS`               | ROM manager with embedded emulator               |
| Media Requests | `Jellyseer`                          | Handle media requests for Jellyfin               |

> ⚠️ Note: Some plugins or services are more niche or personal. I might cover them in future posts if there's interest.

Each app listed above deserves its own deep dive, so I'm gonna break it down:

- Media Server Setup using **Jellyfin**+**Jellyseer** & Download tools
- Self Host Finance app using **Firefly III**
- My own SQL playground using **Cloudbeaver**.
- Self-host game ROM Library using **RomM**+**EmulatorJS**
- Web Development using **PHP** framework **Laravel** using **Caddy** and **FrankenPHP**

## 📸 Visual Overview

### My Homarr Dashboard

![Homarr screenshot](https://raw.githubusercontent.com/EnKuldes/articles-assets/refs/heads/master/01-%20setup%20overview/Homarr%20Dashboard.png)

### Topology Logic

![Topology Logic](https://raw.githubusercontent.com/EnKuldes/articles-assets/refs/heads/master/01-%20setup%20overview/Homelab%20Topology-Logic%20Topology.drawio.png)

## 💬 What's Next?

In upcoming posts, I’ll dive deeper into each part of this setup. If there’s any app or setup you want me to write about first, let me know in the comments, or connect with me on [LinkedIn](https://www.linkedin.com/in/fahm13/)!

Thanks for reading!
