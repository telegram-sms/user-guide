# 用戶手冊

## 介紹

Telegram SMS 是一個運行在您 Android 設備上的 Telegram Bot，它無需第三方中轉服務器，只要您當前的網絡環境能夠正常訪問 `api.telegram.org` 即可正常使用。它可以通過遠程指令，來方便管理您的簡訊，未接電話以及電量。

## 1、起步 - 建立一個Telegram Bot

* 訪問 [@botfather](https://t.me/botfather)，輸入 `/newbot` 來獲取一個Bot。

> Telegram SMS 採取一台手機一個Bot的原則，故請不要共用一個bot，以免導致錯誤發生。

* 提示`Alright, a new bot. How are we going to call it? Please choose a name for your bot.` ，輸入您Bot的顯示名稱。

* 提示`Good. Now let's choose a username for your bot. It must end in bot. Like this, for example: TetrisBot or tetris_bot.` 輸入您的Bot Username，Username必須用 `bot` 作為結尾

* 然後您會獲取到一個機器人令牌和一個添加鏈接，就像下面這樣。請點擊 t.me 鏈接，將 Bot 加入您的聊天列表並啟動它（可以多發幾次 `/start` ,之後將會用到）。

```
Done! Congratulations on your new bot. You will find it at t.me/<你的機器人用戶名>. You can now add a description, about section and profile picture for your bot, see /help for a list of commands. By the way, when you've finished creating your cool bot, ping our Bot Support if you want a better username for it. Just make sure the bot is fully operational before you do this.

Use this token to access the HTTP API:
xxxxxxxx:xxxxxxxxxxxxxx
Keep your token secure and store it safely, it can be used by anyone to control your bot.

For a description of the Bot API, see this page: https://core.telegram.org/bots/api
```

其中 `xxxxxxxx:xxxxxxxxxxxxxx` 為您的機器人令牌

## 2、配置 - 讓Bot正常響應

> Telegram SMS 採用 Long Polling 來實現指令監聽，故無需設置 Webhook。如果Bot之前設置過 Webhook，請訪問 `https://apt.telegram.org/bot<您的機器人令牌>/setwebhook` 來清除 Webhook 設定

* 將上面獲取到的機器人令牌填入機器人令牌一欄。

>如果您使用電腦配置這個Token，並能使用 ADB 進行調試。您可以將輸入焦點放在機器人令牌一欄，使用 `adb shell input text <您的機器人令牌>`（需要當前系統環境中含有adb），這將模擬鍵盤輸入機器人令牌。

* 在 Telegram 上給機器人發一句話，內容任意。 （如果您在前面發送過 `/start` 此步驟可省略）

* 點擊 “獲取最近的對話ID”，選擇您的賬戶。

* 填寫一個可信的電話號碼，這個電話號碼用於使用簡訊遠程控制。您可以使用這個號碼來發送簡訊，重啟後台服務。

* 選擇下方的附加選項

>* 網絡錯誤回退到簡訊 - 當消息發送失敗的時候，通過簡訊發送到可信號碼。
>* 監控電池狀態 - 當充電狀態變動或手機電量過低的時候，發送訊息。
>* 獲取聊天命令 - 使用聊天命令管理機器人(不啟用將僅使用簡訊管理)
>* 在雙卡模式下顯示SIM卡別名 - 在消息標題顯示卡別名

* 點擊 `測試並保存`，給予相應的權限。當您收到以下訊息時，配置完成。

```
[系統訊息]
您已成功連接到 Telegram bot 服務器。
```
### 注意
* Telegram SMS 需要您禁用電池優化功能，禁用電池優化功能將使程序能夠穩定快速的接收您的消息。如若使用代理軟件，請一併設置禁止電池優化。

* 當您使用MIUI等系統時，請注意在設置中將電池限制關閉，並且啟用開機自動啟動。當您需要接收通知類簡訊的時候，請在設置中將通知類簡訊權限打開。

* MIUI系統自帶的MIUI優化功能，可能導致程序後台被殺死，故建議關閉。 （該情況未實際確認）

* 如果您的系統無法正常接收簡訊通知，這是因為系統限制的原因，請將本應用設置為默認簡訊APP。

## 3、簡訊 - 使用可信手機控制機器人

您可以為自動轉髮指定可信電話號碼。機器人從該號碼收到消息後將自動轉發，格式如下：

```
{接收方電話號碼}
{簡訊內容}
```

例子：

```
800
11
```

它會將內容 `11` 的簡訊發送到號碼`800`。

您可以通過發送命令 `restart-service` 重新啟動所有後台進程

**如果您不在當前區域，請添加您的國家/地區呼叫區號（例如，台灣國際區號： 886）。**

## 4、命令 - 使用聊天命令控制機器人

您可以通過發送`/start`命令獲取當前可用儀表的列表。

發送簡訊的格式是：

```
/sendsms
{接收方電話號碼}
{簡訊內容}
```
例如：
```
/sendsms
800
11
```
它會將內容`11`的簡訊發送到號碼`800`。

使用`/sendsms`通過默認 SIM 卡發送。當您使用雙卡時，使用`/sendsms1`通過第一張SIM卡發送簡訊，使用`/sendsms2`通過第二張SIM卡發送簡訊（如果可用）。

您可以使用 Telegram 的回复功能快速回複收到的簡訊和未接來電。 （清除日誌時，日誌清除前的訊息將無法快速響應。）

當電話權限不可用時，您只能使用默認的 SIM 卡發送簡訊。