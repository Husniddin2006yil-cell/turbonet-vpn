const express = require("express");
const bodyParser = require("body-parser");
const TelegramBot = require("node-telegram-bot-api");

const token = "TOKENNI_BU_YERGA";
const bot = new TelegramBot(token);
bot.setWebHook(`${process.env.VERCEL_URL}/bot${token}`); // webhook URL

const app = express();
app.use(bodyParser.json());

app.post(`/bot${token}`, (req, res) => {
  bot.processUpdate(req.body);
  res.sendStatus(200);
});

// Misol /start
bot.onText(/\/start/, (msg) => {
  bot.sendMessage(msg.chat.id, "🚀 VPN bot Vercelda ishlayapti!");
});

app.listen(3000, () => console.log("Server ishlayapti"));
