# transfer2

##### 说明：转帐操作，参数同transfer, 返回结果中包含当前交易的id

##### usage: transfer2 dbx1 dbx2 100 DBX "transfer memo" true

##### 参数：from_account to_account amount DBX "memo" BROADCAST

| 参数 | 说明 |
| :--- | :--- |
| from_account | 转帐发起帐户 |
| to_account | 转帐接收帐户 |
| amount | 转帐数目 |
| DBX | 转帐资产 |
| memo | 转帐备注，交易所用户充值时需要填写备注 |
| true | true表示真正执行 |



