# chat.rip

Client-side encrypted file/message delivery service.<br>
Verifiable transfer security by verifying outgoings packets signatures against the locally stored key.

Your browser/client has a master-certificate *(priv, pub)*.<br>
Each message or file-chunk gets it's own AES key, wrapped/encrypted with the recipients public cert.

# Data being shared

 * A locally generated (per refresh of page) public certificate
 * A server-side assigned random ID (per connection/refresh of page)
 * A random `file_id` string based on nothing per file-upload that lasts throughout the upload session.

No other information is ever generated by the client, server or kept on the server.<br>
The servers only tracking of each connection is the during the session and the filenumber internally in Linux.

*TODO: Remove references of IP.*

# File uploads

The file being uploaded will be split into chunks of `1024`.<br>
Each chunk will be encrypted, and sent to your peer.<br>
The server will store `file_id` *(randomly generated on client side)* and ammount of chunks sent/recieved.

This is so that both ends of the transmission can send `checksum: file_id` and get a verification of which chunks might have gotten lost in transmit.
Once both sides are happy / verified the transfer, the checksum information gets dropped.

Data won't be stored, since there's no point since each side in the P2P connection encrypts the data.

**TODO:** Sent message should be added to history.