# ServerStatus
there is a `customize design version for nanqinlang`

Live demo : https://status.nanqinlang.com

this repo works as this following :
1. `server` listens on tcp port 65535
2. `client` connects to the server
3. `client` generates statistics and periodically send it to the server(defaultly as 5 seconds)
4. `server` writes statistics to `~/website/json/stats.json`
5. `server` provides HTML page with JavaScript to let users load

include dir :
- `~/client` client files
- `~/server` server files
- `~/website` website files

# server
### clone required files
```bash
git clone https://github.com/nanqinlang/ServerStatus-nanqinlang.git
```

### server config
to modify config file: `/ServerStatus/server/config.json`  
make sure that `username and password` must be the same as client  
example:
```json
{ "servers":
	[
		{
			"username": "nanqinlang1",
			"name": "南琴浪博客",
			"type": "KVM",
			"location": "LosAngeles",
			"password": "nanqinlang",
		},	
	
	
		{
			"username": "nanqinlang2",
			"name": "www.nanqinlang.com",
			"type": "KVM",
			"location": "LosAngeles",
			"password": "nanqinlang",
		}
		
	]
}
```

### running server
```bash
cd ~/ServerStatus/server
chmod 7777 ServerStatus
./ServerStatus --config=config.json --web-dir=~/ServerStatus/website(your ServerStatus dir)

# background working
nohup ./ServerStatus --config=config.json --web-dir=~/~ &
(then press ctrl+c to quit nohup prempts)
```

### load your ServerStatus website
additional, you should keep a `http server` to load HTML of ServerStatus  
advises to use like `nginx`
```nginx
# if use nginx, just add this rule
server {
	root ~/ServerStatus/website;
	index index.html;
}
```

# client
this client only works on `Linux`  
### modify client config
vim client.py
```
# ip of server
SERVER = "x.x.x.x"
# if there are both server and client in your vps, use "127.0.0.1"

# listen port, stay no change
PORT = 65535

# username
USER = "nanqinlang2" 

# password
PASSWORD = "nanqinlang"

# statistics update interval(second)
INTERVAL = 5
```

### running client.py
upload `client.py` to your client vps, then
```
nohup python client.py &
```