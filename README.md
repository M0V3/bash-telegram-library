# Bash Telegram Library
Telegram bot library written in bash
  
  
## Introduction
teleLib.sh is intended to be used as a library by other bash scripts.  

It's meant to be easy to understand and fast to use.  

If you want to write an actual bot with many features you should probably look into nodejs or other languages.
  
  
## Using teleLib.sh
Following these steps you should be up and running within about 2 minutes.

### Prerequisites
teleLib.sh depends on:  
* curl
* jq  


Depending on your OS you can install these using the default package manager.  

If you are running a current Debian (based) OS, simply run

```apt install curl jq```

### Installation
teleLib.sh is installed by downloading the script and placing it either next to your main script or in any accessible directory.

Choose where you want teleLib.sh to be located and download it

```wget https://raw.githubusercontent.com/M0V3/bash-telegram-library/master/teleLib.sh```

*or*

```curl -O https://raw.githubusercontent.com/M0V3/bash-telegram-library/master/teleLib.sh```

### Usage
First things first: include teleLib.sh in your script

```source teleLib.sh```

Initialize teleLib.sh with your Bot API Token

```teleLib_init YourTokenHere```

Now you are already able to use any function you can find in the next section.

The following example sends "Its working!" to user id 1337

```
source lib/teleLib.sh
teleLib_init YourTokenHere
teleLib_sendMessage 1337 "Its working!"
```


## Functions
After executing a function you can find the results in the following variables

```functionName_result```: json response of the API

```teleLib_successful_result```: 0/1; 1 = success, 0 = failure

```teleLib_handleResponse_result```: formatted string (success or errorcode + error message)

### teleLib.sh functions

#### init [botApiToken]
```teleLib_init '123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11'```

#### successful [jsonString]
Looks for the index "ok" in the given json and returns 1 for true and 0 for false.

```teleLib_successful '{"ok":false,"error_code":404,"description":"Not Found"}'``` --> 0

#### handleResponse [jsonString]
Uses "successful" to check for success or failure and returns a formatted string. "success" for 1 and "ErrorCode - ErrorMessage" for 0

```handleResponse '{"ok":false,"error_code":404,"description":"Not Found"}'``` -> 404 - Not Found

### Telegram functions
These functions are named after [Telegram API methods](https://core.telegram.org/bots/api#available-methods), go there for in-depth descriptions.

Optional parameters are enclosed in {these pointy mofuggas}

#### getMe
```teleLib_getMe```

#### sendMessage [chat_id] [text] {parse_mode} {disable_web_page_preview} {disable_notification} {reply_to_message_id} {reply_markup}
```teleLib_sendMessage 1337 "Its working!"```

```teleLib_sendMessage 1337 "Its *working*!" "Markdown" false true```

#### forwardMessage [chat_id] [from_chat_id] [message_id] {disable_notification}
```teleLib_forwardMessage 1337 7331 27```

#### sendPhoto [chat_id] [photo] {caption} {parse_mode} {disable_notification} {reply_to_message_id} {reply_markup}
```teleLib_sendPhoto 1337 "https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png"```

