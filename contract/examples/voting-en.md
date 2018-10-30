# Contract introduction
Voting contract: record, find, delete the id, name and votes of candidates.

# Contract code
https://github.com/dbxone/dbxchain/blob/master/contracts/examples/voting/voting.cpp

# Compile the contract
```
dxx -o voting.wast voting.cpp
dxx -g voting.abi voting.cpp
```

# Deploy the contract

To deploy the contract, you have to import the private key of your account to the wallet and make sure it is unlocked.
```
unlocked >>> deploy_contract voting nathan 0 0 ./voting DBX true
```
Thereinto,
```
// voting designates the contract name which is going to be created
// nathan is the account which deploys the contract
// 0 0 respectivelty designates the vm type and version number
// ./voting designates the path of the contract file
// DBX means paying commission in DBX
// true means executing and initiating the broadcast
```

# Call the contract

## Voting
```
call_contract nathan voting null vote "{\"id\":1, \"name\":\"user1\"}" DBX true
call_contract nathan voting null vote "{\"id\":1, \"name\":\"user1\"}" DBX true

call_contract nathan voting null vote "{\"id\":2, \"name\":\"user2\"}" DBX true
call_contract nathan voting null vote "{\"id\":3, \"name\":\"user3\"}" DBX true
```

## Find votes
```
call_contract nathan voting null count "{\"id\":1}" DBX true
```

Hereby, run the log at witness_node and you will see the following information.
```
[(22,count)->22] CONSOLE OUTPUT BEGIN =====================
id=1, name=user1, count=2
[(22,count)->22] CONSOLE OUTPUT END =====================
```

## Find the voting list
```
call_contract nathan voting null list "{}" DBX true
```

Hereby, run the log at witness_node and you will see the following information.
```
[(22,count)->22] CONSOLE OUTPUT BEGIN =====================
id=1, name=user1, count=2
id=2, name=user2, count=1
id=3, name=user3, count=1
[(22,count)->22] CONSOLE OUTPUT END =====================
```

## Delete candidates
```
call_contract nathan voting null remove "{\"id\":1}" DBX true
```
Hereby, run the log at witness_node and you will see the following information.
```
[(22,count)->22] CONSOLE OUTPUT BEGIN =====================
remove name==user1
[(22,count)->22] CONSOLE OUTPUT END =====================
```
