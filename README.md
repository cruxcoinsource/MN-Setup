![Example-Logo](https://i.imgur.com/BmBO5tc.jpg)
# Crux Coin Linux VPS Masternode Setup Guide (Ubuntu 16.04)
This guide will assist you in setting up a Crux Masternode on a Linux Server running Ubuntu 16.04. 

***
## Requirements
1) **2500 (CUX) Crux coins.**
2) **A Vultr VPS running Linux Ubuntu 16.04.**
3) **A Windows local wallet.**
4) **A SSH client such as [Putty](https://the.earth.li/~sgtatham/putty/latest/w32/putty-0.70-installer.msi)**
***
## Contents
* **Section A**: Creating the VPS within [Vultr](https://www.vultr.com).
* **Section B**: Preparing the local wallet.
* **Section C**: Connecting to the VPS and setting up the MN via Putty.
* **Section D**: Connecting & Starting the masternode.
***


## Section A: Creating the VPS within [Vultr](https://www.vultr.com/?ref=7296974) 
***Step 1***
* Register at [Vultr](https://www.vultr.com/?ref=7296974)
***

***Step 2***
* After you have added funds to your account go [here](https://my.vultr.com/deploy/) to create your Server
***

***Step 3*** 
* Choose a server location (preferably somewhere close to you)
![Example-Location](https://i.imgur.com/ozi7Bkr.png)
***

***Step 4***
* Choose a server type: Ubuntu 16.04
![Example-OS](https://i.imgur.com/aSMqHUK.png)
***

***Step 5***
* Choose a server size: $5/mo will be fine 
![Example-OS](https://i.imgur.com/UoGoHcM.png)
***

***Step 6***
* Click "Deploy now"

![Example-Deploy](https://i.imgur.com/4qpYuH0.png)
***


## Section B: Preparing the Local wallet

***Step 1***
* Download and install the Crux Windows wallet [here](https://www.cruxcoin.io/)
***

***step 2***
* Go to the console within the wallet 

![Example-console](https://i.imgur.com/JN1LokE.png)
***

***Step 3***
* Type the command below and press enter 

```linux
masternode genkey
```

* Save this information to somewhere else. We'll be using this key code at multiple places. 
***

***Step 4***
* Type the command below and press enter 

```linux
getaccountaddress mn1
```

* This code will generate a new CUX address for your masternode. Copy this address and send exactly "2500 CUX" to this address.
* ***Double check the address that you’ll send. We can not do anything by mistaken transactions.***
***

***Step 5***
* Type the command below and press enter 

```linux
masternode outputs
```

* Save this informations to somewhere else. We'll be using this key code at setting up our local masternode config file. 
***

***Step 5***
* Navigate to this folder from your local Windows computer. 

> C:\Users\%username%\AppData\Roaming\CruxCoin

* Find "***masternode.conf***" and add following line into it. 
***

* Sample pattern

```linux
<Name of Masternode("mn1" at our example at step 4)> <Unique IP address(Section A)>:29118 <The result of Step 3> <Result of Step 5> <The number after the long line in Step 5>
```

* For instance

```linux
Mn1 209.250.252.98:29118 892WPpkqbr7sr6Si4fdsfssjjapuFzAXwETCrpPJubnrmU6aKzh c8f4965ea57a68d0 e6dd384324dfd28cfbe0c801015b973e7331db8ce018716999 1
```

* Substitute it with your own values and without the “<>”s



## Section C: Connecting to the VPS & Installing the MN script via Putty.

***Step 1***
* Copy your VPS IP (you can find this by going to the server tab within Vultr and clicking on your server. 
![Example-Vultr](https://i.imgur.com/GeaXJ4L.png)
***

***Step 2***
* Open the Putty application and fill in the "Hostname" box with the IP of your VPS.
![Example-PuttyInstaller](https://i.imgur.com/7cWUGKA.png)
***

***Step 3***
* Copy the root password from the VULTR server page.
![Example-RootPass](https://i.imgur.com/SVfas5y.png)
***

***Step 5***
* Write "root" to "Login as" section and press "Enter"
* Press "Shift + Insert" to insert your copied password into password section.
* Your password wont be seen as any characters but don't worry just press "Enter" after you insert your password
![Example-RootPass](https://i.imgur.com/8LG2ufk.png)

***Step 6***
* When you login to your VPS via Putty you'll see screen like this.
![Example-RootPass](https://i.imgur.com/rxb5PWh.png)

* Now we set our Masternode into VPS
***

***Step 7***
* Follow this lines by copying from here and inserting into your Putty VPS client by pressing "Shift + Insert"

* 1) Navigate to home directory at Linux VPS

```linux
cd ~
```

* 2) Download latest CruxCoinwallet from GitHub

```linux
wget https://github.com/cruxcoinsource/MN-Setup/raw/master/cruxlinux.tar.gz
```

* 3) Unzip and extract

```linux
tar -zxvf cruxlinux.tar.gz
```

* 4) Navigate to CruxCoinwallet file’s location

```linux
cd cruxlinux
```

* 5) Start wallet for first time on VPS. It is necessarry to autocreate config files

```linux
./cruxcoind
```

* 6) Exit wallet to continue by pressing CTRL + C (Send kill command for running process)

***

***Step 7***
* Now on the VPS, find to configure Conf. File in the CruxCoin data directory 

* 1) Navigate to CruxCoin data directory.
```linux
cd /root/.cruxcoin
```

* 2) Open the cruxcoin.conf by typing
```linux
vi cruxcoin.conf
```

* 3) then press "i" to go into insert mode and make the config look like this:
```linux
rpcuser=long random username
rpcpassword=longer random password
rpcallowip=127.0.0.1
server=1
daemon=1
logtimestamps=1
maxconnections=256
masternode=1
externalip=Result of SECTION C > Step 1
masternodeprivkey=Result of SECTION B > Step 3
```
* Make sure to replace rpcuser and rpcpassword with your own.

* to exit the editor press "ESC" then write

```linux
:wq!
```

* then press enter.

***

***Step 7***
* We set our masternode deamon on VPS and we're ready to start it. 

* 1) To Start the daemon client in the VPS, navigate to your linux wallet directory
```linux
cd ~/cruxlinux
```

* 2) then start wallet with writing
```linux
./cruxcoind
```


# Section D: Connecting & Starting the masternode 

***Step 1***
* Open your Windows wallet and go to Masternodes tab within the wallet. Select your masternode on list and click "Start Alias" button.
![Example-create](https://i.imgur.com/IjEQAJk.jpg)

* It will prompt you to confirm to start masternode. Click "Yes" to confirm that you want to start.
![Example-create](https://i.imgur.com/zfmQTkU.jpg)

* And it'll start right after.
![Example-create](https://i.imgur.com/zb7gfmT.jpg)
***

***Step 2***

* Back in the VPS wallet (Putty), start the masternode
```linux
./cruxcoin-cli startmasternode local false
```
* A message `masternode successfully started` should appear.
***
# Congratz! Your masternode has been set up and ready to go.
* ***Now the masternode setup is complete, you are safe to remove “enablezeromint=0” from the cruxcoin.conf
file of the control wallet.***

* To check your masternode's status. Write to your VPS wallet  (Putty);
```linux
./cruxcoin-cli masternode status
```
* You should see something like:
```linux
{
  “txhash” : “334545645643534534324238908f36ff4456454dfffff51311”,
  “outputidx” : 0,
  “netaddr” : “45.11.111.111:51472”,
  “addr” : “D6fujc45645645445645R7TiCwexx1LA1”,
  “status” : 4,
  “message” : “Masternode successfully started”
}
```

# Important Notice
* If your VPS masternode doesn't start with errors, give it some time to your coins get maturity, or your linux wallet might be still processing of sync.
