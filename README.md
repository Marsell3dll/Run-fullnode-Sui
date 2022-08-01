# Run-fullnode-Sui

[<img width="200" alt="665875" src="https://user-images.githubusercontent.com/93165931/181920110-c9385bd6-5d22-4fa9-98e2-c37e2d282fda.png">
](https://docs.sui.io/)

### Copy and past this software components installation:

```
rm -rf /var/sui/db /var/sui/genesis.blob $HOME/sui
git clone https://github.com/MystenLabs/sui.git
mkdir /var/sui/db 
cd /root/sui
```

### Set up the Sui repository as a git remote:

```
git remote add upstream https://github.com/MystenLabs/sui


```


### Installing plugins

```
sudo apt update && sudo apt install curl -y < "/dev/null"\
    apt-get update \
    && DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install -y --no-install-recommends \
    tzdata \
    git \
    ca-certificates \
    curl \
    build-essential \
    libssl-dev \
    pkg-config \
    libclang-dev \
    cmake\
sudo curl https://sh.rustup.rs -sSf | sh -s -- -y\
source $HOME/.cargo/env
\
sudo curl https://sh.rustup.rs -sSf | sh -s -- -y\
source $HOME/.cargo/env


```
### Sync your fork:

```
git fetch upstream


```

![image](https://user-images.githubusercontent.com/93165931/181920404-5a8396c4-190f-47c9-b894-f5fff979b837.png)

### Check out the devnet branch:

```
git checkout --track upstream/devnet


```
![image](https://user-images.githubusercontent.com/93165931/181920496-ae8df11c-2213-457e-9869-facb8b8ce224.png)

### Make a copy and edit of the configuration file:

```
cp crates/sui-config/data/fullnode-template.yaml fullnode.yaml
sed -i.bak "s/db-path:.*/db-path: \"\/var\/sui\/db\"/ ; s/genesis-file-location:.*/genesis-file-location: \"\/var\/sui\/genesis.blob\"/" /var/sui/fullnode.yaml

```

### Download the latest genesis state for Devnet by clicking that link or by running the following in your terminal:

```
curl -fLJO https://github.com/MystenLabs/sui-genesis/raw/main/devnet/genesis.blob


```
![image](https://user-images.githubusercontent.com/93165931/181920727-15dde3ca-398b-4d13-bec6-13dd6d37c5c4.png)

### Create and save a service file:

```
echo "[Unit]
Description=Sui Node
After=network.target

[Service]
User=$USER
Type=simple
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target" > $HOME/suid.service

mv $HOME/suid.service /etc/systemd/system/
sudo tee <<EOF >/dev/null /etc/systemd/journald.conf
Storage=persistent
EOF


```
### Restart Node:

```
sudo systemctl daemon-reload
sudo systemctl enable suid
sudo systemctl restart suid


```

### Start your Sui fullnode:

```
cargo run --release --bin sui-node -- --config-path fullnode.yaml
```

### Post [build](https://discord.com/channels/916379725201563759/986662676073709568), receive the success confirmation message, SuiNode started!

### You can check the operation of the node in the explorer: 
- [Sui Explorer](https://explorer.devnet.sui.io/)
- [SUITESTER](https://node.sui.zvalid.com/)





