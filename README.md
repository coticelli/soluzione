# Telegram Bot Project

A feature-rich Telegram bot built with Python that provides various utilities including time checking, weather forecasts, random facts, and interactive menus.

![Telegram Bot](https://img.shields.io/badge/Telegram-Bot-blue?logo=telegram)
![Python](https://img.shields.io/badge/Python-3.10-green?logo=python)

## Features

- 👋 Welcome message and helpful onboarding
- 📚 Help command with available instructions
- ⏰ Current time display
- 🌤️ Simulated weather forecasts
- 🧠 Random interesting facts
- 🎮 Interactive menu with buttons
- 📸 Photo recognition responses
- 🔄 Message echo functionality
- ⚠️ Error handling

## Prerequisites

- Python 3.7 or newer
- A Telegram account
- A Telegram bot token from BotFather

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/telegram-bot.git
   cd telegram-bot
   ```

2. Create a virtual environment (recommended):
   ```
   python -m virtualenv bot_env
   ```

3. Activate the virtual environment:
   - Windows:
     ```
     .\bot_env\Scripts\activate
     ```
   - macOS/Linux:
     ```
     source bot_env/bin/activate
     ```

4. Install dependencies:
   ```
   pip install python-telegram-bot
   ```

## Configuration

1. Get a bot token from [BotFather](https://t.me/botfather):
   - Open Telegram and search for `@BotFather`
   - Start a chat and send `/newbot`
   - Follow the instructions to create your bot
   - Copy the API token provided

2. Open `bot.py` and replace the token placeholder with your token:
   ```python
   app = ApplicationBuilder().token('YOUR_BOT_TOKEN').build()
   ```

## Usage

1. Run the bot:
   ```
   python bot.py
   ```

2. Open Telegram, search for your bot by username, and start interacting!

3. To stop the bot, press `Ctrl+C` in your terminal.

## Bot Commands

| Command | Description |
|---------|-------------|
| /start | Start the bot and get a welcome message |
| /help | Display all available commands and information |
| /time | Show the current date and time in UTC |
| /weather | Get a simulated weather forecast |
| /fact | Learn a random interesting fact |
| /menu | Display an interactive menu with buttons |

## Interactive Features

The bot includes interactive buttons through Telegram's inline keyboard functionality. Users can click buttons in the `/menu` command to:
- Check the current time
- Get weather information
- Learn a random fact

## Deployment Options

For 24/7 operation, consider deploying your bot to one of these platforms:

### PythonAnywhere
1. Sign up at [PythonAnywhere](https://www.pythonanywhere.com/)
2. Upload your code and configure a scheduled task

### Heroku
1. Create a `Procfile` with:
   ```
   worker: python bot.py
   ```
2. Create a `requirements.txt` file:
   ```
   python-telegram-bot
   ```
3. Deploy to Heroku following their [documentation](https://devcenter.heroku.com/articles/getting-started-with-python)

### Replit
1. Create a new Repl with your code
2. Use the "Always On" feature to keep your bot running

## Extending the Bot

You can easily extend the bot by:

1. Adding new command handlers:
   ```python
   async def new_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
       await update.message.reply_text("This is a new command!")

   app.add_handler(CommandHandler("newcommand", new_command))
   ```

2. Adding more interactive buttons:
   ```python
   keyboard.append([InlineKeyboardButton("New Button", callback_data='new_action')])
   ```

3. Connecting to external APIs for real data

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) library
- Telegram for their Bot API

---

Made with ❤️ by [Fabio Coticelli]# soluzione
soluzione a "Perché il bot non funziona più?"
