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