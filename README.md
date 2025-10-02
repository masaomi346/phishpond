# masaomi346/phishpond
<p align="center"><img src="./phishpond.png"></p>

Unofficial maintained of phishpond

## What is phishpond?
https://github.com/zerofox-oss/phishpond

## Changed
PHP 7.4.x -> 8.3.x
mysql 5.7.x  -> 8.4.x

## How to use
1. `git clone https://github.com/masaomi346/phishpond.git`
2. Place phishing kit on `./phishpond/www/`.
3. `cd ./phishpond/`
4. Configure any db connection strings within `docker-compose.yml`
5. Run `docker compose up -d`
6. Browse to `http://localhost:5800` for the virtual browser
7. Browse to `http://localhost:8080/?token=mitm` for mitmproxy
8. Within the virtual browser navigate to `http://phishpond.local`

(Certificates setup)
1. Open preferences within the virtual browser
2. Search `cert`
3. Click `view certificates`
4. Click the authorities tab
5. Click Import
6. Import `/config/certs/mitmproxy-ca-cert.pem`
7. Tick `Trust this CA to identify websites`
8. OK

You will need to repeat these steps every time you remove the `browser-volume`
