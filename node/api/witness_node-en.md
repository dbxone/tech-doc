## Witness API command list

### database api

| Command | Parameter | Explanation | Note |
| :--- | :--- | :--- | :--- |
| [get_objects](witness_node/getobjects.md) | &lt;ids&gt; | Find the target objective according to its ID |  |
| set_subscribe_callback | &lt;cb&gt; &lt;clear_filter&gt; | Callback for the registration of global subscription |  |
| set_data_transaction_subscribe_callback | &lt;cb&gt; &lt;clear_filter&gt; | Callback for the registration of data transaction |  |
| unsubscribe_data_transaction_callback |  | Callback for the cancellation of registrating data transaction |  |
| set_data_transaction_products_subscribe_callback | &lt;cb&gt; &lt;ids&gt; | Data transaction callback for the registration of specific data product ID |  |
| set_pending_transaction_callback | &lt;cb&gt; | Callback for the transaction whose registration has not been confirmed |  |
| set_block_applied_callback | &lt;cb&gt; | Callback for whether Set up the current block as the one registered by callback |  |
| cancel_all_subscriptions |  | Cancel all the subscriptions（callback） |  |
| [get_block_header](witness_node/getblock-header.md) | &lt;block_num&gt; | Acquire the block head information |  |
| get_transaction | &lt;block_num&gt; &lt;trx_in_block&gt; | Acquire the transaction information |  |
| get_block | &lt;block_num&gt; | Acquire the block information |  |
| get_recent_transaction_by_id | &lt;id&gt; | Query the transaction based on TXID, the return is empty if the transaction is overdue |  |
| get_chain_properties |  | Acquire the chain property |  |
| get_global_properties |  | Acquire global propoerty |  |
| get_commission_percent |  | Acquire commission ratio |  |
| get_config |  | Acquire the compiling constant |  |
| get_chain_id |  | Acquire the chain ID |  |
| get_dynamic_global_properties |  | Acquire the dynamic global property |  |
| get_key_references | &lt;key&gt; | Return all the account information pointing to the public key |  |
| is_public_key_registered | &lt;public_key&gt; | Verify whether the public key has been registered |  |
| get_accounts | &lt;account_ids&gt; | Acquire the account information by ID |  |
| [get_full_accounts](witness_node/getfullaccounts.md) | &lt;names_or_ids&gt; &lt;subscribe&gt; | Acquire all the realted information of accounts which satisfy the conditions |  |
| get_account_by_name | &lt;name&gt; | Acquire the account information by the account name |  |
| get_account_references | &lt;account_id&gt; | Acquire the account id related to account_id |  |
| lookup_account_names | &lt;account_names&gt; | Acquire the account information by the account name |  |
| [lookup_accounts](witness_node/lookupaccounts.md) | &lt;limit&gt; &lt;lower_bound_name&gt; | Acquire the name and ID of registered accounts |  |
| get_account_count |  | Acquire the quantity of accounts which are registered on the chain |  |
| [get_account_balances](witness_node/getaccount-balances.md) | &lt;id&gt; &lt;assets&gt; | Acquire the account asset information by account ID and asset ID |  |
| get_named_account_balances | &lt;name&gt; &lt;assets&gt; | Acquire the account asset information by the account name and asset ID |  |
| get_balance_objects | &lt;&lt;\[address\]&gt;&gt; | Return all the balance objective which has not been received on the address |  |
| get_vested_balances | &lt;objs&gt; | Acquire the accessible asset information by the account balance ID |  |
| get_vesting_balances | &lt;account_id&gt; | Acquire information of the balance which belongs to the account but not accessible temprorarily by the account ID |  |
| list_data_transaction_complain_requesters | &lt;start_date_time&gt; &lt;end_date_time&gt; &lt;limit&gt; | Find the complaint initiator by the starting and ending time meanwhile return the first "limit" |  |
| list_data_transaction_complain_datasources | &lt;start_date_time&gt; &lt;end_date_time&gt; &lt;limit&gt; | Acquire the data source which is complained by the starting and ending time meanwhile return the first "limit" |  |
| get_assets | &lt;asset_ids&gt; | Acquire the asset by asset ID |  |
| [list_assets](witness_node/listassets.md) | &lt;lower_bound_symbol&gt; &lt;limit&gt; | Acquire the asset information by asset symbol name and return the first "limit" |  |
| lookup_asset_symbols | &lt;symbols_or_ids&gt; | Acquire the asset list by asset symbol |  |
| get_witnesses | &lt;witness_ids&gt; | Acquire the witness list by witness ID |  |
| get_witness_by_account | &lt;account&gt; | Acquire the witness information by account ID |  |
| lookup_witness_accounts | &lt;lower_bound_name&gt; &lt;limit&gt; | Acquire the ID and name of the registered witness |  |
| get_witness_count |  | Acquire the qunatity of the registered witness |  |
| get_committee_members | &lt;committee_member_ids&gt; | Acquire the information of the committee member by ID |  |
| get_committee_member_by_account | &lt;account&gt; | Acquire the information of the committee member by account ID |  |
| lookup_committee_member_accounts | &lt;account&gt; &lt;limit&gt; | Acquire ID and account name of the registered committee members, return the first "limit" |  |
| get_workers_by_account | &lt;account&gt; | Acquire the working objective information by account ID |  |
| lookup_vote_ids | &lt;votes&gt; | Acquire the voting objective by its ID |  |
| get_transaction_hex | &lt;trx&gt; | Acquire the hexadecimal code of the signed transaction information |  |
| get_required_signatures | &lt;trx&gt; &lt;available_keys&gt; | Acquire the signature public key of the signed transaction information |  |
| get_potential_signatures | &lt;trx&gt; | Acquire the signature public key of the signed transaction information |  |
| get_potential_address_signatures | &lt;trx&gt; | Acquire the address of the signed transaction information |  |
| verify_authority | &lt;trx&gt; | Verify whether the transaction has satisfied all the signature request |  |
| verify_account_authority | &lt;name_or_id&gt; &lt;signers&gt; | Verify whether the signer has enough authority to control an account |  |
| validate_transaction | &lt;trx&gt; | Verify but not broadcast the transaction currently |  |
| get_required_fees | &lt;ops&gt; &lt;id&gt; | Acquire the commission by the operation ID and asset ID |  |
| get_proposed_transactions | &lt;id&gt; | Acquire the related proposed transaction by specific account ID |  |
| get_blinded_balances | &lt;id&gt; | Acquire the hidden asset by the entrusting ID |  |
| get_data_transaction_product_costs | &lt;start&gt; &lt;end&gt; | Acquire the product fee of data the transaction in the designated period |  |
| get_data_transaction_total_count | &lt;start&gt; &lt;end&gt; | Acquire the quantity of data transaction in the designated period |  |
| get_merchants_total_count |  | Acquire current merchant qunatity |  |
| get_data_transaction_commission | &lt;start&gt; &lt;end&gt; | Acquire the data transaction commission in the designated period |  |
| get_data_transaction_pay_fee | &lt;start&gt; &lt;end&gt; | Acquire the data transaction payment fee in the designated period |  |
| get_data_transaction_product_costs_by_requester | &lt;requester&gt; &lt;start&gt; &lt;end&gt; | Acquire the product fee genereated by data transaction of the requested account (merchant) in designated period |  |
| get_data_transaction_total_count_by_requester | &lt;requester&gt; &lt;start&gt; &lt;end&gt; | Acquire the transaction frequency of the requested account (merchant) in designated period |  |
| get_data_transaction_pay_fees_by_requester | &lt;requester&gt; &lt;start&gt; &lt;end&gt; | Acquire the transaction payment fee of the requested account (merchant) in designated period |  |
| get_data_transaction_product_costs_by_product_id | &lt;product_id&gt; &lt;start&gt; &lt;end&gt; | Acquire the product costs generated by buying designated product in designated period |  |
| get_data_transaction_total_count_by_product_id | &lt;product_id&gt; &lt;start&gt; &lt;end&gt; | Acquire the frenquency of buying designated product in designated period |  |
|  |  |  |  |

### history api

| Command | Parameter | Explanation | Note |
| :--- | :--- | :--- | :--- |
| get_account_history | &lt;account_id&gt; &lt;start&gt; &lt;limit&gt; &lt;stop&gt; | Query transaction history of the account, among which start/stop is operation_history_id， id is 1.11.x |  |
| get_account_history_by_operations | &lt;account_id&gt; &lt;operation_ids&gt; &lt;start&gt; &lt;limit&gt; | Query transaction history of the account, filter out designated transaction history according to operations_ids，among which start is the serial number which begins from 1 |  |
