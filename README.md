# Twiсy
![logo](_README/logo.png)
* First risk-game on Free TON
* 100% on smart-contracts

## Address
```sh
0:05f6a489d8df02f44707a7d7cf04e9b75c050fdb0b7a1f175a55144daf1f53e0
```
* [ton.live](https://ton.live/accounts/accountDetails?id=0%05f6a489d8df02f44707a7d7cf04e9b75c050fdb0b7a1f175a55144daf1f53e0)


## How to play
![How to play x2](_README/how-to-play-x2.png)
* Send 10💎 to smart-contract
  * If you use [Surf](https://ton.surf/) on mobile use this link [ton://transfer/0:05f6a489d8df02f44707a7d7cf04e9b75c050fdb0b7a1f175a55144daf1f53e0?amount=10000000000](ton://transfer/0:05f6a489d8df02f44707a7d7cf04e9b75c050fdb0b7a1f175a55144daf1f53e0?amount=10000000000). If link not clickable then sorry. Github parser has not yet learned how to make links for the Free TON
  * More than 10💎 and less than 10💎 are not acceptable
* Get an answer and wait your turn
* Get 20💎

## Economics
![Diagramm](_README/diagramm.png)
* **95%** - 9💎 from every 10💎 - payouts to participants
* **5%** - 0.5💎 from every 10💎 - developers reward and fee for smart-contracts
 
## How it works
![Rules](_README/rules.png)
Participants receive payments in turn
 
 
## Security
![Security](_README/security.png)
* **No setcode().** Nobody can change the contract
* **No selfdestruct().** Nobody can destroy the contract
* **No setters.** Nobody can change parameters of contract
* **Doesn't store many crystals.** Nobody can steal all crystals

## Responsibility game
![Responsibility game](_README/responsibility-game.png)
* Don't play on last money
* Don't take credits to play
* Play at own risk
* It's just fun

## Tech
### Structure
![Smart-contracts](_README/smart-contracts.png)
* **User** - user wallet
* **Twicy** - main contract. Collects crystals and pays out rewards
* **TwicyStorage** - Deployed by main contract. It stores information about deposits

### Call stacks
#### Deposit
```
Twicy.deposit()
  _depositWithoutReferralBonus()
    _deposit()
      _depositConfirmation()
        → 0.001💎 to USER
      _save()
        → 0.2💎 to TwicyStorage.save()
      _dispatchDepositsForPayout()
        → 0.2💎 to TwicyStorage.dispatchDepositsForPayout()
          → +0.1💎 to Twicy.onReceiveDepositsForPayout()
            → reward 💎 to USER
```


### Deploy
#### 1. Compile TwicyStorage
```sh
solc TwicyStorage.sol
tvm_linker compile TwicyStorage.code -o TwicyStorage.tvc
tvm_linker decode --tvc TwicyStorage.tvc > code.txt
```

#### 2. Copy code from code.txt
```text
te6ccgECMQEACEYAAib/APSk ... 84AHwAfhHbpMw8jze
```

#### 3. Compile Twicy
```sh
solc Twicy.sol
tvm_linker compile Twicy.code -o Twicy.tvc
tonos-cli genaddr Twicy.tvc Twicy.abi.json --genkey Twicy.keys.json
```

#### 4. Send minimum 3💎 on generated address and deploy
```sh
tonos-cli deploy Twicy.tvc '{"storageCode": "te6ccgECMQEACEYAAib/APSk ... 84AHwAfhHbpMw8jze","storageLength": 20000}' --abi Twicy.abi.json --sign Twicy.keys.json
```

### Deployment tools
Solc from [TON Solidity Compiler](https://github.com/tonlabs/TON-Solidity-Compiler)
```
solc, the solidity compiler commandline interface
Version: 0.6.3-develop.2020.12.13+commit.54c8a5a1.mod.Linux.g++
```

[TVM linker](https://github.com/tonlabs/TVM-linker)
```
TVM linker 0.1.0
COMMIT_ID: 2e15070e458637add2ecb279a03bd88d8df37bde
BUILD_DATE: 2020-12-13 03:25:46 +0300
COMMIT_DATE: 2020-11-20 10:57:07 +0300
GIT_BRANCH: master
```

[tonos-cli](https://github.com/tonlabs/tonos-cli)
```
tonos_cli 0.1.28
COMMIT_ID: a389881108384118ba1a565a0450762fdabeb705
BUILD_DATE: 2020-12-13 03:41:14 +0300
COMMIT_DATE: 2020-11-30 17:42:19 +0300
GIT_BRANCH: master
```

### Migration
[Migration from v1.0.0 to 1.1.0](MIGRATION.md)

## Telegram
[@freeton_twicy](https://t.me/freeton_twicy)
