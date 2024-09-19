---
title: "Create a Telegram Bot on Python"
date: 2024-09-19
---
# How to create a Telegram Bot on Python: Step-by-Step guide.
### Table of Contents:
1. [What Is a Telegram Bot?](#1-what-is-a-telegram-bot)
2. [Prerequisites](#2-prerequisites)
3. [Creating a Bot on Telegram](#3-creating-a-bot-on-telegram)
4. [Setting Up Python Environment](#4-setting-up-python-environment)
5. [Writing the Bot Code](#5-writing-the-bot-code)
6. [Deploying the Bot](#6-deploying-the-bot)
7. [Conclusion](#7-conclusion)

---

## 1. What Is a Telegram Bot?

Bots are small applications that run entirely within the Telegram app. Users interact with bots through flexible interfaces that can support any kind of task or service. 

You can read more about bots in official documentation:
[Bots](https://core.telegram.org/bots)
[Telegram Bot API](https://core.telegram.org/bots/api)

---

## 2. Prerequisites

Before diving into bot creation, you'll need the following:

- **A Telegram Account**: You can easily create one by downloading the Telegram app on your phone.
- **Python Installed**: We will use Python 3, so make sure it’s installed on your computer. _[download link](https://www.python.org/downloads/)_
- **Basic Python Knowledge**: Understanding Python syntax and packages will help you navigate the code. I can recommend this book [Automate the Boring Stuff with Python](https://automatetheboringstuff.com/)
- **BotFather Access**: BotFather is a built-in Telegram bot that helps you manage and create new bots.
- **VS Code(Optional)**: I use it for writing my bots. But feel free to choose any other editor. But I'd recommended to use this one.
_[Here](https://code.visualstudio.com/download) you can download the latest version of VS Code, and [here](https://code.visualstudio.com/docs/python/python-tutorial) is instruction on how to set it for Python._

---

## 3. Creating a Bot on Telegram

To create your own bot, you need to use **BotFather**, the official tool for registering and managing bots on Telegram.

### Steps:
1. Open Telegram and search for the **BotFather** bot. (Enter @BotFather into the search menu)
2. Start a chat with BotFather by typing `/start`.
3. Create a new bot by typing `/newbot`.
4. You will be prompted to provide a name for your bot. Enter a unique name (e.g., `Hello World`).
5. BotFather will ask for a username for the bot. The username must end with "bot" (e.g., `HelloWorldBot`).
6. After completing these steps, BotFather will give you a **token**. This token is crucial as it authenticates your bot and allows you to interact with Telegram’s API.

> **Important:** Keep your token private and do not share it publicly!

---

## 4. Setting Up Python Environment

Next, we need to set up our Python environment to interact with the Telegram API. We will use the `python-telegram-bot` library, which provides a simple and easy-to-use interface for developing Telegram bots.

### Steps:
**Install the python-telegram-bot library**:
 Run the following command to install the necessary library:
 ```bash
 pip install python-telegram-bot 
 ```
**Create a new Python file:** You can name it something like my_bot.py to hold your bot's code.

---

## 5. Writing the Bot Code

Now that our environment is ready, let’s write the bot code.

### Sample Code
Here’s a basic bot that responds to /start and /help commands:
```python
import logging
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes

# Enable logging
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
                    level=logging.INFO)
logger = logging.getLogger(__name__)

# Define a start function to respond to the /start command
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    await update.message.reply_text('Hello! I am your bot. How can I help you today?')

# Define a help function to respond to the /help command
async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    await update.message.reply_text('You can use the following commands:\n/start - Start the bot\n/help - Get help')

def main():
    # Create the application and pass the bot token
    application = ApplicationBuilder().token('YOUR_BOT_TOKEN_HERE').build()

    # Add command handlers for /start and /help
    application.add_handler(CommandHandler("start", start))
    application.add_handler(CommandHandler("help", help_command))

    # Start the bot and run it until manually stopped
    application.run_polling(allowed_updates=Update.ALL_TYPES)

if __name__ == '__main__':
    main()
```

### Explanation:
* **Imports:** We import `telegram` and `telegram.ext` modules to build our bot. These provide the classes and functions necessary to interact with the Telegram API.
* **Logging:** Logging is enabled to track events and errors.
* **Start and Help Commands:** We define two functions (`start` and `help_command`) that send a message when users trigger the corresponding commands.
* **Token:** Replace `'YOUR_BOT_TOKEN_HERE'` with the token you received from BotFather.
* **Polling:** The bot uses polling to constantly check for new messages and responds to them as they come.

### Running the Bot:
 1. Replace the placeholder token in the code with your bot’s token.
 2. Run your Python script:
 ```bash
 python my_bot.py
 ```
Your bot is now up and running! Open Telegram, send the `/start` or `/help` commands to the bot, and it will respond.

---

## 6. Deploying the Bot

Running the bot on your local machine is great for testing, but what if you want it to be available 24/7? To achieve this, you can deploy the bot to a server or cloud service.

### Common Deployment Options:
* **Heroku:** A free cloud platform where you can host your bot.
* **AWS (Amazon Web Services):** More scalable but may require some setup for beginners.
* **VPS (Virtual Private Server):** Gives you full control over your server.
* **PythonAnywhere:** A beginner-friendly option with free tiers.
Each platform offers unique ways to deploy Python applications. You can follow deployment tutorials specific to your chosen service.

---

## 7. Conclusion
Congratulations! You’ve successfully created a basic Telegram bot using Python. You learned how to:

* Set up a Telegram bot using BotFather.
* Write Python code to handle commands.
* Run the bot locally and interact with it on Telegram.

---

Next, I'd recommend you to learn the [example bots](https://docs.python-telegram-bot.org/en/stable/examples.html) from `python-telegram-bot` 

---
This is a series of articles. In next articles, I'll explain how to host you bot on **PythonAnywhere**, how to host bots on your own **Raspberry PI** server, and how to create more complicated bots.
