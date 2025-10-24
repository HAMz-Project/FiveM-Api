# FiveM-Api
Fivem Api Documentation

## User
- User Session (GET)  : https://forum.cfx.re/session/current.json </br>
- Information (GET)   : https://forum.cfx.re/u/{username}.json </br>
- CSRF Session (GET)  : https://forum.cfx.re/session/csrf.json </br>
- Username Check (GET): https://forum.cfx.re/u/check_username.json?username={username} </br>
- Email Check (GET)   : https://forum.cfx.re/u/check_email.json?email={email} </br>
- Policy User (GET)   : https://policy-live.fivem.net/api/getUserInfo/{id} </br>
- Send Email (POST)   : https://forum.cfx.re/u/action/send_activation_email </br>
&nbsp;&nbsp;&nbsp;&nbsp;Header : {</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'Cfx-Entitlement-Ticket': {input ownership ticket},</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'x-requested-with': 'XMLHttpRequest',</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'discourse-present': 'true',</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'x-csrf-token": {input csrf},</br>
&nbsp;&nbsp;&nbsp;&nbsp;}</br>
&nbsp;&nbsp;&nbsp;&nbsp;Data = username: {input your username}</br>

## FiveM
- Main Information (GET)        : http://{ip:port}/info.json </br>
- Dynamic Information (GET)     : http://{ip:port}/dynamic.json </br>
- Player Information (GET)      : http://{ip:port}/players.json </br>
- Server List Information (GET) : https://servers-frontend.fivem.net/api/servers/single/{address} </br>
- All Server Data (GET)         : https://servers-frontend.fivem.net/api/servers/streamRedir </br>
- Top Server (Country) (GET)    : https://servers-frontend.fivem.net/api/servers/top/{language} </br>
- Upvote Informartion (GET)     : https://servers-frontend.fivem.net/api/upvote/ (header seperti diatas) </br>
- Player Playtime (GET)         : https://lambda.fivem.net/api/ticket/playtimes/{ip:port}?identifiers[]={identifier} </br>
- Promotions (GET)              : https://runtime.fivem.net/promotions_targeting.json </br>
- CnL (GET)                     : https://lambda.fivem.net </br>
- CnL Heartbeat (GET)           : https://cnl-hb-live.fivem.net </br>
- Top Server (GET)              : https://runtime.fivem.net/pins.json </br>
- Sentry Login (GET)            : https://sentry.fivem.net/auth/login </br>
- Build Change Log (GET)        : https://changelogs-live.fivem.net/api/changelog/versions/{buildversion} </br>
- NUI Blacklist (GET)           : https://runtime.fivem.net/nui-blacklist.json </br>
- Players Count (GET)           : https://runtime.fivem.net/counts.json </br>
- Players Count FiveM (GET)     : https://static.cfx.re/runtime/counts.json </br>
- Players Count RedM (GET)      : https://static.cfx.re/runtime/counts_rdr3.json </br>
- Tweet (GET)                   : https://runtime.fivem.net/tweets.json </br>
- Artifact Data (GET)           : https://changelogs-live.fivem.net/api/changelog/versions/win32/server </br>
- Loading Screen (GET)          : http://niklasvh.github.io/WebGL-GTA or https://runtime.fivem.net/loadscreen/spotlight-2/WebGL-GTA </br>
- Pool Size Limits FiveM (GET)  : https://content.cfx.re/mirrors/client/pool-size-limits/fivem.json </br>
- Pool Size Limits RedM (GET)   : https://content.cfx.re/mirrors/client/pool-size-limits/redm.json </br>
- Native FiveM (GET)            : https://static.cfx.re/natives/natives.lua </br>
- Native RedM (GET)             : https://static.cfx.re/natives/natives_rdr3.lua </br>
