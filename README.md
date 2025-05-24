Tutorial - Install a mining pool on Ubuntu Server 22.04
Install a mining pool on Ubuntu Server 22.04 with the following tutorial.

Update your Ubuntu server with the following command:

sudo apt-get update && sudo apt-get upgrade -y

Install the dependencies with the following command:

sudo apt-get install unzip redis-server npm git nano cmake screen -y

Download the Linux daemon for your wallet with the following command:

wget "https://dl.walletbuilders.com/download?customer=b99a53a3f81f1bbb2049773ab7e188c73b503cc19256b64eb5&filename=kingpepe-daemon-linux.tar.gz" -O kingpepe-daemon-linux.tar.gz

Extract the tar file with the following command:

tar -xzvf kingpepe-daemon-linux.tar.gz

Download the Linux tools for your wallet with the following command:

wget "https://dl.walletbuilders.com/download?customer=b99a53a3f81f1bbb2049773ab7e188c73b503cc19256b64eb5&filename=kingpepe-qt-linux.tar.gz" -O kingpepe-qt-linux.tar.gz

Extract the tar file with the following command:

tar -xzvf kingpepe-qt-linux.tar.gz

Type the following command to install the daemon and tools for your wallet:

sudo mv kingpeped kingpepe-cli kingpepe-tx /usr/bin/

Type the following command to open your home directory:

cd $HOME

Create the data directory for your coin with the following command:

mkdir $HOME/.kingpepe

Open nano.

nano $HOME/.kingpepe/kingpepe.conf -t

Paste the following into nano.

rpcuser=rpc_kingpepe

rpcpassword=dR2oBQ3K1zYMZQtJFZeAerhWxaJ5Lqeq9J2

rpcbind=127.0.0.1

rpcallowip=127.0.0.1

listen=1

server=1

txindex=1

daemon=1

paytxfee=0.0002

deprecatedrpc=accounts

addresstype=legacy

addnode=http://85.237.211.140:22093

Save the file with the keyboard shortcut ctrl + x.

Type the following command to start your daemon:

kingpeped

Type the following command to create a wallet for your daemon:

kingpepe-cli createwallet ""

Type the following command to create a new receiving address for your daemon:

kingpepe-cli getnewaddress ""

Example output.

4UyrFQrAoNQMEMqNhZTareRmjeU68bLiop

Type the following commands to install NOMP:

git clone https://github.com/walletbuilders/node-open-mining-portal.git nomp
cd nomp
npm update

Type the following command to create the file settings.json:

cp config_example.json config.json

Open nano.

nano config.json -t

Modify the following values in the file config.json.

host - Change the value “0.0.0.0” with the IPv4 address of your server.

stratumHost - Change the value “cryppit.com” with the IPv4 address of your server.

Save the file with the keyboard shortcut ctrl + x.

Type the following commands to create the config file for your coin:

cd coins
cp bitcoin.json kingpepe.json

Open nano.

nano kingpepe.json -t

Modify the following values in the file kingpepe.json.

name - “Bitcoin” -> “KingPepe”.

symbol - “BTC” -> “KPEPE”.

Save the file with the keyboard shortcut ctrl + x.

Type the following commands to create the config file for your pool:

cd ../pool_configs
cp litecoin_example.json kingpepe_pool.json

Open nano.

nano kingpepe_pool.json -t

Modify the following values in the file kingpepe.json.

enabled - “false” -> “true”.

coin - “litecoin.json” -> “kingpepe.json”.

address - “n4jSe18kZMCdGcZqaYprShXW6EH1wivUK1” -> Enter the receiving address from the RPC command “getaccountaddress ""”.

rewardRecipients - Remove all recipients.

minimumPayment - “70” -> “0.01”.

"paymentProcessing" -> port - “19332” -> “22093”.

"paymentProcessing" -> user - “testuser” -> “rpc_kingpepe”.

"paymentProcessing" -> password - “testpass” -> “dR2oBQ3K1zYMZQtJFZeAerhWxaJ5Lqeq9J2”.

"daemons" -> port - “19332” -> “22093”.

"daemons" -> user - “testuser” -> “rpc_kingpepe”.

"daemons" -> password - “testpass” -> “dR2oBQ3K1zYMZQtJFZeAerhWxaJ5Lqeq9J2”.

p2p - “true” -> “false”.

Save the file with the keyboard shortcut ctrl + x.

Type the following command to open a screen session:

screen

Type the following commands to start your mining pool:

cd $HOME/nomp
sudo node init.js

Press the keyboard shortcut ctrl + a + d to disconnect from your screen session.


Instructions to mine with your mining pool.

Open your wallet.

Go to Tools -> Console.
This is the console where you execute RPC commands.

Type the following command, to create a legacy receiving address for your miner:

getnewaddress "" "legacy"

Example output.

4UyrFQrAoNQMEMqNhZTareRmjeU68bLiop

Click here to download cpuminer and extract the zip file.

Open "Run" with the keyboard shortcut winkey + r.

Enter the following text behind "Open": notepad

Press on the button "OK".

Modify the following values in the following text.

minerd -a sha256d -o stratum+tcp://203.0.113.53:3008 -u 4UyrFQrAoNQMEMqNhZTareRmjeU68bLiop -p anything

203.0.113.53 - “203.0.113.53” -> IPv4 address of your VPS.

4UyrFQrAoNQMEMqNhZTareRmjeU68bLiop - “TP56yqPtRTkse49B96sHzo2B6v48MV24vP” -> Receiving address from the RPC command “getnewaddress” for your miner.

Paste the modified text into notepad.

Click on the menu item "File" -> "Save As...".

The Open dialog box will appear, click on "Save as type" and select the option "All Files (*.*)".

Enter the following text behind "File name": mine.bat

Click on the menu bar, open the directory where you extracted pooler-cpuminer-2.5.0-win64.zip and press on the enter key. enter

Press on the button "Save".

Execute mine.bat to mine with your mining pool.
