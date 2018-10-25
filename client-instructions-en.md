# Client instruction

## Synchronization

When running full-node client, you need to wait until data of all blocks has been synchronized to execute any operation. Because there is lots of data, it might take some time to complete the synchronization.

## Phrase explanation

### Wallet

---

The wallet is used to store the asset issued on the chain. Meanwhile, the wallet is also the client of DBXChain decentralized exchange where you can find the real time transactions in the exchange and listed data type.

Wallet file：Wallet file（suffix is .bin）could be regarded as the key to the account, similar to your bank cards. You need to unlock your account by your wallet file and password. If your wallet file is broken or you forget your password, you are not able to unlock your wallet. **So please back up your wallet file and password carefully**.

### Account

---

As the carrier to store the asset issued on DBXChain, account is similar to your bank account.

1、Address：Asset account on DBXChain, which can be used for asset transferring and transaction on the chain.

2、Address type：//Address type instruction（Common account address, smart contract address）

3、Public key：It can be extrapolated from the private key, matching the only private key.

4、Private key：It is a random number with 256 digits, similar to your identification card, serving as the only proof of ownership and right of use of the asset in your account，unkown to the public. You can find your private key by clicking your public key in the client. **Please keep your private key safe**， once it is disclosed, the hacker could steal your account asset even without the wallet file and password.
5、Brain wallet：//Brain wallet

There are two methods to unlock the wallet：**1）Wallet file+Password**      ** 2）Private key**      Please keep these three elements safe, treating blockchain asset as seriously as you will do for the real asset

### Asset

---

The information of asset owned by the account, including：asset, type, balance, issuance qunatity, issuer, etc.

### Recent activity

---

Able to find the change of the asset of your account.

### Transfer

---

Transfer the asset of current account to other accounts.

### Charge

---

Transfer asset from other accounts to current account

### Material

---

Find account type and permission 

### Voting

---

DBX and DBX holder vote on the witness candidates, DBX holders could vote by themselves or entrust other accounts to vote standing for them. The witness nodes are determined by the ultimate voting result.（Witness application has not opened yet）.

## Wallet introduction

---

Thare two methods to use DBX：

1. Use webpage wallet；

2. Download the wallet client to use. There is no difference betweent the two methods, for common users, we recommend to use【Webpage wallet】.

### **Webpage wallet registration**

---

