# FiveM-Api
Fivem Api Documentation

# User
User Session (GET)  : https://forum.cfx.re/session/current.json </br>
Information (GET)   : https://forum.cfx.re/u/{username}.json </br>
CSRF Session (GET)  : https://forum.cfx.re/session/csrf.json </br>
Username Check (GET): https://forum.cfx.re/u/check_username.json?username={username} </br>
Email Check (GET)   : https://forum.cfx.re/u/check_email.json?email={email} </br>
Policy User (GET)   : https://policy-live.fivem.net/api/getUserInfo/{id} </br></br>
Send Email (POST)   : https://forum.cfx.re/u/action/send_activation_email </br>
&nbsp;&nbsp;&nbsp;&nbsp;Header : {</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'Cfx-Entitlement-Ticket': {input ownership ticket},</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'x-requested-with': 'XMLHttpRequest',</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'discourse-present': 'true',</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'x-csrf-token": {input csrf},</br>
&nbsp;&nbsp;&nbsp;&nbsp;}</br>
&nbsp;&nbsp;&nbsp;&nbsp;Data = username: {input your username}</br>

# Server
Main Information (GET)        : IP:PORT/info.json </br>
Dynamic Information (GET)     : IP:PORT/dynamic.json </br>
Player Information (GET)      : IP:PORT/players.json </br>
Server List Information (GET) : https://servers-frontend.fivem.net/api/servers/single/{address} </br>
All Server Data (GET)         : https://servers-frontend.fivem.net/api/servers/stream/1658188050/ </br>
Top Server (GET)              : https://servers-frontend.fivem.net/api/servers/top/{language}
