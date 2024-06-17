# \#5. Deployment

## Create Deployment Scripts
Create a bash script named `deploy.sh` outside of the token project directory and copy the following into the file

```bash
PROGRAM_ID="<Your Token Project Name>"

snarkos developer deploy \
--private-key <PRIVATEKEY> \
--query https://api.explorer.aleo.org/v1 \
--priority-fee 0 \
"${PROGRAM_ID}.aleo" \
--path ./build/ \
--broadcast https://api.explorer.aleo.org/v1/testnet/transaction/broadcast
--network 1
```

You can also simply deploy the program using leo cli using the below command
```bash
 leo deploy --private-key <add your ptovatke key here>
```

## Request for test tokens from the faucet

Follow [this](https://www.leo.app/blog/aleo-faucet) guide from Leo Wallet.

**Definitely Recommend to install [Leo wallet](https://www.leo.app/) if you want to try out Aleo ecosystem!**

## Deploy

Once you get your token for your account, Run the deploy script if deploying through snarkOS:

```bash
bash ./deploy.sh
```

If you run into issues with deploying through leo cli or snarkOS cli, follow [this link](https://github.com/demox-labs/leo-wallet-demo) to deploy your Leo program using the interface by locally running the project.

## Test Mint and Transfer Function onchain

Mint Token
```bash
snarkos developer execute \
--broadcast https://api.explorer.aleo.org/v1/testnet/transaction/broadcast \
--private-key <PRIVATEKEY> \
--query https://api.explorer.aleo.org/v1 \
"${PROGRAM_ID}.aleo" mint 100u64
```

Transfer Token
```bash
snarkos developer execute \
--broadcast https://api.explorer.aleo.org/v1/testnet/transaction/broadcast \
--private-key <Private Key> \
--query https://api.explorer.aleo.org/v1 \
"${PROGRAM_ID}.aleo" transfer <recipient_address> 20u64 <token_record>
```
