# Thursday, February 15, 2024

To Do:

- Train Stable Diffusion on kanji dataset

Done:

- Transferred BTC from Bitget to BTCBOX

# Wednesday, February 14, 2024

To Do:

- Train Stable Diffusion on kanji dataset
- Open a Japanese crypto exchange account — done
- Sync the data from lambda-1 and terminate it — done
- Remind Haruka about information for Charles — done
- Furusato Nozei scans — done

# Tuesday, October 31, 2023

Fixing Bluetooth on Ubuntu 22.04:

```bash
sudo rmmod btusb
sudo modprobe btusb
```

# Friday, October 27, 2023

On Linux, you can type an em-dash (—) using Unicode input:

- Hold Ctrl + Shift and type U
- A small underlined "u" should appear
- Type 2014 (the Unicode code for em-dash)
- Press Enter or Space

# Tuesday, August 15, 2023

## [Mystery of Entropy FINALLY Solved After 50 Years! (STEPHEN WOLFRAM)](https://www.youtube.com/watch?v=dkpDjd2nHgo)

We need a theory of the observer. An observer takes a lot of detail about the world and averages it down, or equivalences it down, to make a definite conclusion.

# Thursday, April 20, 2023

## Bluetooth Quick Connect GNOME shell extension

https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/

# Sunday, April 16, 2023

## Language support in Ubuntu

```bash
sudo apt install -y \
    language-pack-gnome-en \
    language-pack-gnome-pl \
    language-pack-gnome-ja
gsettings set org.gnome.desktop.input-sources sources "[('xkb', 'us'), ('xkb', 'pl'), ('xkb', 'jp')]"
check-language-support --show-installed
```

# Tuesday, April 11, 2023

Use `home.kwos.dev` for links to all my personal sites.

## Recording default PulseAudio monitor stream

```bash
parec -d "@DEFAULT_MONITOR@" | lame -r -V0 - recording.mp3
```

# Monday, April 3, 2023

## Connecting to lambda-1 with SSH through Cloudflare Tunnel

Connect the server to Cloudflare:

https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/use_cases/ssh/#1-connect-the-server-to-cloudflare-1

Update the SSH configuration file:

```text
Host lambda-1.kwos.dev
  User ubuntu
  ProxyCommand /usr/local/bin/cloudflared access ssh --hostname %h
  ForwardAgent yes
```

# Sunday, March 26, 2023

## Running Redis Stack

```bash
docker run -d \
    --network=host \
    --name redis \
    --volume /data/redis:/data \
    redis/redis-stack-server:latest
```

# Tuesday, March 2, 2023

## Removing blank lines from a file

```bash
grep '[^[:blank:]]' <file.in >file.out
```

## Running ClickHouse server

```bash
docker run -d \
    --network=host \
    --name clickhouse-server \
    --ulimit nofile=262144:262144 \
    --volume /data/clickhouse:/var/lib/clickhouse \
    --restart unless-stopped \
    clickhouse/clickhouse-server
```

## Renaming `storage` volume to `data`

1. Use Disks app to change mount point from `/storage` to `/data`
2. Rename VG `sudo vgrename vgstorage vgdata`
3. Rename LV `sudo lvrename vgdata storage data`

## Setting up OpenAI File Q&A app

1. Create a Pinecone index `file-q-and-a` with dimension 1536 and cosine metric
2. Set up the OpenAI File Q&A server
   - Export the `OPENAI_API_KEY` environment variable
   - Edit `server/config.yaml` with the Pinecone API key, index name, and environment
   - Run `python app.py` in the `server` directory
3. Set up the OpenAI File Q&A client
   - Run `npm install` in the `client` directory
   - Run `npm run dev` in the `client` directory
   - Open http://localhost:3000 in the browser

# Wednesday, February 22, 2023

## Installing Audio Selector GNOME shell extension

1. Install `chrome-gnome-shell`

   ```bash
   sudo apt install install chrome-gnome-shell
   ```

