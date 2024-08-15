HTTPIE
======

httpie is an open source API cli tool that improves upon curl. Just how vim improved vi, httpie imporves curl. 

Install HTTPIE
--------------
```
curl -SsL https://packages.httpie.io/deb/KEY.gpg | sudo gpg --dearmor -o /usr/share/keyrings/httpie.gpg
sudo su -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/httpie.gpg] https://packages.httpie.io/deb ./" > /etc/apt/sources.list.d/httpie.list'
sudo apt update && sudo apt install httpie -y 
```

HTTPIE Basics:
-------------
```
# Basic GET Request to example.com
http --pretty=format GET "https://example.com" "Authorization:Bearer $API_KEY" "Accept:application/json"  >> example.json

# POST Request with JSON Data to example.com
http --pretty=format POST https://example.com "Authorization:Bearer $API_KEY" "Accept:application/json"  >> example.json

# PUT Request with JSON Data to example.com
http --pretty=format PUT https://example.com "Authorization:Bearer $API_KEY" "Accept:application/json"  >> example.json
```

HTTPIE OpenSeach Ex:
---------------------
```
http --auth your_username:your_password POST https://IP-OR-Domain:9200/your-index/ Content-Type:application/json < example.json
```

HTTPIE MISP EX:
---------------
```
http --verify=no --pretty=format GET "https://IP-OF-Server/events/index" "Authorization: MISP-API-KEY" "Accept:application/json" >> misp.json
```

HTTPIE Meraki EX:
-----------------
```
http --pretty=format GET "https://api.meraki.com/api/v1/networks/$network_id/alerts/history" "Authorization:Bearer $API_KEY" "Accept:application/json"  >> alerts.json
http --pretty=format GET "https://api.meraki.com/api/v1/networks/$network_id/events?productType=$product_type" "Authorization:Bearer $API_KEY" "Accept:application/json" >> events.json
```

References:
-----------

https://httpie.io/