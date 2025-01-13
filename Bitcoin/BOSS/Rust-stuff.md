## btc transaction object


version field = `u32` unsigned integer data type

>[!note]
>version field in BTC transaction data = 4bytes
>A byte is a unit of computer memory that holds
>8 bits of data
>1 byte = 8 bits
>4 bytes = 8 x 4 = 32 bits

Each bit is the most basic computing unit and can either be `1` or `0`


**signet challenge hint**

format good, balance bad 
NEW
[18:43]
you are very close
NEW
[18:43]
the big hint for this challenge is: just iomport your descriptor into your locally synced signet node and query the balance

1
NEW
[18:43]
then you know the exact right answer
NEW
[18:44]
and can even look through the tx history to see what you did wrong
NEW
[18:44]
its not cheating as long as you still write working code
NEW
[18:48]
@riverKanies 
println!("{} {:.8}", WALLET_NAME, balance);

is this the right format? i am a rust n00b !