# Desire-Masternode


Fast installation for Daemon Desire Coin in your VPS

If you have alredy installa swap file, please jump this passage

# Create your Swap file

fallocate -l 3000M /mnt/3000MB.swap

dd if=/dev/zero of=/mnt/3000MB.swap bs=1024 count=3072000

mkswap /mnt/3000MB.swap

swapon /mnt/3000MB.swap

chmod 600 /mnt/3000MB.swap

echo '/mnt/3000MB.swap  none  swap  sw 0  0' >> /etc/fstab

# Download your Desire Daemon

past this line in your vps

wget https://github.com/Simo190/Desire-Masternode/releases/download/Desire/Desire.zip

# Set the repository

Type in your vps and press enter:

apt-get update;apt-get upgrade -y;apt-get dist-upgrade -y;apt-get install nano htop git -y;apt-get install build-essential libtool autotools-dev automake pkg-config -y;apt-get install libssl-dev libevent-dev bsdmainutils software-properties-common -y;apt-get install libboost-all-dev -y;apt-get install libzmq3-dev libminiupnpc-dev libssl-dev libevent-dev -y;add-apt-repository ppa:bitcoin/bitcoin -y;apt-get update;apt-get install libdb4.8-dev libdb4.8++-dev -y;

# Install your Desire Daemon

Past in your vps this line

For open the port: ufw allow 9919/tcp

For unzip you daemon: unzip Desire.zip

For give the permission at your daemon:

chmod +x desire-cli

chmod +x desire-tx

chmod +x desired

For move you daemon in the correct folder

mv desire-cli usr/local/bin

mv desire-tx usr/local/bin

mv desired usr/local/bin

Now you can start your daemon type in your vps:

desired

Then press control+c. When the prompt come back type:

cd .desirecore

nano desire.conf (if you haven't use nano press 2)

Paste in your editor this line:

rpcuser=user

rpcpassword=pass

rpcallowip=127.0.0.1

listen=1

server=1

daemon=1

rpcport=9918

staking=0

externalip=IP:9919

masternode=1

masternodeprivkey=yourprivkey

Replasce user and pass (don't need to remember it)
Replace IP with your IP Address
Replace yourprivkey (see Side wallet)
For exit control+x, save and exit

Now you can start the daemon in your vps:

desired -daemon

For check if the sync is going type

desire-cli getblockcount

If the sync don't start try to add a node (you can find it in your peer list in your wallet)

Type in your vps: desire-cli addnode IPaddress onetry

# Side wallet

Go to your local computer where your main wallet is running with all your coins inside.

On menu, Go to FILE -> RECEIVING ADDRESSES -> click NEW and put your Label (alias), we are using "MN1" on this tutorial. Feel free to choice or use the same.

Then copy the address and send EXACTLY 1000 DSR to this address, you will be just send a payment to yourself.
Wait for 15 confirmations, then go to the debug console and use this command:

masternode outputs

You should see one line corresponding to the transaction id (tx_id) of your 1000 coins with a digit identifier (digit). Save these two strings in a text file.

Note that if you get more than 1 line, it’s because you made multiple 1000 coins transactions, with the tx_id and digit associated.

Now we have to create the masternode private key to link the main wallet and the VPS masternode. Type in the debug console :

masternode genkey

Copy this key somewhere. It will be referred as yourprivkey.

Next, you have to go to the data directory of your main wallet (in Linux it’s located at /home/user/.desirecore) or you can open it by wallet GUI by Tools - Open masternode configuration file. So type :

MN1 IP:9919 masternodeprivkey tx_id digit

Put your data correctly, save it and close. Restart your main wallet.

Note that each line of the masternode.conf file corresponds to one masternode.

Then wait almost 15 confirmation for your collateral transaction, then you can start your vps with start alias right button.

