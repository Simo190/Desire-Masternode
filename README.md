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

