## Index Table
| belong | api name | description |
| --- | --- | --- |
| <graphenelib/action.h> | [current_receiver](#current_receiver) | Return the id of current contract account |
| <graphenelib/action.h> | [get_action_asset_id](#get_action_asset_id) | Return the asset id sent from this call to the contract |
| <graphenelib/action.h> | [get_action_asset_amount](#get_action_asset_amount) | Return the asset quantity sent from this call to the contract |
| <graphenelib/asset.h> | [withdraw_asset](#withdraw_asset) | Transfer the asset of current contract to an external account |
| <graphenelib/asset.h> | [get_balance](#get_balance) | Acquire the balance of certain asset of the external account |
| <graphenelib/crypto.h> | [sha256](#sha256) | Compute sha256 of the data|
| <graphenelib/crypto.h> | [sha512](#sha512) | Compute sha512 of the data|
| <graphenelib/crypto.h> | [ripemd160](#ripemd160) | Compute ripemd160 of the data |
| <graphenelib/crypto.h> | [verify_signature](#verify_signature) | Verify the signature |
| <graphenelib/global.h> | [get_head_block_num](#get_head_block_num) | Acquire the number of the newest block |
| <graphenelib/global.h> | [get_head_block_id](#get_head_block_id) | Acquire the hash of the newest block |
| <graphenelib/global.h> | [get_head_block_time](#get_head_block_time) | Acquire the time of the newest block where the return value is in second unit |
| <graphenelib/global.h> | [get_trx_sender](#get_trx_sender) | Acquire the instance_id of the account calling the contract |
| <graphenelib/global.h> | [get_account_id](#get_account_id) | Acquire the instance_id of the account according to the account's name |
| <graphenelib/global.h> | [get_asset_id](#get_asset_id) | Acquire the instance_id of the asset according to the asset's name |
| <graphenelib/system.h> | [graphene_assert](#graphene_assert) | If the condition is not satisfied, terminate the contract execution and roll back all the status |
| <graphenelib/system.h> | [graphene_assert_message](#graphene_assert_message) | If the condition is not satisfied, output the necessary information while the contract execution will continue |
| <graphenelib/system.h> | [print](#print) | Used for printing the log when doing the test work|


<a name="current_receiver"></a>
## uint64_t current_receiver()
Return the account id of the current contract, reserve all the decimals. For example, if the account id is 1.2.12345, then 12345 should be reserved.

<a name="get_action_asset_id"></a>
## uint64_t get_action_asset_id();
When calling a contract, the asset id sent to the contract will be rounded to all decimals.


<a name="get_action_asset_amount"></a>
## int64_t get_action_asset_amount();
The asset quantity sent to a contract (multiplied by 100 thousand) when calling it

<a name="withdraw_asset"></a>
## void withdraw_asset(uint64_t from, uint64_t to, uint64_t asset_id, int64_t amount)
Transfer the asset of current contract to an external account

\<uint64_t\> from: Transfer from which account, normally_self <br>
\<uint64_t\> to: Transfer to which account, only account instance_id should be sent. For example, if the external account is 1.2.33, then you only need to send 33 <br>
\<uint64_t\> asset_id: Designate the asset id used for transfer, only instance_id of the asset id should be sent. For exmaple, if the asset id is 1.3.0, only 0 should be sent <br>
\<int64_t\> amount: Transfer amount, this number represents the accuracy of the asset. For example, if you want to transfer 1 DBX, then you should enter 100000 <br>




<a name="get_balance"></a>
## int64_t get_balance(int64_t account, int64_t asset_id)

Acquire the balance of certain asset of an external account

\<int64_t\> account: instance_id of an external account<br>
\<int64_t\> asset_id: instance_id of the designated asset

<a name="sha256"></a>
## void sha256(const char *data, uint32_t length, checksum256 *hash)
Compute sha256 of the data

\<char\> data: The address of the string head used for computing sha256 <br>
\<uint32_t\> length: Length of the data string <br>
\<const checksum256 *\> hash: Used for storing the computed sha256


<a name="sha512"></a>
## void sha512(const char *data, uint32_t length, checksum512 *hash)

Compute sha512 of the data

\<char\> data: The address of the string head used for computing sha512 <br>
\<uint32_t\> length: Length of the data string <br>
\<const checksum512 *\> hash: Used for storing the computed sha512



<a name="ripemd160"></a>
## void ripemd160(const char *data, uint32_t length, checksum160 *hash)

Compute ripemd160 of the data

\<char\> data: The address of the string head used for computing ripemd160 <br>
\<uint32_t\> length: Length of the data string <br>
\<const checksum160 *\> hash: Used for storing the computed ripemd160 <br>



<a name="verify_signature"></a>
## bool verify_signature(const char *data, uint32_t datalen, const signature* sig,  const char *pub_key, uint32_t pub_keylen)

Verify the signature

\<const char\> data: The initla string of the signature <br>
\<uint32_t\> datalen: data length of the string <br>
\<signature\> sig: Signature data <br>
\<const char *\> pub_key: The public key corresponding to the private key which is used to do the signature <br>
\<uint32_t\> pub_keylen: Length of the public key



<a name="get_head_block_num"></a>
## int64_t get_head_block_num()

Acquire the number of the newest block



<a name="get_head_block_id"></a>
## int64_t get_head_block_id()

Acquire the hash of the newest block



<a name="get_head_block_time"></a>
## int64_t get_head_block_time()

Acquire the time of the newest block where the return value is in second unit



<a name="get_trx_sender"></a>
## int64_t get_trx_sender()

Acquire the instance_id of the account calling the contract



<a name="get_account_id"></a>
## int64_t get_account_id(const char * data, uint32_t length)

Acquire the instance_id of the account according to the account's name


\<const char *\> data: Acoount name, for example, nathan <br>
\<uint32_t\> length: Length of the account name, for example, length of nathan is 6



<a name="get_asset_id"></a>
## int64_t get_asset_id(const char * data, uint32_t length)

Acquire the instance_id of the asset according to the asset's name

\<const char *\> data: Asset name <br>
\<uint32_t\> length: Length of the account name, for example, length of nathan is 6



<a name="graphene_assert"></a>
## void graphene_assert(uint32_t test, const char* msg)

If the condition is not satisfied, terminate the contract execution and roll back all the status

\<uint32_t\> test:  <br>
\<const char*\> msg: <br>



<a name="graphene_assert_message"></a>
## void graphene_assert_message(uint32_t test, const char* msg, uint32_t msg_len)

If the condition is not satisfied, output the necessary information while the contract execution will continue

\<uint32_t\> test: <br>
\<const char*\> msg:  <br> 
\<uint32_t\> msg_len:  <br>



<a name="print"></a>
## inline void print( const char* ptr )；[example](examples/helloworld.md)

Used for printing the log when doing the test work

\<const char*\> ptr: 
