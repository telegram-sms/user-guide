# User manual

## Welcome

Welcome to use Telegram SMS! You can learn how to build a Telegram SMS bot better from scrach by reading this manual.

## Introduction

Telegram SMS is a Telegram Bot that runs on your Android devices. It requires no third-party relay server but your network must have access to  `api.telegram.org` .

## 1. Startup - Build a Telegram Bot

* Visit [@botfather](https://t.me/botfather), and enter  `/newbot` to get a new bot.

> Telegram SMS requires one bot per phone, so please DO NOT share one bot between different phones, or errors might occur.

* When you see `Alright, a new bot. How are we going to call it? Please choose a name for your bot.` , enter your bot's display name.

* When you see `Good. Now let's choose a username for your bot. It must end in bot. Like this, for example: TetrisBot or tetris_bot.` , enter your bot's Username. Note that the Username of bot must end in `bot`.

* Then you will receive your bot token and URL just as shown below. Please click on the t.me URL to add your bot to your conversation list and start it. You can send several `/start` to start your bot, which helps later.

```
Done! Congratulations on your new bot. You will find it at t.me/<Username of your bot>. You can now add a description, about section and profile picture for your bot, see /help for a list of commands. By the way, when you've finished creating your cool bot, ping our Bot Support if you want a better username for it. Just make sure the bot is fully operational before you do this.

Use this token to access the HTTP API:
xxxxxxxx:xxxxxxxxxxxxxx
Keep your token secure and store it safely, it can be used by anyone to control your bot.

For a description of the Bot API, see this page: https://core.telegram.org/bots/api
```

where  `xxxxxxxx:xxxxxxxxxxxxxx` is the token of your bot.

## 2. Configuration - Let the bot respond properly

> Telegram SMS use Long Polling to listen on the commands, so no Webhook is needed. If your bot set the Webhook before, please visit `https://apt.telegram.org/bot<Your bot token>/setwebhook` to clear the Webhook settings.

* On your phone, enter the Bot Token you just received.

> If you configure your token on the your computer with ADB, you can set the input focus on the column of Bot Token, and enter  `adb shell input text <Your bot token>` in your terminal, which will help you fill in the column. ADB is required for this method.

* Send something arbitrary to the bot. (If you have sent `/start` as said before, you can skip this step.)

* Click `Get recent chat ID`, and select your account.

* Enter a trusted phone number, which will be used for SMS remote control. You can use this phone number to send SMS or restart the background service.

* Select the following options

>* Network error falls back to SMS - Send the messages that fail to send to your trusted phone number.
>* Battery monitoring - When charging status changes or low battery, you will be notified by SMS.
>* Get chat command - Use chat commands to manage your bot (SMS management only if you disable this)
>* Display SIM card alias in dual card mode - Display SIM card alias on the SMS title.

* Click `Test and save` to grant corresponding permissions. The configuration succeeds when you receive the following SMS:

```
[System information]
Connected to the Telegram API Server.
```
### Precautions
* Telegram SMS needs you to ban the adaptive battery. It will help you receive your messages quickly and stably. If you are using a proxy APP, please stop restrict its battery use.

* When you are using OS like MIUI, please close the battery restriction in the settings, and enable starting with the system. When you need to receive Service SMS, please grant the corresponding permissions in the settings.

* The MIUI optimization function in the MIUI OS might kill the APP, so we suggest to close it. (Not verify it yet.)

* If your system cannot receive SMS successfully due to the system restriction, please set this APP as the default SMS APP.

## 3. SMS - Use trusted phones to manage bot

You can set a trusted phone number for automatic forward. The bot will forward the SMS automatically when receiving an SMS from the number. The format is:

```
{Receiver phone number}
{SMS content}
```

Example：

```
+441807391001
example.com
```

It will send `example.com` to the number `+441807391001` by SMS.

You can use the command `restart-service` to restart all the background service.

** If you are roaming, please add your country/region codes before the number(e.g., UK country calling code: +44)

## 4. Commands - Use chat commands to manage bot

You can see the panel by sending `/start` command.

The command format to send an SMS is:

```
/sendsms
{Receiver phone number}
{SMS content}
```
For example,
```
/sendsms
+441807391001
example.com
```

It will send `example.com` to the number `+441807391001` by SMS.

An SMS will be sent by default SIM card when using `/sendsms`. When you are using dual SIM cards, use `/sendsms1` to send SMS from the first SIM card and `/sendsms2` to send SMS from the second SIM card (if SIM2 is avaliable).

You can use the reply function of Telegram to reply the SMS and missed calls quickly. (After clearing logs, you will not be able to reply to any messages received before.)

When calling permission is not granted, you can only send SMS from the default SIM card.
