# <a name="index"></a>index
* [Brief introduction of contract storage](#smart_contract_storage_brief_introduction)
* [example](#example)
* [Define the storage type](#define_type)
* [Add](#add)
* [Delete](#delete)
* [Find](#find)
* [Modify](#modify)


## <a name="smart_contract_storage_brief_introduction"></a>Brief introduction of contract storage
Used for storing contract data in the long term 
Data must be stored in the unit based on the C++ type case so that it must defines C++ types which can be stored in the contract. Each type has one table which is similar to the single sheet of the database of the relationship type but differntiates in the following features：  
```  
Support multiple indice   
Do not support union index   
Only the primary key is unique   
As to the index type, only uint64_t is supported   
If you want to take a string as an index, you must utilize uint64_t string_to_name(string str) in the contract library to transfer the string to uint64_t. Besides, the length of the string cannot exceed 12 and can only contain ([a-z].[1-5]) those 32 characters   
As to indice except for the primary key, when there are multiple records having same index value, the acquired objective is the most early record interpolated to the storage   
Support functions including add, delete, find and modify 
```
The following content will illustrate the principle based on examples  
[go_back](#index)  


## <a name="example"></a>example
```c++
#include <graphenelib/contract.hpp>
#include <graphenelib/dispatcher.hpp>
#include <graphenelib/multi_index.hpp>
#include <graphenelib/print.hpp>

using namespace graphene;

class multindex : public contract
{
    struct offer;

  public:
    multindex(uint64_t id)
        : contract(id)
        , offers(_self, _self)
    {
    }

    //@abi action
    void additem(uint64_t i1, uint64_t i2, std::string name)
    {
        uint64_t pk = offers.available_primary_key();
        print("pk=", pk);
        offers.emplace(0, [&](auto &o) {
            o.id = pk;
            o.idx1 = i1;
            o.idx2 = i2;
            o.stringidx = graphenelib::string_to_name(name.c_str());
        });
    }

    //@abi action
    void getbypk(uint64_t key)
    {
        auto it = offers.find(key);
        if (it != offers.end()) {
            dump_item(*it);
        }
    }

    //@abi action
    void getbyidx1(uint64_t key)
    {
        auto idx = offers.template get_index<N(idx1)>();
        auto matched_offer_itr = idx.lower_bound(key);
        if (matched_offer_itr != idx.end()) {
            dump_item(*matched_offer_itr);
        }
    }

    //@abi action
    void getbyidx2(uint64_t key)
    {
        auto idx = offers.template get_index<N(idx2)>();
        auto matched_offer_itr = idx.lower_bound(key);
        if (matched_offer_itr != idx.end()) {
            dump_item(*matched_offer_itr);
        }
    }
    
    //@abi action
    void getbystring(std::string key)
    {
        auto idx = offers.template get_index<N(stringidx)>();
        auto matched_offer_itr = idx.lower_bound(N(key));
        if (matched_offer_itr != idx.end()) {
            dump_item(*matched_offer_itr);
        }
    }

  private:
    void dump_item(const offer &o)
    {
        print("offer.id:", o.id, "\n");
        print("offer.idx1:", o.idx1, "\n");
        print("offer.idx2:", o.idx2, "\n");
        graphenelib::name n;
        n.value = o.stringidx;
        print("offer.stringidx:", n.to_string().c_str(), "\n");
    }

  private:
    //@abi table offer i64
    struct offer {
        uint64_t id;
        uint64_t idx1;
        uint64_t idx2;
        uint64_t stringidx;

        uint64_t primary_key() const { return id; }

        uint64_t by_index1() const { return idx1; }

        uint64_t by_index2() const { return idx2; }
        
        uint64_t by_stringidx() const {return stringidx; }

        GRAPHENE_SERIALIZE(offer, (id)(idx1)(idx2)(stringidx))
    };

    typedef multi_index<N(offer), offer,
                        indexed_by<N(idx1), const_mem_fun<offer, uint64_t, &offer::by_index1>>,
                        indexed_by<N(idx2), const_mem_fun<offer, uint64_t, &offer::by_index2>>,
                        indexed_by<N(stringidx), const_mem_fun<offer, uint64_t, &offer::by_stringidx>>>
        offer_index;

    offer_index offers;
};

GRAPHENE_ABI(multindex, (additem)(getbypk)(getbyidx1)(getbyidx2)(getbystring))

```


## <a name="define_type"></a>Define the storage type
```c++
  private:
    //@abi table offer i64
    struct offer {
        uint64_t id;
        uint64_t idx1;
        uint64_t idx2;
        uint64_t stringidx;

        uint64_t primary_key() const { return id; }

        uint64_t by_index1() const { return idx1; }

        uint64_t by_index2() const { return idx2; }
        
        uint64_t by_stringidx() const {return stringidx; }

        GRAPHENE_SERIALIZE(offer, (id)(idx1)(idx2)(stringidx))
    };

    typedef multi_index<N(offer), offer,
                        indexed_by<N(idx1), const_mem_fun<offer, uint64_t, &offer::by_index1>>,
                        indexed_by<N(idx2), const_mem_fun<offer, uint64_t, &offer::by_index2>>,
                        indexed_by<N(stringidx), const_mem_fun<offer, uint64_t, &offer::by_stringidx>>>
        offer_index;

    offer_index offers;
```

There should be annotation added with the type//@abi table offer i64  
@abi table fixed collocation  
offer is the table name, which can be self-defined based on your business demand but cannot exceed 12 characters and can only contain [a-z][1-5] those 32 characters, with letter and dot initial.  
i64 is the index type and fixed in writting.

struct offer{...} is the common c++ type with GRAPHENE_SERIALIZE(offer, (id)(idx1)(idx2)(stringidx)) at the bottom used for serializing.   
GRAPHEN_SERIALIZE(Type name, (Field name 1)(Field name 2)(Field name 3)(Field name 4)...)  

uint64_t primary_key() const { return id; } The function name and type of this part of code is fixed and unchangable which is used to designate the unique primary key. Here we regard id as the primary key  

The other three functions are used to define secondary indice  

The following code is used to define indice based on the defined c++ type：  
```
    typedef multi_index<N(offer), offer,  
                        indexed_by<N(idx1), const_mem_fun<offer, uint64_t, &offer::by_index1>>,  
                        indexed_by<N(idx2), const_mem_fun<offer, uint64_t, &offer::by_index2>>,  
                        indexed_by<N(stringidx), const_mem_fun<offer, uint64_t, &offer::by_stringidx>>>  
        offer_index;  
typedef multi_index<N(offer), offer,This line of code N(offer) should be consistent with the offer in the annotation'//@abi table offer i64'  
, offer is used to designate the defined type name  
``` 

```
indexed_by<N(idx1), const_mem_fun<offer, uint64_t, &offer::by_index1>>, this part of code is used to define a secondary index, one table can only define 16 indice at most, here we defined three  
N(idx1) is used to define index name  
const_mem_fun<offer, uint64_t, &offer::by_index1> The first parameter in the parantheses is the defined offer type name, the second parameter is the index type while the third one is the fucntion name among the offer types which is called by the index

Finally it is needed to define the real case variable of the index, offer_index offers，in the contract. _self (contract id) is needed for initialization in the constructor of the contract：   
```c++_
    multindex(uint64_t id)
        : contract(id)
        , offers(_self, _self)
    {
    }
```
[go_back](#index)  


## <a name="add"></a>Add
```c++
uint64_t pk = offers.available_primary_key();
print("pk=", pk);
offers.emplace(0, [&](auto &o) {
    o.id = pk;
    o.idx1 = i1;
    o.idx2 = i2;
    o.stringidx = graphenelib::string_to_name(name.c_str());
});
```
uint64_t pk = offers.available_primary_key(); used for acquiring the next legal primary key after self-increasing primary key, also can be designated by yourself
```c++
offers.emplace(0, [&](auto &o) {  
    o.id = pk;  
    o.idx1 = i1;  
    o.idx2 = i2;  
    o.stringidx = graphenelib::string_to_name(name.c_str());  
});
```

Interpolating objective utilizes lambda expression to assign a value to the new added objective o

o.stringidx = graphenelib::string_to_name(name.c_str()); here string type is used to realize the index but string is not directly supported to serve as an index

[go_back](#index)  


## <a name="delete"></a>Delete
Please read [Find] first (#find)  
Delete is always completed by the iterator of the table, and firstly it is always needed to call the find to find out the iterator of the objective needed to be deleted

offers.delete(it);  it is the iterator of the returned objective by the find operation
[go_back](#index)  


## <a name="find"></a>Find
```c++
auto idx = offers.template get_index<N(stringidx)>();
auto matched_offer_itr = idx.lower_bound(N(key));
if (matched_offer_itr != idx.end()) {
    dump_item(*matched_offer_itr);
}
```

auto idx = offers.template get_index<N(stringidx)>(); Acquire the index whose offer table's name is stringidx, the offer table has 4 indice, one is primary key index and the other three are idx1，idx2，  stringidx. It is more convenient to use primary key index without the need to firstly acquire the index by its name and then find the according key, however, it directly offers.find(pk)，which is also the iterator of the returned objective.  

auto matched_offer_itr = idx.lower_bound(N(key)); find the primary key objective corresponding to the string key by indice，meanwhile return the corresponding iterator matched_offer_itr  
[go_back](#index)  


## <a name="modify"></a>Modify

Please read [Find] first (#find)  

Modifying objective always executes modification by the iterator of the objective and lambda expression

```c++
offers.modify(it, 0, [&](auto &o) {
	//This is the modifying code of the objective
	o.idx1 = 1000;
});
```

[go_back](#index)
