# Telegram Bot: Polling vs Webhook Solution

## Il Problema

Quando si sviluppa un bot Telegram, esistono due modi principali per ricevere aggiornamenti:

### Polling
- Il bot richiede continuamente aggiornamenti a Telegram ("Ci sono nuovi messaggi?")
- Consuma più risorse poiché è in costante esecuzione
- Funziona su qualsiasi hosting, anche locale
- Non richiede un URL pubblico
- Più semplice da configurare

### Webhook
- Telegram invia gli aggiornamenti direttamente al bot quando arrivano messaggi
- Più efficiente perché il bot viene attivato solo quando necessario
- **Richiede** un URL pubblico con certificato HTTPS
- Ideale per servizi cloud come Render, Heroku, ecc.
- Richiede una configurazione più complessa

### Il Problema Specifico
Quando si utilizza un servizio di hosting gratuito come Render, il server può andare in "sleep" dopo un periodo di inattività. Con il polling, il bot smette di funzionare quando il server va in sleep mode. Questo è il motivo per cui il webhook è preferibile per deployment su cloud.

## Le Soluzioni

### Soluzione 1: Polling (per esecuzione locale o server sempre attivi)

```python
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes
import random
import os
import logging

# Set up logging
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)
logger = logging.getLogger(__name__)

# Barzellette divise per tema
barzellette = {
    "scuola": [
        "Perché il libro di matematica era triste? Perché aveva troppi problemi.",
        "Maestra: 'Giovannino, coniuga il verbo cadere!'\nGiovannino: 'Io cado, tu scadi, egli scade...'",
    ],
    "animali": [
        "Un cane entra in un bar e dice: 'Avete qualche osso?'. Il barista: 'No, solo cocktail!'",
        "Cosa fa un gatto sul computer? Naviga su Miao-soft.",
    ],
    "carabinieri": [
        "Perché i carabinieri vanno in giro in tre? Uno sa leggere, uno sa scrivere e l'altro controlla gli intellettuali.",
    ],
}

# Comando /start
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "Ciao! Sono il bot delle barzellette. Scrivi /barz <tema> per ricevere una barzelletta!\nTemi disponibili: scuola, animali, carabinieri"
    )

# Comando /barz <tema>
async def barz(update: Update, context: ContextTypes.DEFAULT_TYPE):
    if len(context.args) == 0:
        await update.message.reply_text("Specifica un tema. Esempio: /barz scuola")
        return

    tema = context.args[0].lower()
    if tema in barzellette:
        barz = random.choice(barzellette[tema])
        await update.message.reply_text(barz)
    else:
        await update.message.reply_text("Tema non disponibile. Temi: scuola, animali, carabinieri")

# Entry point
if __name__ == '__main__':
    # Token handling
    TOKEN = os.environ.get('TELEGRAM_BOT_TOKEN', '7517732337:AAFTMh4j2x_6yg6rxrIDKNBSSkDw4wFB_Ow')
    
    app = ApplicationBuilder().token(TOKEN).build()

    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("barz", barz))

    print("Bot avviato in modalità polling...")
    app.run_polling()
