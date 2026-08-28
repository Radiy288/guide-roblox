# What you need

- HxD (or any other hex editor)
- x32dbg ([download](https://sourceforge.net/projects/x64dbg/files/snapshots/))
- 10 letter domain
- Webserver (this guide assumes you are using php)
- 2016 client (download one from [here](https://archive.roblonium.com/Client/Windows/RobloxPlayer/main%20%28roblox.com%29/2016/))
- 2016 rcc ([here is a video on how to get it](https://files.catbox.moe/b3k2rf.mp4), the zip file with all the dlls and stuff is at [https://files.catbox.moe/vokn4m.zip](https://files.catbox.moe/vokn4m.zip))
- Keypair generator ([download](https://files.catbox.moe/9o59cx.zip))
- Premade website files ([download](https://files.catbox.moe/uj6l9d.zip))

# Client

1. Open up your hex editor on `RobloxPlayerBeta.exe`, go to text replace, search for `roblox.com` and replace all with your 10-letter domain.

   ![replace example](https://files.catbox.moe/wans4c.png)
   
3. Extract the keypair generator and run the exe file in the folder. After that, open `PublicKeyBlob.txt` and copy the contents.
4. Go inside your hex editor again and do a normal text search for `BGIAA`. After that, select the whole BGIAA string that comes up and replace it with the one from the file (just do ctrl v). After that, you can save the file.
   ![search example](https://files.catbox.moe/z0ycad.png)
   
   ![bgiaa example](https://files.catbox.moe/re5ask.png)
   
   ![replaced bgiaa](https://files.catbox.moe/re5ask.png)
5. Open up `AppSettings.xml` in the client folder and replace `roblox.com` with your 10-letter domain. (keep www)
6. Create a batch file in the same folder and put `RobloxPlayerBeta.exe -a "http://www.yourdomain.tld/" -j "http://www.yourdomain.tld/join?placeId=1818&username=usernamehere" -t ""` inside. This will be used to start the client.

# RCC

1. Open up your hex editor on `RCCService.exe`, go to text replace, search for `roblox.com` and replace all with your 10-letter domain.
   (image is above just do the same thing)
2. Do a normal text search for `versioncompatibility`, after that in the left pane zero it out as [in this video](https://files.catbox.moe/yuz866.mp4). After that, you can save the file and close the hex editor.
3. Open up `AppSettings.xml` in the RCC folder and replace `roblox.com` with your 10-letter domain. (keep www)
4. Open x32dbg from `\release\x32` in the downloaded zip file (NOT x64dbg!) and open `RCCService.exe`. After that, right click in the middle of the window, and click on `Search for > All modules > String references`.

   ![x32dbg search](https://files.catbox.moe/o5k0vh.png)
5. After that, wait for the progress bar at the bottom to complete and after that click on the text box and type in `sysstats`.
6. Follow the steps in [this video](https://files.catbox.moe/yuz866.mp4). (for editing the jne, je, push etc press space after you have selected it in the window)
7. Go at the top of the window to `File > Patch file` and click on Patch file and save the file in the same folder. (give it another name or you won't be able to save it)
8. Create a batch file in the same folder and put `yourexecutablename.exe /console /placeid:1818` inside. This will be used to start the rcc.

# Webserver

1. Extract the premade website files to your server.
2. Go to [this website](https://emn178.github.io/online-tools/md5_checksum.html) and put your `RobloxPlayerBeta.exe` in and get the MD5 hash. After that, go into `GetAllowedMD5Hashes > index.php` on your server and paste the md5 hash in there.
3. Launch `RobloxPlayerBeta.exe` with the argument --version and note the version in the message box. Then, go into `GetAllowedSecurityVersions > index.php` and edit the version number to the one on the client and leave `pcplayer` unchanged.
4. Go inside `join > index.php` and edit the server ip, port and baseurl if necessary.
5. Replace `join > PrivateKey > PrivateKey.pem` with the file from the key generator folder from earlier.
6. Go inside the `asset` folder and place an rbxl file named `1818` with no file extension inside. This will be used by the rcc to host.

# Domain

1. Make records on `@`, `*`, and `*.*` on your domain.
2. Please use Cloudflare and disable https redirects.

# Ending

- Use your batch file on the RCC to start it up.
- Use your batch file on the client to start it up.

~~DM me on Discord if anything does not work and I'll help fix.~~