Enter [https://wallet.dbx.io](https://wallet.dbx.io) in your browser，open the webpage wallet, click【Creat account】 on the right side of the page

![](/assets/网页钱包.jpg)

Then, you are directed to the account creation page, set your wallet account name and password. Please note that the wallet account name should be combination of letters and numbers without any Chinese characters, the sample is as follows：

![](/assets/注册.jpg)

Please keep your wallet account name and password safe. DBX is developed based on BTS framework, the wallet account name is the address for transferring and receiving asset, so when you transfer to other wallets, do not be surprised when the transaction party provides you a series of code.

Please remember after creating the account successfully, keep your **Wallet file** and **Password** safe. If you forget your password also lose your private key, you are not able to manage asset in your wallet, which is similar to the occasion that asset in the wallet will be locked permanently in Bitcoin network if the private key of the Bitcoin address is lost.

### **Download and registration of the client wallet**

---

The downloading address of DBXChain client is：[https://www.dbx.io](https://www.dbx.io)，go to the page，scroll down the page to 【Download】page, select the corresponding client to download：

![](/assets/download.jpg)

1. Select the first icon for windows system：for 32 unit windows system or above, choose the upper client, for 64 unit windows system, choose the lower client

\*Baidu search “windows system type”, to know your windows system version

2. Select the second icon for OS X system 

Once the client is downloaded, the account registration method and procedure is the same as that of webpage wallet.

After finishing registrating the wallet, please refer to “How to back up DBX” for the next key step, for your asset security reason in your wallet, please read and operate carefully.

### **How to back up DBX**

---

After registrating the wallet, you will be directed to the wallet back up page, click 【Create（DEFAULT）wallet back up】

![](/assets/wallet backup 1.jpg)

![](/assets/wallet backup2.jpg)

After you click back up, it will generate the backup file belonging to your wallet, click 【Download】, save the wallet file properly.

![](/assets/wallet backup3.jpg)

Please do make several copies of the wallet backup files and save them separately, it is recommended in multiple USB disks. Similar to other cryptocurrency wallets, DBX can only be used in the computer where it is registered. When you want to open your wallet on other computers, it need to import wallet backup files or the private key again, please note: when importing the wallet back up, it needs the wallet password, so please keep your password safe.

PS：If you do not back up in time after registrating your account, you can click 【Need back up】 in the status colomun at the right corner in the bottom to back t up.

### **How to store the private key**

---

When emergencies that the client is delete, your computer is lost or damaged or you want to use the wallet on other computers, in addition to recovering by importing the wallet backup files again, you can also do it by 【Private key】 of the wallet. Thus, the private key is also needed to be kept safe. The storing method of the wallet private key is as follows：

1. First, click 【Account】 at the left side on the upper part of the wallet page, then click 【Permission】 at the left side on the lower part of the page，go to the permission page of the wallet, shown as follows：

![](/assets/get private key.jpg)

Then click the wallet public key right besides the key shaped icon，it will pop up the private key checking menu, then click 【Display】

![](/assets/private key1.jpg)

After entering the wallet password, it will show your wallet private key, please jot it down and store it separately and do not disclose it to others,

Anyone who knows your private key can control your account.

![](/assets/private key2.jpg)

### **How to recover and import your wallet**

---

Similar to other cryptocurrency wallets, DBX can only be used on the computer where it is registrated. You are not required to log in repeatedly when using DBX on one computer. If you need to use former wallet on other computers, or your wallet client was once deleted, you need to import wallet back up files or wallet private key again, the operating approach is as follows：

First, Open wallet, click 【Settings】 as a gear shaped icon at the upper right corner.

![](/assets/recover via PK.jpg)

Then click 【Recover\Import】 in the menu at the left side, there are three methods to import the wallet, here we only focus on importing by wallet backup and wallet private key.

![](/assets/PK2.jpg)

**The first method：Recover by the wallet backup file**

Select 【Recover from wallet backup（.bin）】 in the selection column, then select the wallet files you backed up before in the second column

![](/assets/PK3.jpg)

After importing the files, you are required to enter the password to finish the whole process.

![](/assets/PK4.jpg)

**The second method：Recover by the wallet private key**

It's no need to know your former wallet password if you choose to recover it by the private key, instead creating a new wallet and then import the information and asset of the original account to the new wallet, the operating approach is as follows：

Select 【Import private key】 in the selection column, then enter the password of the new wallet and reenter to confirm

![](/assets/PK5.jpg)

After entering the password, it means you create a new wallet, then go to the home page of the wallet, click the gear shaped icon at the upper right corner——click recover\import, then enter the private key of the wallet you want to import

![](/assets/PK6.jpg)

Next, click the 【Import private key】 button in green to finish the import so that the information and asset of the original wallet is imported to the new wallet.

### **Charge and withdrawal instruction**

---

**1.Withdrawing address instruction**

When others want to transfer or charge DBX to your wallet, your**Wallet account name ** is your wallet charging address, for example, in the following picture, the wallet account name is zhangsan113, which means zhangsan113 is also your wallet address.

![](/assets/transfer.jpg)

Withdrawing DBX from the trading platform has the same condition, fill in your wallet account name in the blockchain address area in the withdrawing menu of the exchange, taking the picture above as an example, the address filled in is：zhangsan113

Particular reminder：Similar to Bitcoin and other crypto assets, DBX is also decentralized and anonymous. When you withdraw to other accounts due to filling in a wrong address in the trading platform, no one could contact the account and return your crypto asset, so please check the address several times when you withdraw your asset.

**2.Transfer instruction**

1）.Transfer to others by your wallet

Go to your wallet account, click 【Account】 at the upper left corner to go to the account page, click 【Transfer】 in the leftside menu to start transferring

![](/assets/transfer2.jpg)

After you are in the transferring page, enter the receiver's wallet account (wallet address), transferring amount in DBX, attach realted instruction in【Memo】 if needed. The commission at the bottom will be calculated automatically based on the length of MEMO words，you don't need to set it artificially (Based on the final transfer information confirmation page)

![](/assets/transfer3.jpg)

After clicking send, you are required to enter your wallet password to unlock the wallet for transferring

![](/assets/transfer4.jpg)

Before the transfer is sent, it will show the completed transfer information for your confirmation, shown as follows：

![](/assets/transfer5.jpg)

After clicking send, the transfer will be processed soon, and there will be message emerging on the right side to remind you the transfer has been confirmed

![](/assets/transfer6.jpg)

2）.Charging DBX to the trading platform

Charging the trading platform by the wallet is the same as transferring to other accounts. The exchange wallet address could be found in the exchange.

The difference is，**You must fill in the MEMO which is given by the exchange，**MEMO is your own charging number on this platform. The platform will identify who charges crypto asset to it by this number. Thus keep in mind you must fill in the memo when you charge the platform and check if the information you enter is correct, otherwise your DBX asset could be charged to other accounts not refundable.

Based on the case above, if account zhangsan113 wants to charge 0.5DBX to the platform, the wallet transfer information should be entered as follows：

![](/assets/deposit.jpg)

![](/assets/deposit2.jpg)

## Premium functionality

### Issue asset

---

//Issue asset on DBXChain

### Distribute asset

---

//Allocate asset on the chain

### Voting

---

Vote for the witness candidates to elect out the witness

Voting functionality is needed to be updated（Not opened yet）

### Merchant verification

---

Apply to be a merchant, acquire the permission to trade your data in DBXChain data exchange.

Please refer to [DBXChain](/dbxui.md) for detailed methods.

### Loyalty plan

---

Loyalty plan, aiming to encourage DBX holders to hold DBX in the long term. Participants are required to lock certain amount of DBX for a stipulated period of time in their wallets. DBXChain will take some shares of bonus to reward the participants.

After DBX is transferred to the wallet, at DBX home page (Click “Account” in the top navigating column of the wallet to go back to the home page), click DBX column then click 【Join in loyalty plan】, shown as the following picture：![](/assets/loyalty.jpg)

After clicking 【Join in loyalty plan】, you are directed to the loyalty plan setting page.First, select the term you want to join in this plan, there are three avaiable terms which are 3 months, 9 months and 24 months. Different terms corresponds to different DBX reward ratio, please see the following picture：

1. Locking period and expiring reward ratio

| Locking period | Annualized profit |
| :---: | :---: |
| 3 months | 4% |
| 9 months | 6% |
| 24 months | 8% |

After determining the period, enter the DBX amount you want to lock in the 【Locking amount】, it will automatically calculate the rewarding DBX amount athe expiration date based on the amount you entered, shown as follows:

![](/assets/loyalty2.jpg) Aftering setting the period and locking amount, click the black button 【Join in loyalty plan】 to submit. You will receive a locking reminder——The amount joining in the loyalty plan will be locked and cannot be sold during the plan term.

![](/assets/loyalty3.jpg)**Once you confirm to join in the plan, no one has the permission to unlock and release the DBX amount in the plan no matter it is you or DBXChain project. Thus, before confirming to join in the loyalty plan, please carefully plan your budget.**

After clicking confirm to join in, you are required to enter your wallet password to finish the authorization to the locking operation.

If you want to check the status you are in the plan, you can click 【Balance to be unlocked】 at the lower left side to see the amount you put in the plan and the time period of your plan (shown in the following picture).

![](/assets/loyalty4.jpg)Up till now, the loyalty plan has been launched to the webpage wallet and new verison wallet client of DBXChain.

As to the newest version of the wallet client, after visiting DBXChain official website [www.dbx.io](/www.dbx.io) click 【Download wallet】 to download the new version wallet file, and reinstall to use (No need to delete the orginal client and import the wallet again).

\*When using the wallet, please back up wallet files and the private key, which is the core proof to show your ownership; what's more, when using webpage wallet, we strongly recommend users to access and use webpage wallet on their computers instead of cellphones, since the cellphone surfer is very easy to remove the wallet when it clears the caches，in which case you need to import wallet back up files or the private key again to continue using the wallet.
