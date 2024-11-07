# 🚀 Hemi-Miner Setup Guide

Welcome to the **Hemi-Miner** setup guide! Whether you're new to mining or experienced, follow these steps to get started with Hemi-Miner quickly and smoothly.

---

## 📋 Step 1: Preparing Your System

First, let’s get all the necessary tools installed:

```bash
sudo apt-get update && sudo apt-get install -y wget tar nano screen curl jq
🧹 Step 2: Check for Previous Installations
If you've previously installed Hemi-Miner, stop any running instances first to avoid conflicts.

List existing screens to check for active Hemi screens:

bash
Copy code
screen -ls
Close any active Hemi screen (if present):

bash
Copy code
screen -XS hemi quit
Backup your old wallet file (if you have one):

bash
Copy code
cp /root/popm-address.json /root/popm-address_backup.json
💾 Step 3: Download and Extract Hemi-Miner
Download the Hemi binary:

bash
Copy code
wget https://github.com/hemilabs/heminetwork/releases/download/v0.4.5/heminetwork_v0.4.5_linux_amd64.tar.gz
Create a new directory for Hemi:

bash
Copy code
mkdir hemi
Extract the downloaded file into the hemi directory:

bash
Copy code
tar --strip-components=1 -xzvf heminetwork_v0.4.5_linux_amd64.tar.gz -C hemi
Navigate to the Hemi directory:

bash
Copy code
cd hemi
🔑 Step 4: Generate a New Wallet
If you don’t have a wallet yet or are setting up Hemi-Miner for the first time, you’ll need to create one.

Generate a new wallet:

bash
Copy code
./keygen -secp256k1 -json -net="testnet" > ~/popm-address.json
View your wallet address to confirm it was created successfully:

bash
Copy code
cat ~/popm-address.json
🌐 Step 5: Set Up Environment Variables
Replace yourpk with your private key and set up the required environment variables:

bash
Copy code
export POPM_BTC_PRIVKEY=yourpk
export POPM_STATIC_FEE=400
export POPM_BFG_URL=wss://testnet.rpc.hemi.network/v1/ws/public
🖥️ Step 6: Run Hemi-Miner in a New Screen
To keep Hemi-Miner running independently, start it in a new screen.

Create a new screen for Hemi-Miner:

bash
Copy code
screen -S Hemi-Miner
Start the Hemi-Miner:

bash
Copy code
./popmd
Detach from the screen without stopping the miner:

Press Ctrl + A, then D.
To reconnect to the Hemi-Miner screen:

bash
Copy code
screen -r Hemi-Miner
🔄 Step 7: Install and Run the Fee Updater (Optional but Recommended)
Running the fee updater keeps mining fees up-to-date. This step is optional but can help improve mining efficiency.

Create a new screen for the fee updater:

bash
Copy code
screen -S hemi-fee-updater
Run the fee updater script:

bash
Copy code
[ -f "hemifee.sh" ] && rm hemifee.sh; curl -sSL -o hemifee.sh https://raw.githubusercontent.com/zunxbt/pop-mining/refs/heads/main/hemifee.sh && chmod +x hemifee.sh && ./hemifee.sh
Detach from the screen:

Press Ctrl + A, then D.
📊 Step 8: Verify Miner Status
To ensure that everything is running as expected, check the miner's status.

View miner logs:

bash
Copy code
sudo journalctl -u hemi.service -f -n 50
Exit the log view by pressing Ctrl + C.

📌 Note
Always back up sensitive files like popm-address.json. Follow the instructions carefully, and happy mining! 💪
