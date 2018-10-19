# get_account_history_by_operations

##### 说明：根据oeration_type查询帐户最近的交易记录，支持翻页并且返回operation对应的txID

##### usage: get_account_history_by_operations \[\] start limit_num

##### 参数：account_name_or_id, \[\], start, limit_num

| 参数 | 说明 |
| :--- | :--- |
| account_name_or_id | 帐户名或者id |
| \[\] | operation_type，比如转帐为0，可以写成\[0\]。若传空，则表示查询所有的operation_type |
| start | 起始序号，同get_relative_account_history |
| limit_num | 显示最近limit条交易记录 |



