# Get_objects

##### Explanation：Query the target objective according to its ID

| Parameter | Explanation |
| :--- | :--- |
| ids | Target ID |

### **Calling case**

```
curl --data '{
"jsonrpc": "2.0", 
"method": "call", 
"params": [0, "get_objects", [["1.25.100","1.2.200"]]], "id": 1
}' 
 https://node1.dbx.io/rpc
```
