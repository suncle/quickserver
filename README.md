# Quick-Server
## A Server Framework Based On OpenResty

---
## Latest Version 0.3.9
- **Coming Soon 0.4.0**
- **0.4.0-rc0 is released**

## Installation

### Install via Docker

1. Install Docker. Please refer to https://www.docker.com/
2. Run command: docker pull chukong/quick-server
3. And please refer this documents for next steps: [Deploy Quick-Server with Docker] (https://github.com/dualface/quickserver/wiki/%E7%94%A8Docker%E9%83%A8%E7%BD%B2Quick-Server)

### Install via Shell Script

1. Download codes from github or osc.

   github:
   https://github.com/dualface/quickserver.git
   
   OSChina mirror:
   https://git.oschina.net/cheerayhuang/quick-x-server.git
   
2. Run shell script **install_ubuntu.sh** in root of codes dir.

## Change Log

### 0.4.0-rc0
- FEATURE: Add an new action "SessionAction" to generate **session_id** for user.
- FEATURE: adjust many interfaces in RanklistAction. 
    - Each interface calling needs checking **session_id**. 
    - "Add" interface can generate a uid according to the **nickname** when user calls it first time.
    - the format of uid is "nickname+numbers" in order to keep each uid unique.
    - score, remove, getrank and getrevrank should get key from param "uid".
    - "GetRevRank" also replies score.
    - "GetRankAction" also return socre.
    - "AddAction" can return a percent to indicate "rank/total", in other words, it's the user's positiono in a ranklist.
    - Add some test cases for RanklistAction.
- BUGFIX: if a redis command fails, it replies an int 0 not a string "0".

### 0.3.9
- FEATURE: implement a ranklist with friendship based on social network platform.(only support Weibo now)
- FEATURE: Each interface calling needs checking **session_id**.
- FEATURE: ADD some test cases for FriendshipAction.
- BUGFIX: table.length() method in function.lua moduel.

### 0.3.8 
- FEATURE: implement chatting room, ChatAction module. 
    - Add a new sub-table as the configuration for ChatAction in config.lua.
    - assign an user to a channel automatically.
    - Add some tests cases for ChatAction. 
- IMPROVE: remove BeginSession interface.  
- IMPROVE: optimize some lua codes in the initialization of mysql and redis.

### 0.3.7

- FEATURE: implement user login function through Cocochina platform.
- FEATURE: when invoking the service of Quick-Server via either http or WebSocket, to verify session ID is needed.
- IMPROVE: implment user.uploadcodes action instead of "user/codes" web interface. The original http interface "user/codes" will be obsoleted in next release.
- OTHER MINOR CHANGES:
   - BUGFIX: fix some bugs in http.lua and url.lua.
   - CHANGE: add a configuration into nginx.conf for DNS server.
   - IMPROVE: Write a new shell named "status\_quick\_server.sh" to show the status of Quick-Server processes.
   - IMPROVE: implement two functions to release mysql and redis connections. 
   - IMPROVE: After installation, server/config.lua should not be compiled in order to be configured by user conveniently.
   - BUGFIX: fix a slight mistake in urlencodeChar() of functions.lua.
   - BUGFIX: the param "value" of Ranklist.Add is allowed to be a string.
   - BUGFIX: fix the version of luajit in "compile_bytecode.sh", change it to "luajit-2.1.0-alpha".
   - IMPROVE: StoreObj returns a id  which don't includes "/" symbol definitely.
   - IMPROVE: change the level of error() in the method "throw" of debug.lua in order to make error messge more concise.

### 0.3.6

- UPGRADE: OpenResty 1.4.1 to 1.7.2. 
- IMPROVE: support accessing user-defined codes via WebSocket besides HTTP.
- BUGFIX: fix LUA_PATH of index-cleaner script.
- DOCS: improve wiki in Chinese based on github wiki.
- CHANGE:  Quick-Server is released in bytecode generated by Luajit via Docker. And modify shell script in Ubuntu for some installation errors.

### 0.3.5

- Adjust directory structure of project, make it more simpler and cleaner.
- Integrate lua-resty-http with quick-server. 
- Fix and mend some confinguration in nginx.conf.

### 0.3.1
- Fix bug: There should be an "actions" sub-dir in root of user-defined codes.  
- Fix bug: Allow the type of response of HTTP is "string".
- Improve: Support case-insensitive uri.

### 0.3.0
- Improve the implemnet of user-defined function, supporting sub-dir structure deployment.

### 0.2.0
- Support user-defined function via uploading lua codes by users themselves.
- Support Http protocol for invoking interfaces. 
- Docker becomes a new way which users can choose for installation besides shell script. 

### 0.1.0
- Support Object Store based on MySql 5 with JSON format.
- Support Index in Object Store.
- Implement Ranklist function based on Redis. 
- All interfaces is based on WebSocket protocol.




