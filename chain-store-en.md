## Colorful eggs on the chain
--------------------

Only support cli_wallet operation currently. Require cli_wallet has imported the private key of the account.

### 1. Start cli_wallet, connect to the node1 wallet accessing point in the main net

```
./programs/cli_wallet/cli_wallet -swss://node1.dbx.io -w wallet.json
```

Start successfully, the wallet is locked, it will print the following interactive reminding symbols：

```
locked>>>
```

### 2. Unlock the wallet

```
unlock "Password"
```

Thereinto, "Password" is a string which is the password of your local wallet  
Once unlocking successfullu, the interactive reminding symbol becomes:`unlocked >>>`

### 3. Using custom command, record self-defined data on the blockchain

Command line format is 

`custom account name 0 "Text" DBX false`

Thereinto, the account name refers to that of the imported wallet; 0 represents the serial number, which should be a positive integar; "Text" is a long string, which wil be recorded on the blockchain unchangedly; DBX means the bookkeeping commission is paid in DBX; false means only for the rehearsal without actual execution, otherwise change false to be true

For example, use b22 account, record some words on the blockchain：

```
custom b22 0 "\n鹅鹅鹅，\n曲项向天歌。\n白毛浮绿水，\n红掌拨清波。\n" DBX false
```

New line funtionality in the text use \n替换. The endpoint wil print：

```
unlocked >>> 
custom b22 0 "\n鹅鹅鹅，\n曲项向天歌。\n白毛浮绿水，\n红掌拨清波。\n" DBX false
unlocked >>> custom b22 0 "\n鹅鹅鹅，\n曲项向天歌。\n白毛浮绿水，\n红掌拨清波。\n" DBX false
3162718ms th_a       wallet.cpp:3761               custom               ] raw_data: 
鹅鹅鹅，
曲项向天歌。
白毛浮绿水，
红掌拨清波。
{
  "ref_block_num": 21160,
  "ref_block_prefix": 2495112407,
  "expiration": "2018-06-21T07:53:09",
  "operations": [[
      35,{
        "fee": {
          "amount": 2000,
          "asset_id": "1.3.1"
        },
        "payer": "1.2.466",
        "required_auths": [],
        "id": 0,
        "data": "0ae9b985e9b985e9b985efbc8c0ae69bb2e9a1b9e59091e5a4a9e6ad8ce380820ae799bde6af9be6b5aee7bbbfe6b0b4efbc8c0ae7baa2e68e8ce68ba8e6b885e6b3a2e380820a"
      }
    ]
  ],
  "extensions": [],
  "signatures": [
    "2006d3f54a8a480b83743da496bd038d87cfc46810784f74baf540eacfe786eb162f98993401eb39a349c30bd186ba5100fec65085769ed02dc1457edd2f2da477"
  ]
}
unlocked >>
```

Once recording successfully, it will return a series of stylized json string

### 4. Check on the blockchain surfer

Visit the blockchain surfer https://block.dbx.io/\#/
