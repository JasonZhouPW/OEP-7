# OEP-7 URI Schema

## Abstract

The OEP-7 Proposal is a standard interface of URI schema,  this standard allows for the implementation of mapping ontology address to readable strings.



## Motivation

1.  when transfer assets or invoke a smart contract , you need to input or copy&paste the base58 format address, it's very hard to type the 34 meaningless characters exactly and  some virus may modify the clipborad content.
2. when a smart contract upgrade or migrate, the related contracts which using appcall  will have to upgrade too.



## Specification

All the following address should be base58 format

### Methods

#### register

```
def register(from_address, uri, validt_to, network_id)
```

This allows user(address) to register (bind) a meaningful string ,

the  name should be alphanumeric and no more than 64 characters, 

valid_to is time stamp ,

networkid is reserved for subchain, 1 is for mainnet.

This should be raise a 'transfer' event with ['00', from_address, uri, network_id]

#### ownerOf

```
def ownerOf(uri, network_id)
```

Returns owner address of the URI name



#### getOwnedUriCount

```
def getUriCount(from_address, network_id)
```

Returns binded URI count of from address



#### getAddressByURI

```
def getAddressByURI(uri, network_id)
```

Returns the address binded by URI



#### transfer

```
def transfer(from_address, to_address, uri, network_id)
```

Transfer(bind) URI to other address, if the URI is invalid will raise an exception, this should be only called by URI owner. 

Note: transfer will not change the valid time of the URI.

This should trigger a 'transfer' event with [from_address, to_address, uri, network_id]



#### getURIByIndex

```
def getURIByIndex(index, network_id)
```

Returns the URI of the give index



#### getURITotalCount

```
def getURITotalCount(network_id)
```

Returns the total registered URI count 



#### getValidTimeOfURI

```
def getValidTimeOfURI(uri, network_id)
```

Returns valid time stamp of the URI



#### renewalURI

```
def renewalURI(from_address, uri, valid_to, network_id)
```

URI owner renewal URI valid time stamp



#### releaseURI

```
def releaseURI(admin_address, uri, network_id)
```

Release the invalid binded URI



#### releaseInvalid

```
def releaseInvalid(admin_address)
```

Release all invalid URIs



### Events

#### transfer

```
transferEvent = RegisterAction('transfer', 'from_address', 'to_address', 'uri')
```

This event MUST be triggered when URI registered and transfered