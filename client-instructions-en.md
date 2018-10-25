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

2.下载钱包客户端后使用。两者在使用上没有差别，对于一般用户，我们推荐使用【网页版钱包】。

### **网页版钱包的注册**

---

在浏览器中输入[https://wallet.dbx.io](https://wallet.dbx.io)，打开网页版钱包，点击页面右侧的【创建账户】

![](/assets/网页钱包.jpg)

然后，你将来到账户创建页面，设置你钱包的账户名和密码。注意，钱包账户名需为字母+数字的组合，不可设置为中文，样式如下：

![](/assets/注册.jpg)

请务必妥善保管你的钱包账户名和密码。DBX基于BTS的架构开发，钱包账户名就是转账和收款的地址，当你给其他钱包转账时，发现对方提供不是一长串乱码，不必奇怪。

注意，账户创建成功后，请务必保管好你的**钱包文件**和**密码**。如果你的密码丢失或忘记，而你又没有保存好私钥，你将无法对你的钱包资产进行管理，就像丢失了比特币地址的私钥一样，钱包内的资产将被永久锁死。

### **客户端钱包的下载和注册**

---

DBXChain客户端的下载地址是：[https://www.dbx.io](https://www.dbx.io)，进入页面，下滑网页到【下载】页面，选择对应的客户端进行下载：

![](/assets/download.jpg)

1.windows系统选择第一个图标：32位windows系统的选择上方客户端，64位windows系统的选择下方客户端

\*可百度“如何查看windows系统类型”，了解自己的windows系统版本

2.OS X系统选择第二个图标。

客户端下载完成后，账户注册方法和流程与网页版钱包一致。

完成钱包注册后，接下来是最关键的一步，请见“如何备份DBX”，事关钱包中的资产安全，务必仔细阅读和操作。

### **如何备份DBX**

---

完成钱包注册后，会进入钱包备份页面，点击【为钱包（DEFAULT）创建备份】

![](/assets/wallet backup 1.jpg)

![](/assets/wallet backup2.jpg)

点击备份后，会生成属于你钱包的备份文件，点击【下载】，将钱包文件保存好。

![](/assets/wallet backup3.jpg)

钱包备份文件务必复制多份，分开保存，建议保存在多个U盘中。与其他数字资产钱包一样，DBX只能在注册所在的电脑上使用，在其他电脑需要打开你的钱包时，需要重新导入钱包备份文件或私钥方可使用，注意：在导入钱包备份时，是需要用到钱包密码的，密码务必保存记录好。

PS：如果注册账号后没有及时备份，可点击右下角状态栏的【需要备份】进行备份

### **如何保存私钥**

---

当发生客户端被删除、电脑丢失损毁、或是要在其他电脑上使用钱包的情况，除了重新导入钱包备份文件恢复之外，也可以通过钱包的【私钥】来恢复。所以，私钥也需要好好保存。钱包的私钥保存方式如下：

1.首先，点击钱包界面上方左侧的【账户】，再点击左侧下方的【权限】，进入钱包的权限界面，如下：

![](/assets/get private key.jpg)

然后点击页面钥匙状图标右侧的钱包公钥，弹出私钥查看菜单，然后点击【显示】

![](/assets/private key1.jpg)

输入钱包密码后，就会展示出你钱包的私钥，请务必妥善抄录后分开保存，绝对不要透露给他人，

任何人窃取了你的私钥都可以控制你的账户。

![](/assets/private key2.jpg)

### **如何恢复和导入钱包**

---

跟其他数字资产钱包一样，DBX只能在钱包注册的电脑使用。在同一台电脑使用DBX，也是不需要反复登陆的。如果你需要在其他电脑使用之前的钱包，或是你的钱包客户端被删除过，就要重新导入钱包备份文件或是钱包私钥，操作方法如下：

首先，打开钱包，点击右上角齿轮状的图标【设置】

![](/assets/recover via PK.jpg)

然后，点击左侧菜单栏的【恢复\导入】，这里可以选择三种方式导入钱包，这次主要讲从钱包备份导入和从私钥导入两种方法。

![](/assets/PK2.jpg)

**第一种方式：从钱包备份文件恢复**

在选择栏选择【从钱包备份文件恢复（.bin）】,然后在第二栏选择你此前备份的钱包文件

![](/assets/PK3.jpg)

导入文件后，要输入钱包密码，方可完成钱包文件的导入

![](/assets/PK4.jpg)

**第二种方式：用钱包私钥恢复**

用钱包私钥恢复，无需知晓之前钱包的密码，而是需要重新建立一个钱包，将原账户的信息和资产导入新钱包。操作方式如下：

在选择栏选择【导入私钥】，然后输入新建钱包的密码，并重输一遍确认

![](/assets/PK5.jpg)

输入完成后，等于新创建了一个钱包，再回到钱包首页，点击右上角齿轮状图标——点击恢复\导入，然后输入要导入的钱包私钥

![](/assets/PK6.jpg)

再点绿色的【导入私钥】按钮，完成导入，原钱包的信息和资产都进入新钱包。

### **充值和提现说明**

---

**1.提现地址说明**

当别人要给你的钱包转账或充值DBX时，你的**钱包账户名**就是你的钱包充值地址，比如下图中钱包账户名为zhangsan113，zhangsan113就是你的钱包地址。

![](/assets/transfer.jpg)

从交易平台提现DBX情况也一样，在交易所提现菜单的区块链地址中，填写你的钱包账户名，以上图钱包账户为例，填写的钱包地址就是：zhangsan113

特别提醒：跟比特币和其他数字资产一样，DBX也是去中心化和匿名的。从交易平台提现填错地址导致提现至他人账户时，没有人可以联络到该账户和追回你的数字资产，所以在提现时务必反复核对提现地址。

**2.转账说明**

1）.用钱包给他人转账

进入你的钱包账户，点击左上角【账户】来到账户页面，点击左侧菜单的【转账】开始转账

![](/assets/transfer2.jpg)

进入转账界面后，输入对方的钱包账户（钱包地址）、转账DBX数量，并可在【备注消息】（英文称为MEMO）附上相关说明，没有可以不填。最下方的手续费会根据MEMO的字符长短自动计算，不必自行设置（以最后的转账信息确认页为准）

![](/assets/transfer3.jpg)

点击发送后，需要你输入钱包的密码，来解锁钱包允许转账

![](/assets/transfer4.jpg)

转账发送前，会显示完整的转账信息，供你确认，如下：

![](/assets/transfer5.jpg)

点击发送后，转账很快就就会完成，并会在右侧出现转账被确认的信息提醒

![](/assets/transfer6.jpg)

2）.交易平台充值DBX

用钱包给交易平台充值，和给别的账户转账操作一样。交易所的钱包地址可以在交易所中查到。

与之前不同的是，**一定要填写交易所告知你的MEMO，**充值备注（MEMO）就是在这个平台，属于你的专属充值编号，平台通过这个编号来识别是谁给平台充值了数字资产。所以在转账充值时务必填写备注，并核对填写信息正确，填错可能导致DBX资产误充至他人账户导致无法追回。

根据以上情况，zhangsan113账户如果要给该平台充值0.5个DBX，钱包转账信息应该如下填写：

![](/assets/deposit.jpg)

![](/assets/deposit2.jpg)

## 高级功能

### 发行资产

---

//在DBXChain发行资产

### 分发资产

---

//链上分配资产

### 投票

---

用于给见证人候选人投票，从而选举出见证人

投票功能待更新（暂未开放）

### 商家认证

---

申请成为商家，获得在DBXChain数据交易所交易数据的权限。

方法详见[DBXChain](/dbxui.md)。

### 忠诚计划

---

忠诚计划，旨在激励公新股（DBX）持有人长期持有公信股。参与者要求在钱包内，按照计划规定的时间锁定一定量的公信股。DBXChain将在拿出一部分份额奖励忠诚计划参与者。

DBX转入钱包后，在DBX的首页（点击钱包顶端导航栏的“账户”可回到首页），点击DBX栏目下点击【加入忠诚计划】，如下图：![](/assets/loyalty.jpg)

点击【加入忠诚计划】后，会出现忠诚计划的设置页面。首先，选择你的参与计划时长，目前有3个月、9个月和24个月3个周期可供选择，不同的周期对应着不同DBX奖励比例，请见下图：

1. 锁定周期及到期奖励比率

| 锁定周期 | 年化收益 |
| :---: | :---: |
| 3个月 | 4% |
| 9个月 | 6% |
| 24个月 | 8% |

选定参与周期后，在【锁定金额】栏输入你要锁定的DBX数量，根据你输入的锁定数量，下方会自动计算出到期后可获得的奖励DBX数量，如下图：

![](/assets/loyalty2.jpg)设置完你参与的计划周期和参与数量后，点击【加入忠诚计划】的黑色按钮进行提交。你会收到一个锁仓提示——加入忠诚计划的金额将被锁定，期间不可卖出。

![](/assets/loyalty3.jpg)**一旦你确认参与，无论是你本人还是DBXChain项目方，无人有权限将参与计划的DBX解锁和释放。所以，在确认参与忠诚计划之前，请务必做好你的资金规划。**

点击确认参与后，需输入你的钱包密码，最终完成你对这笔锁仓操作的授权。

如果想要查看你已参与忠诚计划的情况，可以在钱包首页左侧下方点击【待解冻余额】，就可以查看到你已经参与的金额和时间情况（如下图）。

![](/assets/loyalty4.jpg)目前，DBXChain的网页钱包和新版钱包客户端已经完成忠诚计划功能的上线。

最新版钱包客户端，在访问DBXChain官网[www.dbx.io](/www.dbx.io)点击【钱包下载】下载新版钱包文件，重新安装后即可使用（无需删除原客户端和重新导入钱包）。

\*在使用钱包时，请务必做好钱包文件和私钥的备份，这是你控制钱包核心凭证；此外，在使用网页版钱包时，我们强烈建议用户使用电脑来访问和使用网页版钱包，而不是手机，因为手机浏览器容易在清理缓存时把钱包也清理掉，这时就需要重新导入钱包备份文件或私钥后方可使用。
