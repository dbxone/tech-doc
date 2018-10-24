DBXChain smart contract database operation

---------------

The operation of the smart contract database is primarily realized by methods of multi-index table including emplace, erase, modify and find. 

### 1. Add

Using emplace method，complete the addition of new objectives into the table. Thereof, the parameter of emplace function is `lamada` expression.

```c++
        tables.emplace([&](auto &o) {
            o.issuer = owner;
        }); 
```

### 2. Delete

Useing erase method，delete the designated objectives in the table.

```c++
        tables.erase(table_iter);
```

### 3. Update

Using modify method, update the objectives in the table.

```c++
        tables.modify(table_iter, [&](auto &o) {
            o.issuer = new_issuer;
        });
```

### 4. Query

There are two methods to query the database: query by the primary key and query by the secondary index.

Query by the primary key：

```
        auto table_itr = tables.find(issuer);
```
