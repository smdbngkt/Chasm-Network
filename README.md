
![Logo](https://superoo7.com/images/chasm-scout/cover.png)


# Cara Testnet Install Charm Network



## Step 1. Mint NFT untuk dapatkan Scout ID dan Api Key

### Buka https://scout.chasm.net


![Logo](https://superoo7.com/images/chasm-scout/mint.gif)

#### kamu akan mendapatkan WEBHOOK_API_KEY dan SCOUT_UID dari sini.

## Step 2: Dapatkan Groq API Key

###  Buka [Groq](https://console.groq.com/keys) dan dapatkan Api Keynya

![logo](https://superoo7.com/images/chasm-scout/groq.gif)

## Step 3: Install Dockers (jika sudah install bisa skip)

### Install docker dan mengaktifkan port 3001

``` 
sudo ufw status
sudo ufw allow 3001
sudo ufw allow 3001/tcp
sudo ufw allow 22/tcp
sudo ufw reload
sudo ufw enable
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install Docker
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin 
```

### Buat .env

```
nano .env
```

### Isi Semua Yang Belum di Isi

```
PORT=3001
LOGGER_LEVEL=debug
ORCHESTRATOR_URL=https://orchestrator.chasm.net
SCOUT_NAME=
SCOUT_UID=
WEBHOOK_API_KEY=
WEBHOOK_URL=http://IP:3001/
PROVIDERS=groq
MODEL=gemma2-9b-it
GROQ_API_KEY=
OPENROUTER_API_KEY=
OPENAI_API_KEY=
```

### Jalankan Nodemu!

```
# Pull the code from DockerHub
docker pull chasmtech/chasm-scout
# Start the docker file
docker run -d --restart=always --env-file ./.env -p 3001:3001 --name scout chasmtech/chasm-scout
```

### Cek Apakah Node Aktif

#### paste kode di bawah

```
source ./.env
curl -X POST \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $WEBHOOK_API_KEY" \
     -d '{"body":"{\"model\":\"gemma2-9b-it\",\"messages\":[{\"role\":\"system\",\"content\":\"You are a helpful assistant.\"}]}"}' \
     $WEBHOOK_URL
```

#### atau bisa kunjungi https://scout.chasm.net













