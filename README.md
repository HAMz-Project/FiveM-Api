# FiveM-Api
Fivem Api Documentation

# User
User Session (GET)  : https://forum.cfx.re/session/current.json </br>
Information (GET)   : https://forum.cfx.re/u/{username}.json </br>
CSRF Session (GET)  : https://forum.cfx.re/session/csrf.json </br>
Send Email (POST)   : https://forum.cfx.re/u/action/send_activation_email </br>
                      Header : {</br>
                          'Cfx-Entitlement-Ticket': {input ownership ticket},</br>
                          'x-requested-with': 'XMLHttpRequest',</br>
                          'discourse-present': 'true',</br>
                          'x-csrf-token": {input csrf},</br>
                      }
                      Data = username: {input your username}</br>

# Server
Main Information (GET) : IP:PORT/info.json </br>
Dynamic Information (GET) : IP:PORT/dynamic.json </br>
Player Information (GET) : IP:PORT/players.json </br>
Server List Information (GET) : https://servers-frontend.fivem.net/api/servers/single/{ username keymaster } </br>
All Server Data (GET) : https://servers-frontend.fivem.net/api/servers/stream/1658188050/
