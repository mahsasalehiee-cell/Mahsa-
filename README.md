# Mahsa-import logging
import time
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, ContextTypes, filters

# لاگ برای خطاها
logging.basicConfig(
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
    level=logging.INFO
)

TOKEN = "8317900445:AAE38wTCDLiG72XiWGJBOCjj8zrPD8wfrgQ"

# --- دستورات ---
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text("سلام 👋\nمن ربات گلزارم 😎\nمنو تو گروه اد کن تا حال کنیم!")

# --- جواب‌های فان ---
async def reply_to_messages(update: Update, context: ContextTypes.DEFAULT_TYPE):
    text = update.message.text.lower()

    if "سلام" in text:
        await update.message.reply_text("سلام پاپت 😏")
    elif "خوبی" in text:
        await update.message.reply_text("تو خوبی پاپت؟ 🤨")
    elif "خفه شو" in text:
        await update.message.reply_text("پیش گلزار هیچی نیسی 🤫")
    elif "درد" in text:
        await update.message.reply_text("خجالت بکش 😒")
    elif "گلزار" in text:
        await update.message.reply_text("جونم 😎")
    elif "احمق" in text:
        await update.message.reply_text("من عقده‌ایم کثافت؟ 🤔")
    elif "پاپت" in text:
        await update.message.reply_text("جون 😏")
    elif "مدیرت کیه" in text:
        await update.message.reply_text("مدیر من مهساست 👑")

# --- اجرای بدون توقف ---
def run_bot():
    while True:
        try:
            app = ApplicationBuilder().token(TOKEN).build()

            app.add_handler(CommandHandler("start", start))
            app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, reply_to_messages))

            app.run_polling()
        except Exception as e:
            logging.error(f"خطا پیش اومد: {e}")
            time.sleep(5)  # ۵ ثانیه صبر بعد دوباره استارت

if name == "main":
    run_bot()
