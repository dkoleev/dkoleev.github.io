---
title: "Host Telegram Bot on Raspberry Pi 5 via SSH"
date: 2024-09-24
---

# How to host Telegram Bot on Raspberry Pi 5: Step-by-Step Guide
### Table of Contents:
* [Intruduction](#intruduction)
* [Install OS on Raspberry Pi 5](#install-os-on-raspberry-pi-5)
* [Connect to Raspberry Pi via `SSH`](#connect-to-raspberry-pi-via-ssh)
* [Prepare envariement](#prepare-envariement)
* [Create and Run the Bot](#create-and-run-the-bot)
* [Keep the bot running in the background using `tmux`](#keep-the-bot-running-in-the-background-using-tmux)
* [Automatically Start the Bot on Boot (Optional)](#automatically-start-the-bot-on-boot-optional)

## Intruduction
In my previous article, I demonstrated how to create and run a Telegram Bot using Python. You can find it [here](https://dev.to/dmitry-koleev/create-a-telegram-bot-on-python-44l4)

In this guide, I’ll walk you through hosting your Telegram bot on your own Raspberry Pi server.

## Install OS on Raspberry Pi 5
Follow [this guide](https://www.raspberrypi.com/documentation/computers/getting-started.html#raspberry-pi-imager) to create an image with Raspberry Pi Imager.   
I recommend choosing `Raspberry Pi OS Lite` OS because it is the best option in terms of lightweight simplicity. 

In the imager settings check the box next to **Enable SSH** and select **use password authentification**. This will allow you to connect to your Raspberry Pi via `SSH`.

After creating the image on a USB flash drive, insert the flash card into your Raspberry Pi and power it on.

## Connect to Raspberry Pi via `SSH`
1. Open the console (cmd or PowerShell on Windows)
2. Ping your Raspberry Pi the following command:
```bash
ping raspberrypi.local
```
You’ll receive ping statistics along with the IP address of your Raspberry Pi.
3. Use this IP address to connect via SSH:
```bash
SSH pi@<your_raspberry_pi_ip> (for example: SSH pi@192.168.0.10)
```
4. Enter the password (default is `raspberry`). I strongly recommend changing this later.
5. If the password is correct, you will be connected to your Raspberry Pi via `SSH`.

## Prepare Envariement
1. Update your Raspberry Pi
```bash
sudo apt update
sudo apt upgrade
```
2. Install Python
Raspberry Pi OS usually comes with `Python` pre-installed. Check if it's installed:
```bash
python3 --version
```
If `Python` is not installed, you can install it using:
```bash
sudo apt install python3 python3-pip
```
3. Set Up a Virtual Environment (Optional but Recommended)
It’s a good practice to create a virtual environment to keep your project dependencies isolated:
```bash
sudo apt install python3-venv
python3 -m venv telegram-bot-env
source telegram-bot-env/bin/activate
```
4. Install the [Python Telegram Bot Library](https://python-telegram-bot.org/)
```bash
pip install python-telegram-bot --upgrade
```

## Create and Run the Bot
1. Create a new `Python` file using the `nano` text editor
```bash
nano bot.py
```
2. Write your bot code in this new file _(you can use code from my [previous article](https://dev.to/dmitry-koleev/create-a-telegram-bot-on-python-44l4)). Press `CTRL + O` then hit `Enter` to save changes. To exit press `CTRL + X`.
3. Run the bot
```bash
python3 bot.py
```
Your bot is now running, and you can test it on Telegram.  

However, this method will terminate the bot when you close the terminal.      

To keep it running in the background we can use [`tmux`](https://github.com/tmux/tmux/wiki)

## Keep the Bot Running in the Background Using `tmux`
### Create an Executable Shell Script to Start Your Bot
1. Install `tmux`
```bash
sudo apt update
sudo apt install tmux
```
2. Create a new shell script to start your bot. You can name it start_bot.sh
```bash
nano start_bot.sh
```
3. Add the following lines to the script, replacing `bot.py` with the name of your Python bot file and `telegram-bots-env` with your env name:
```bash
#!/bin/bash
source telegram-bots-env/bin/activate
python3 bot.py
```
4. Save and exit `(CTRL + O, Enter, CTRL + X)`.
5. Make the script executable:
```bash
chmod +x start_bot.sh
```
### Run Bot via `tmux`:
1. Start a new `tmux` session:
```bash
tmux new -s my_bot_session
```
2. Inside the `tmux` session, run your bot script:
```bash
./start_bot.sh
```
3. Detach from the `tmux` session by pressing `CTRL + B`, then `D`
4. Reattach to the `tmux` Session (if needed)
To reattach to your bot’s `tmux` session later, use:
```bash
tmux attach -t my_bot_session
```
## Automatically Start the Bot on Boot (Optional)
If you want your bot to start automatically on boot, you can use a systemd service. Here’s how:
1. Create a new service file:
```bash
sudo nano /etc/systemd/system/my_bot.service
```
2. Add the following configuration, modifying paths as needed:
```ini
[Unit]
Description=My Bot Service

[Service]
ExecStart=/usr/bin/tmux new-session -d -s my_bot_session '/path/to/start_bot.sh'
WorkingDirectory=/path/to/my_bot
User=pi

[Install]
WantedBy=multi-user.target
```
3. Save and exit the file.
4. Reload the systemd daemon:
```bash
sudo systemctl daemon-reload
```
5. Enable the service to start on boot:
```bash
sudo systemctl enable my_bot.service
```
6. Start the service:
```bash
sudo systemctl start my_bot.service
```

