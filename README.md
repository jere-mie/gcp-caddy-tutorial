# gcp-caddy-tutorial

Instructions for deploying a website to the web using Google Cloud Platform and Caddy

## Signing up for and configuring GCP

-   Head to the [Google Cloud Platform Console](https://console.cloud.google.com/) and sign in with your Google account.
-   Create a new project
-   Enable billing and input your credit card or other billing details
-   Enable compute engine

## Creating your first VPS

-   Head to `Compute Engine > VM Instances`
-   Select "Create Instance"
-   Name your instance whatever you want, and you can keep the zone and region as whatever the default is.
-   Change the "Machine Type" to "e2-micro"
    -   This is so that you can get the server for free!
-   Under "boot disk" select "change"
-   I recommend changing the version to "Debian 11" or, if you prefer Ubuntu, change "Operating System" to Ubuntu, and version to "Ubuntu 21.10"
-   Change the "boot disk type" to "Standard persistent disk"
-   **IMPORTANT** - make sure to check the boxes saying "Allow HTTP traffic" and "Allow HTTPS traffic"
    -   If the boxes aren't checked, people cannot visit your website!
-   Hit "Create"

Your VPS is now created! You can access it by hitting the "SSH" button in the VM Instances list.

## Reserving a static IP address

-   A static IP address needs to be reserved so that your server's IP address won't change
-   Go to `VPC Network > External IP Addresses`
-   You should see your VPS' IP address listed
-   At the far right, press the "reserve" button
-   Choose a name for the IP address
-   And that's it!

Make sure to take note of this IP address for when you connect it to your domain!

## Connecting your domain to your VPS

-   Login to your domain provider (for example, namecheap), and go to your DNS settings page
-   Create a new A record for your domain:
    -   Under "host" you may need to leave it blank or put @ (depending on your domain provider)
        -   This connects the "apex" domain to your VPS. If you prefer a subdomain, such as "www", put that here instead
        -   If you want both your apex domain and "www", create 2 A records
    -   Under "value" put the IP address from the above step

## Some scripts to run on your VPS

```bash
sudo apt update
sudo apt upgrade
sudo apt install python3 python3-pip git htop vim screen dnsutils neofetch
```

## Installing Caddy

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
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
