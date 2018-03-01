# FAQ

## The `masternode outputs` return an empty object.
```
masternode outputs
```

You must receive the **1000 GOA** for the **masternode** in a single transaction on your **Control Wallet** and wait for at least 1 confirmation.
> If you already have the **1000 GOA** but it came from multiple transactions, you can send the **1000 GOA** to yourself.

## Running a **wallet** or a **masternode** container result in the following error:
```
************************
EXCEPTION: N5boost12interprocess22interprocess_exceptionE
No such file or directory
Wallet in AppInit()

terminate called after throwing an instance of 'boost::interprocess::interprocess_exception'
 what():  No such file or directory


************************
EXCEPTION: N5boost12interprocess22interprocess_exceptionE
No such file or directory
Wallet in AppInit()
```

Ensure the `data` folder is *writable* for the container.
