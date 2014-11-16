P2F
===

Privacy Second Factor


Given the secret key, all public keys and signatures must be verifiable
===
kdf():  must be explicitly defined by FIDO (or let the manufacture explicitly defined the algorithm). (My suggestion is explicitly defined by FIDO and HKDF-SHA256(inputKeyMaterial:secret key, salt:user, info/context: server))

sign(): must be deterministic signing. (My suggestion is any secure curve with http://tools.ietf.org/html/rfc6979)

H():    defined FIDO (obviously not hashFunction(user || server || challenge). There's several ways to prevent collisions I just didn't want to bike shed over this).


First time use
===
Choice of set secret key with a live CD or use default secret key.

Legend
===
```
K = USB Key
B = Browser
S = Server
```

Registration
===
```
K<-B<-S: User (user id or user name), server (ie google.com)
K: Button is pressed
K: privateKey = kdf(secretKey, user, server)
K: publicKey = genPublicKey(privateKey)
K->B->S: publicKey
```

Login
===
```
K<-B<-S: User (user id or user name), server (ie google.com), challenge (32 bytes of CSPRNG)
K: Button is pressed
K: privateKey = kdf(secretKey, user, server)
K: signature = sign(privateKey, H(user, server, challenge))
K->B->S: signature
```

----------

Button press is REQUIRED for registration and login to happen \*PERIOD\* \*END OF SENTENCE\*
