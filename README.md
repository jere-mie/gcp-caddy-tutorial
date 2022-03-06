# gcp-caddy-tutorial
Instructions for deploying a website to the web using Google Cloud Platform and Caddy

## Some scripts to run on your VPS

```bash
sudo apt update
sudo apt upgrade
sudo apt install python3 python3-pip git htop vim screen dnsutils
```

## Installing Caddy

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

## Configuring Caddy

```bash
cd ~

# here, put in your Caddyfile config
nano Caddyfile

sudo caddy stop
sudo caddy start
```

## Setting up the sample site

```bash
git clone https://github.com/WinHacks/flask-workshop
cd flask-workshop
cp *.json secrets.json

# update your secret
nano secrets.json

# change debug=True to debug=False in app.py
nano app.py

# install dependencies
pip3 install flask flask-sqlalchemy

# run the app!
python3 app.py &
```
