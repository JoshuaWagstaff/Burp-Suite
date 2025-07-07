# Writeup
# Burp Suite

## Objective

Comprehensive use of burpsuite for the following and more:

-Bypass the login form to authenticate as Bender via SQL injection

-Escalate to the real administrator account with a targeted SQLi payload

-Recover the administrator’s password by brute-forcing with Burp Intruder

-Download a “.bak” backup file despite an extension-filter by abusing a null-byte trick

-Discover and navigate to the hidden Angular “Administration” route in the single-page app

-Exploit an IDOR to view another user’s shopping basket by tampering the basket ID

-Bulk-delete all 5-star reviews via the admin panel’s delete-review API calls

-Trigger a purely client-side (DOM) XSS through the search box

-Persistently inject an XSS payload via a custom HTTP header (True-Client-IP)

-Perform a reflected XSS on the Order History tracking page by injecting into the URL

### Skills Learned

-Intercepting and forwarding HTTP(S) requests in Burp Proxy

-Crafting and injecting JSON payloads for POST login requests

-Writing basic SQLi payloads (' OR 1=1--, valid-email plus --)

-Using Burp Intruder: marking payload positions, loading wordlists, spotting a 200 OK response

-Bypassing file-extension checks with URL-encoded null-bytes (%00)

-Inspecting and searching bundled JavaScript in Browser DevTools to enumerate client routes

-Manually navigating SPA fragments (e.g. /#/administration)

-Tampering REST resource IDs (IDOR) and replaying requests with valid Bearer tokens

-Mapping UI actions (trash-icon clicks) to underlying DELETE/POST API calls

-Crafting DOM XSS payloads (<iframe src="javascript:alert('xss')">) and URL-encoding them

-Adding and persisting HTTP headers in Burp Proxy Inspector

-Distinguishing between DOM, persistent (via header), and reflected XSS

-URL-based reflected XSS injection on tracking endpoints

### Tools Used

Burp Suite Community Edition

Proxy (Intercept & Forward, Inspector)

Intruder (Sniper)

Browser & Extensions

-Firefox/Chrome with FoxyProxy

-Developer Tools: Debugger/Sources, Network/Inspector

--Wordlist

-best1050.txt (common-credentials pack)

-Manual Techniques

-URL-bar injection

-Null-byte URL trick (%00)

## Steps
---
Ref.1: we will turn burp intercept on and proxy to capture info
<img width="812" alt="1-- we will turn burp incercept on and proxy to capture info " src="https://github.com/user-attachments/assets/c98c6e9a-aab6-4ce6-b22a-d71d0b6ca2d4" />
---
Ref.2: Captured login request in burpsuite
<img width="910" alt="2- captured login request in burpsuite" src="https://github.com/user-attachments/assets/100ef967-bd2a-4150-b985-f15aa20f6987" />
---
Ref.3: Use sql injection on captured request
<img width="467" alt="3= use sql injection on captured request" src="https://github.com/user-attachments/assets/48a20662-b533-425b-a386-2ae99bf8f108" />
---
Ref.4: Flag received
<img width="519" alt="4- flag received" src="https://github.com/user-attachments/assets/2191754c-5d3f-4181-a117-4c7513e9d6d0" />
---
Ref.5: Next scenario
<img width="362" alt="5- next scenario" src="https://github.com/user-attachments/assets/4f5fe08e-c9ae-440b-911b-a54f9f7c116d" />
---
Ref.6: Capturing request
<img width="899" alt="6- capturing request" src="https://github.com/user-attachments/assets/a4a331a4-2eb7-4afb-9391-587aecf47cc2" />
---
Ref.7: Forwarding with '-- attached
<img width="329" alt="7- forwarding with '-- attached" src="https://github.com/user-attachments/assets/c0ddd7da-f400-488a-8a4c-1362335a0b6f" />
---
Ref.8: Flag received
<img width="387" alt="8- flag receieved" src="https://github.com/user-attachments/assets/a284fb23-0050-49ab-979e-86194a5ceb86" />
---
Ref.9: Make request
<img width="806" alt="9- make request" src="https://github.com/user-attachments/assets/ef7f5f12-def5-48b6-8030-c2c9f3044521" />
---
Ref.10: Forward to intruder
<img width="366" alt="10- forward to intruder" src="https://github.com/user-attachments/assets/e9568fc9-513a-4deb-9524-b86d49a115f7" />
---
Ref.11: Add payload position in password
<img width="272" alt="11- add payload positionn in password" src="https://github.com/user-attachments/assets/f00fa404-366d-4f5e-8b41-fa65628f4e5e" />
---
Ref.12: Selecting wordlist payload
<img width="863" alt="12- selecting wordlist payload" src="https://github.com/user-attachments/assets/f192dda0-ce38-4cf1-81dd-8a3de885fcec" />
---
Ref.13: Starting attack
<img width="879" alt="13- starting attack" src="https://github.com/user-attachments/assets/6af343ae-b637-489f-82bd-ff97604ff499" />
---
Ref.14: code 200, password found
<img width="841" alt="14- code 200, password found" src="https://github.com/user-attachments/assets/f0d81113-a761-4799-bfa9-d778e765c8f9" />
---
Ref.15: Flag received
<img width="1127" alt="15 - flag received" src="https://github.com/user-attachments/assets/73ea742f-a1ac-415f-b92d-4da783943fab" />
---
Ref.16: We will find exposed data on the site
<img width="1190" alt="16- we will find exposed data on the site" src="https://github.com/user-attachments/assets/369e2433-5ef8-40a3-98ce-a2909b3cbad2" />
---
Ref.17: When we click terms of service we arae brought to this page
<img width="719" alt="17- when we click terms of service we are brought to this page" src="https://github.com/user-attachments/assets/397d4cb5-7fbd-4bff-8249-ba54a4afa3fd" />
---
Ref.18: We will take out legal.md and just go to ftp
<img width="302" alt="18- we will take out legal md and just go to the ftp" src="https://github.com/user-attachments/assets/39d3544e-9209-4626-99b7-a5bb0e73af7e" />
---
Ref.19: We find exposed sensitive data 
<img width="1139" alt="19- we find exposed sentitive data" src="https://github.com/user-attachments/assets/e6e3aa13-7f09-4150-a31e-e414c24393c3" />
---
Ref.20: Flag received
<img width="697" alt="20- flag received" src="https://github.com/user-attachments/assets/3f3ad31a-bfc9-4a65-8fa8-d8f968d5f8e2" />
---
Ref.21: Cant download this package because of a 403 error where only .md and .pdf files can be downloaded
<img width="161" alt="21- cant download this package bexause of a 403 error where only  md and  pdf files can be downloaded" src="https://github.com/user-attachments/assets/b83692cc-2ded-40c0-a6f9-5dea026e4cdf" />
---
Ref.22: Must use a null terminator 
<img width="955" alt="22- must use a null terminator" src="https://github.com/user-attachments/assets/2f2e5dc9-0bf3-4d22-a336-28cc1cd56864" />
---
Ref.23: Edited to include %2500 allowing download
<img width="1242" alt="23- edited to include %2500 md allownig download" src="https://github.com/user-attachments/assets/cbdc767d-e502-4158-94b9-0f30027ca4e8" />
---
Ref.24: Flag received
<img width="974" alt="24- flag received" src="https://github.com/user-attachments/assets/f7c752ec-b3b6-43d3-8764-716efa3281fc" />
---
Ref.25: Broken access controls project
<img width="472" alt="25- broken access controls project" src="https://github.com/user-attachments/assets/2fad7436-51d7-42bb-a7d0-fd187a76f64d" />
---
Ref.26: Open debugger on firefox located page and search for admin
<img width="733" alt="26- open debugger on firefox located page and search for admin" src="https://github.com/user-attachments/assets/7f9d3acf-71f4-4dd0-8c78-87dd010ab6d1" />
---
Ref.27: Found admin path
<img width="271" alt="27- found admin path " src="https://github.com/user-attachments/assets/3ce0eaa5-ac4a-494a-959d-deb03128a7ff" />
---
Ref.28: Log back in to admin using previously captured credentials
<img width="758" alt="28- log back in to admin using previously captured credentials " src="https://github.com/user-attachments/assets/e43c1b92-192d-4406-8073-c742a786953d" />
---
Ref.29: Go to administration path
<img width="470" alt="29- go to administration path" src="https://github.com/user-attachments/assets/04b6b876-24cf-4789-9fa5-eebdc4bbd280" />
---
Ref.30: Flag received
<img width="705" alt="30- flag received" src="https://github.com/user-attachments/assets/7745c525-f746-4d8e-8490-bb64cc53810a" />
---
Ref.31:  New task
<img width="521" alt="31- new task" src="https://github.com/user-attachments/assets/311a130c-bafa-4470-8e6b-b12a62444113" />
---
Ref.32: Capture basket request
<img width="778" alt="32- capture basket request" src="https://github.com/user-attachments/assets/b41bd6f1-8cce-4088-962f-601311565d66" />
---
Ref.33: Change basket id to 2 instead of 1 and forward
<img width="238" alt="33- change basket id to 2 instead of 1 and forward" src="https://github.com/user-attachments/assets/b1cb1253-2cd2-417e-9773-2c2cc0358189" />
---
Ref.34: Flag received
<img width="629" alt="34- flag receieved" src="https://github.com/user-attachments/assets/d5c2f208-8c1d-44bb-9a51-d93b2b4d5b8f" />
---
Ref.35: Next task
<img width="596" alt="35- next task" src="https://github.com/user-attachments/assets/5dded57d-598e-4d52-a354-ebafff3066f2" />
---
Ref.36: 5 star deleted flag received
<img width="853" alt="36- 5 stars deleted flag receieved" src="https://github.com/user-attachments/assets/5bc4b191-ab06-400f-935c-493ebad4f188" />
---
Ref.37: Cross site scripting
<img width="290" alt="37- cross site scripting" src="https://github.com/user-attachments/assets/580dfe09-039a-427b-965a-48ffba65eb5e" />
---
Ref.38: Put in javascript code, success, and flag received
<img width="835" alt="38- put in javascript code, success, flag receieved" src="https://github.com/user-attachments/assets/0773be3a-01f0-43fc-ae1b-871aab06f438" />
---
Ref.39: Perform persistent XSS
<img width="736" alt="39- perform persistent XSS" src="https://github.com/user-attachments/assets/1fbf94ee-448e-46f7-8f25-20c8115e773f" />
---
Ref.40: Captured logout
<img width="659" alt="40- captured logout" src="https://github.com/user-attachments/assets/ea2f8e0d-1f26-4c6d-9160-960f9f3389bf" />
---
Ref.41: Add header with javascript xss
<img width="284" alt="41= add header with javascript xss" src="https://github.com/user-attachments/assets/674ce413-0866-4e9f-afd7-38bb1f76aa90" />
---
Ref.42: After forwarding flag is receieved
<img width="381" alt="42- after forwarding flag is receieved" src="https://github.com/user-attachments/assets/96117bfa-e411-4de0-b677-e10e5c106d94" />
---
Ref.43: Reflected xss
<img width="370" alt="43- reflected xss" src="https://github.com/user-attachments/assets/006ea763-fc88-4ca7-9fb9-1ae6593f8af0" />
---
Ref.44: We will do a reflected attack on this page
<img width="1047" alt="44- we will do a reflected attack on this page" src="https://github.com/user-attachments/assets/fe61942d-b57c-42f6-8b28-fa10310f7599" />
---
Ref.45: We will use this for the xss attack
<img width="596" alt="45- we will use this for the  xss attack" src="https://github.com/user-attachments/assets/e55e6bdf-5320-46ce-b992-28c1b31d846a" />
---
Ref.46: Xss completed
<img width="914" alt="46- xss completed" src="https://github.com/user-attachments/assets/e95eac04-ee33-4d12-a116-cb8b8b1e8968" />
---




