2. Navigate to https://extensions.gnome.org/extension/906/sound-output-device-chooser/
3. Click the toggle switch to install the extension

# Saturday, February 18, 2023

## Setting up pass

1. Install `pass` and `pass-extension-otp`

   ```bash
   sudo apt install pass pass-extension-otp
   ```

2. Download the GPG key from Proton Mail
3. Import the GPG key

   ```bash
   gpg --import <key>
   ```

4. Set up Git remote and clone the `password-store` repo

   ```bash
   pass git remote add gitlab git@gitlab.com:krzysztof.wos/password-store.git
   pass git pull -r gitlab master
   ```

# Friday, February 17, 2023

## Setting up AirPods Max on Ubuntu 22.04

Update `ControllerMode` in `/etc/bluetooth/main.conf` to `bredr` and restart bluetooth service with `sudo service bluetooth restart`. Then, use the Settings app to pair the AirPods Max.

# Wednesday, February 15, 2023

## Running ClickHouse server

```bash
docker run -d \
    --network=host \
    --name clickhouse-server \
    --ulimit nofile=262144:262144 \
    --volume /storage/clickhouse:/var/lib/clickhouse \
    --restart unless-stopped \
    clickhouse/clickhouse-server
```

### References

- https://hub.docker.com/r/bitnami/clickhouse
- https://hub.docker.com/r/clickhouse/clickhouse-server

# Sunday, February 12, 2023

## Configuring RAID 1 on Ubuntu 22.04

1. Create Physical Volumes

   ```bash
   sudo pvs
   ```

   ```text
   PV             VG       Fmt  Attr PSize    PFree
   /dev/nvme0n1p2 vgubuntu lvm2 a--  <931.01g    0
   ```

   ```bash
   sudo pvcreate /dev/sda
   ```

   ```text
   Physical volume "/dev/sda" successfully created.
   ```

   ```bash
   sudo pvcreate /dev/sdb
   ```

   ```text
   Physical volume "/dev/sdb" successfully created.
   ```

   ```bash
   sudo pvs
   ```

   ```text
   PV             VG       Fmt  Attr PSize    PFree
   /dev/nvme0n1p2 vgubuntu lvm2 a--  <931.01g     0
   /dev/sda                lvm2 ---    <1.82t <1.82t
   /dev/sdb                lvm2 ---    <1.82t <1.82t
   ```

2. Create a Volume Group `vgstorage`

   ```bash
   sudo vgs
   ```

   ```text
   VG       #PV #LV #SN Attr   VSize    VFree
   vgubuntu   1   2   0 wz--n- <931.01g    0
   ```

   ```bash
   sudo vgcreate vgstorage /dev/sda /dev/sdb
   ```

   ```text
   Volume group "vgstorage" successfully created
   ```

   ```bash
   sudo vgs
   ```

   ```text
   VG       #PV #LV #SN Attr   VSize    VFree
   vgstorage  2   0   0 wz--n-   <3.64t <3.64t
   vgubuntu   1   2   0 wz--n- <931.01g     0
   ```

3. Create a RAID 1 Logical Volume `storage`

   ```bash
   sudo lvs
   ```

   ```text
   LV     VG       Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
   root   vgubuntu -wi-ao---- 930.05g
   swap_1 vgubuntu -wi-ao---- 976.00m
   ```

   ```bash
   sudo lvcreate --type raid1 -m1 -l 100%FREE -n storage vgstorage
   ```

   ```text
   Logical volume "storage" created.
   ```

   ```bash
   sudo lvs
   ```

   ```text
   LV      VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
   storage vgstorage rwi-a-r---  <1.82t                                    3.66
   root    vgubuntu  -wi-ao---- 930.05g
   swap_1  vgubuntu  -wi-ao---- 976.00m
   ```

4. Use Disks app to format and mount the volume

### References

- https://www.server-world.info/en/note?os=Ubuntu_22.04&p=lvm
