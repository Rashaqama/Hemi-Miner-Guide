🚀 Hemi-Miner Setup Guide
Welcome to the Hemi-Miner setup guide! If you're new to mining, don't worry – follow these steps, and you'll be mining in no time. This guide combines all the essentials into a straightforward path to get you started quickly.

📋 Step 1: Preparing Your System
First, let’s get all the necessary tools installed.

bash
Copy code
sudo apt-get update && sudo apt-get install -y wget tar nano screen curl jq
🧹 Step 2: Check for Previous Installations
If you have any old versions of Hemi-Miner running, stop them first to avoid conflicts.

List existing screens to check for any active Hemi screens:

bash
Copy code
screen -ls
Close the active Hemi screen (if any):

bash
Copy code
screen -XS hemi quit
Backup your old wallet file (just in case):

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
Extract the file into the hemi directory:

bash
Copy code
tar --strip-components=1 -xzvf heminetwork_v0.4.5_linux_amd64.tar.gz -C hemi
Navigate to the Hemi directory:

bash
Copy code
cd hemi
🔑 Step 4: Generate a New Wallet
If you don’t have a wallet yet or this is your first time setting up Hemi-Miner, you’ll need a new one.

Generate a new wallet:

bash
Copy code
./keygen -secp256k1 -json -net="testnet" > ~/popm-address.json
View your wallet address to confirm it was created:

bash
Copy code
cat ~/popm-address.json
🌐 Step 5: Set Up Environment Variables
Set up the required environment variables. Replace yourpk with your private key.

bash
Copy code
export POPM_BTC_PRIVKEY=yourpk
export POPM_STATIC_FEE=400
export POPM_BFG_URL=wss://testnet.rpc.hemi.network/v1/ws/public
🖥️ Step 6: Run Hemi-Miner in a New Screen
Running Hemi-Miner in a screen allows it to run independently, even if you disconnect.

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
Keeping fees updated is essential for effective mining. Run the following commands in a separate screen.

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
To make sure everything is running smoothly, check the miner's status.

View miner logs:

bash
Copy code
sudo journalctl -u hemi.service -f -n 50
Exit the log view by pressing Ctrl + C.

📌 Note:
Always back up sensitive files like popm-address.json. Happy mining! 💪
