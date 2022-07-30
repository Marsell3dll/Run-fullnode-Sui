# Run-fullnode-Sui

## Guide compiled from an official source [Run a Sui Fullnode](https://docs.sui.io/build/fullnode#configuring-your-fullnode)

[<img width="200" alt="665875" src="https://user-images.githubusercontent.com/93165931/181920110-c9385bd6-5d22-4fa9-98e2-c37e2d282fda.png">
](https://docs.sui.io/)


### Set up your fork of the Sui repository:
Go to the [Sui repository](https://github.com/MystenLabs/sui) on GitHub and click the Fork button in the top right-hand corner of the screen.
Clone your personal fork of the Sui repository to your local machine (ensure that you insert your GitHub username into the URL):

![image](https://user-images.githubusercontent.com/93165931/181919813-c046e1e9-8f2b-48a4-a750-f729e58cd8b0.png)



### And copy this command. The only thing you need to change is to put your `login from GitHub instead` of *`<YOUR_GITHUB_USERNAME>`*:
```
git clone https://github.com/<YOUR_GITHUB_USERNAME>/sui.git
```
>For example:
>>`git clone https://github.com/StakeTake/sui.git`

### Go to directory ***Sui:***

```
cd sui
```

### Set up the Sui repository as a git remote:

```
git remote add upstream https://github.com
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

### Make a copy of the configuration file

```
cp crates/sui-config/data/fullnode-template.yaml fullnode.yaml
```

### Download the latest genesis state for Devnet by clicking that link or by running the following in your terminal:

```
curl -fLJO https://github.com/MystenLabs/sui-genesis/raw/main/devnet/genesis.blob
```
![image](https://user-images.githubusercontent.com/93165931/181920727-15dde3ca-398b-4d13-bec6-13dd6d37c5c4.png)


>### Optional: You can skip this set of steps if you are willing to accept the default paths to resources. If you need custom paths, edit your fullnode.yaml file to reflect the paths you employ:
Update the db-path field with the path to where the fullnode's database will be located. By default this will create the database in a directory ./suidb relative to your current directory:

```
db-path: "/path/to/suidb"
```
>>### You can do this with Midnight Commander
```
mc
```
>>>Find the file and `press f4` then edit the data and `press f2` and `Enter`:
![image](https://user-images.githubusercontent.com/93165931/181921557-e53b6a7c-5971-4b3c-a598-9970cb9f6cd3.png)

### Start your Sui fullnode:

```
cargo run --release --bin sui-node -- --config-path fullnode.yaml
```

### Post [build](https://discord.com/channels/916379725201563759/986662676073709568), receive the success confirmation message, SuiNode started!

### You can check the operation of the node in the explorer: 
- [Sui Explorer](https://explorer.devnet.sui.io/)
- [SUITESTER](https://node.sui.zvalid.com/)





