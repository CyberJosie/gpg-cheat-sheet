# gpg-cheat-sheet
It's a GPG cheat sheet, I don't know what else to say.

GnuPG is a tool for secure communication. This chapter is a quick-start guide that covers the core functionality of GnuPG. This includes keypair creation, exchanging and verifying keys, encrypting and decrypting documents, and authenticating documents with digital signatures. It does not explain in detail the concepts behind public-key cryptography, encryption, and digital signatures. 

# Using The GPG Command Line Utility
Click the links along this page that reference the official GPG documentation. 

## Generating Key Pairs
[Read The Docs](https://www.gnupg.org/gph/en/manual/c14.html)

To generate a key pair with the GPG command line utility use this command:
```
```
You will be asked questions about the key including:
* Encryption Algorythms
* Key Size (1024 - 4096)
* Key Expiration (If any at all)
* Real name (Just something that identifies you, like a username)
* Email address (Recommended)
* Comment (Optional)

## Generating A Revocation Certificate
[Read The Docs](https://www.gnupg.org/gph/en/manual/c14.html)

Revocation certificates are used to revoke usage of your key if it is lost or compromised. It is important to generate this certificate each time you create a new key BEFORE you need it and store it in a safe place.

To Generate a revocation certificate:
```
gpg --output revocation.crt --gen-revoke <alias_email_or_fingerprint>
```

## Encrypting & Decrypting Messages
[Read The Docs](https://www.gnupg.org/gph/en/manual/x110.html)

Encryption is done via the public key and can only be decrypted by the corresponding private key.
```
gpg --output encrypted_message.gpg -r <alias_email_or_fingerprint> --encrypt <message_or_file>
```

Decryption can only be done via the private key. It's a good practice to verify signatures along with decryption, but we'll cover that later.
```
gpg --output decrypted_msg.txt -r <alias_or_fingerprint_slice> --decrypt msg.gpg
```
