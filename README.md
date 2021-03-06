<h1 id="-p-align-center-vktgbot-v0-8"><p align="center">vktgbot</h1>
<p align=center>
    <a target="_blank" href="https://www.python.org/downloads/" title="Python Version"><img src="https://img.shields.io/badge/python-%3E=_3.5-purple.svg"></a>
    <a target="_blank" href="https://github.com/alcortazzo/vktgbot/releases"><img alt="docker image" src="https://img.shields.io/github/v/release/alcortazzo/vktgbot?include_prereleases"></a>
    <a target="_blank" href="LICENSE" title="License: GPL-3.0"><img src="https://img.shields.io/github/license/alcortazzo/vktgbot.svg?color=red"></a>
</p>    
<p align="center">Telegram Bot on Python for repost from VKontakte community pages (group, public page or event page) to Telegram Channels.
<p align="center">
    <a href="#what-is-now-implemented">What is now implemented</a>
    &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
    <a href="#how-bot-works">How bot works</a>
    &nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
    <a href="#installation--usage">Installation & Usage</a>
</p>
<p align="center">
<a href="https://youtu.be/DyLmaJg0v-w?t=3">
<img src="https://i.imgur.com/rxmbC80.png"/>
</a>
</p>

## What is now implemented
|Type of VK post|Is implemented?|What bot will send to Telegram
|:---:|:---:|:---:|
|Text post|**Yes**|Text post
|Text post with **photo** / gif|**Yes**|Text post with photo / gif
|Text post with **photos**|**Yes**|Text post & post with photos
|Text post with links|**Yes** |Text post with links
|Text post with (yt/vk) video|**50/50**|Text post with video preview > **VK-API restrictions**
|Text post with audios|**50/50**|Text post **without** audios > **VK-API [restrictions](https://vk.com/dev/audio)**
|Text post with document|**Yes**|Text post with document|
|VK reposts|**Yes**|Post with original post & repost text ([**e. g.**](https://i.imgur.com/FRyo80A.png))
|Text post with polls|Not yet|Just text post for now

### In addition, bot can skip ads posts if  in `config.py`
```python
skipAdsPosts = True
```

## How bot works
* Bot sends and receives request from vk api [get.wall method]
* Then bot compares the id from *last_known_id.txt* with the id of the last post
* If `skipAdsPosts = True` in `config.py` bot will skip ads posts
* If id of the last post is larger than id from *last_known_id.txt* the bot will write a new id to file and call the function **sendPosts()**
 * sendPosts() checks post type and
   * if the post type is just text, it sends one text message to telegram
   * if the post type is text with **one photo**, it sends message with photo to telegram
   * if the post type is text with **photos**, it sends two messages to telegram: text message + message with images
   * if the post type is text with **youtube (or vk) video**, it sends message with **video preview** to telegram (because vk_api does not support youtube video links) 
   * if the post type is text with audio, it sends one text message without audio to telegram *(because vk_api [does not support](https://vk.com/dev/audio)  audio files)*
* Then bot waits for the period set by the user and starts again

## Installation & Usage
### Linux
```bash
# clone the repo
$ git clone https://github.com/alcortazzo/vktgbot.git

# change the working directory to vktgbot
$ cd vktgbot

# install python3 and python3-pip if they are not installed

# install the requirements
$ python3 -m pip install -r requirements.txt
```
### Windows
 **If you want to use git**
```bash
# clone the repo
git clone https://github.com/alcortazzo/vktgbot.git

# change the working directory to vktgbot
cd vktgbot

# install python3 and python3-pip if they are not installed

# install the requirements
python -m pip install -r requirements.txt
```
**If you don't want to use git**
1. [Download](https://github.com/alcortazzo/vktgbot/archive/master.zip)  vktgbot repo as ZIP
2. Unzip vktgbot to your folder (for example C:\\Users\\%username%\\bots\\)
3. Then open **cmd** or **powershell**
```bash
# change the working directory to vktgbot
cd c:\\users\\%username%\\bots\\vktgbot

# install the requirements
python -m pip install -r requirements.txt
```
### Open **config** file and update the following variables:
```python
tgChannel = '@aaaa'
tgBotToken = '1234567890:AAA-AaA1aaa1AAaaAa1a1AAAAA-a1aa1-Aa'
vkToken = '00a0a0ab00f0a0ab00f0a6ab0c00000b0f000f000f0a0ab0a00b000000dd00000000de0'
vkDomain = 'aaaaaaaa'
```
* `tgChannel` is the link to channel in telegram `t.me/>>aaaa<<`. **You must add bot to this channel as an administrator**
* `tgBotToken` is the bot token from [BotFather](t.me/BotFather)
* `vkToken` is vk service token. [HowToGet](https://youtu.be/oGS683RYmg8)
  * **If the group is closed you should use your personal access token! [HowToGet](https://github.com/alcortazzo/vktgbot/wiki/How-to-get-personal-access-token)**
* `vkDomain` is the link to vk public `vk.com/>>aaaaaaaa<<`
#### Open **last_known_id.txt** file and write in it id of the last (not pinned!) post (optional):
* Example: if link to post is `https://vk.com/wall-22822305_1070803` id of this post will be `1070803`
* [PhotoExemple](https://i.imgur.com/eWpso0C.png)
### Launch the bot
#### Linux
```bash
$ python3 bot.py
```
#### Windows
```bash
python bot.py
```

## License

GPLv3<br/>
Original Creator - [alcortazzo](https://github.com/alcortazzo)
