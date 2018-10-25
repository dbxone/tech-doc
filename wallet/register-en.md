# Register an account
DBXChain used account model and registration referring mechanism, so to register an account on DBXChain, there are three key points:

* Referrer，which is the existed account on the chain and will register an account by your account name and public key for you
* Account name, which is unique on the chain, so please remember <b>`account name is the address`</b> on DBXChain.
* ECC public key，starting with DBX, ECC public key in Base64 code.

There are two methods to register an account:

## 1. Online wallet
Finish the registration steps in the online wallet page. When registering, the page will automatically call the faucet to intial the registration request.

## 2. Manual registration
It is recommended for developers who have high demand for the private key security to finish the registration by this method, ensuring the private key is offline.

### Step 1: Generate an encrypted key pair through cli_wallet

```
cli_wallet --suggest-brain-key
{
  "brain_priv_key": "SHAP CASCADE AIRLIKE WRINKLE CUNETTE FROWNY MISREAD MOIST HANDSET COLOVE EMOTION UNSPAN SEAWARD HAGGIS TEENTY NARRAS",
  "wif_priv_key": "5J2FpCq3UmvcodkCCofXSNvHYTodufbPajwpoEFAh2TJf27EuL3",
  "pub_key": "DBX75UwALPEFECfHLjHyNSxCk1j7XzSvApQiXKEbanWgr7yvXXbdG"
}
```

Field explanation

* brain_priv_key: Recovery phrase, which is the initial text of the private key, and able to recover the private key
* wif_priv_key: Private key, used in programs
* pub_key: Public key, used for account registration on the chain

### Step 2: Finish the account registration by faucet

Registration command is :

```
curl '<url>' -H 'Content-type: application/json' -H 'Accept: application/json’ -d ‘{“account”:{“name”:”<account_name>”,”owner_key”:”<public_key>”,”active_key”:”<public_key>”,”memo_key”:”<public_key>”,”refcode”:null,”referrer”:null}}’
```
account_name and public_key should be substituted to corresponding account name and public key. The private key is stored offline.
