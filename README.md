# Telebot [![Build Status](https://travis-ci.org/cortinico/telebot.svg?branch=master)](https://travis-ci.org/cortinico/telebot) [![GoDoc](https://godoc.org/github.com/cortinico/telebot?status.svg)](https://godoc.org/github.com/cortinico/telebot)

A simple Telegram bot skeleton written in Go.

## Usage

You simply need a configuration (BotName + API Key) and a Response function.

Checkout this sample code:
```go
package main

import "github.com/cortinico/telebot"

func main() {
	conf := telebot.Configuration{
		BotName: "SampleBot",
		ApiKey:  "123456789:AAAAAAAPIKEYHEREEEEEEE",
	}

	var bot telebot.Bot

	bot.Start(conf, func(receivedMessage telebot.TeleMessage) (string, error) {
		var answer string

		var user := receivedMessage.From.Uname
		mess := receivedMessage.Text

		switch mess {
		case "/test":
			answer = "Test command works :)"
		default:
			answer = "Hi" + user + ": you typed " + mess
		}
		return answer, nil
	})
}
```

## TeleMessage type
telebot.TeleMessage is a telebot type which represents message received from Telegram.

Details about the specific message:
```go
type TeleMessage struct {
	Text  string   //received text
	Mesid int64    //message ID
	From  teleFrom //sender info
	Chat  teleChat //chat info
	Date  int64    //received date
}
```

Details about the sender of the message:
```go
type teleFrom struct {
	Frmid   int64  //sender ID
	Fstname string //first name
	Sndname string //second name
	Uname   string //username
}
```

Details about the chat of the message:
```go
type teleChat struct {
	Chatid  int64  
	Fstname string 
	Sndname string 
	Uname   string 
}
```
## Licence

The following software is released under the [MIT Licence](https://github.com/cortinico/telebot/blob/master/LICENSE)
