# GPG Cheat Sheet
It's a GPG cheat sheet, I don't know what else to say.

GnuPG is a tool for secure communication. This guide is a summary of the documentation for the GPG command line utility. Click the links in each section at any time to read more about the subject on the official documentation.

# Using The GPG Command Line Utility

# Listing Keys
To view public keys
```
gpg -k
```
OR
```
gpg --list-keys
```

To view private keys
```
gpg -K
```
OR
```
gpg --list-secret-keys
```

## Generating Key Pairs
[Read The Docs](https://www.gnupg.org/gph/en/manual/c14.html)

To generate a key pair with the GPG command line utility use this command:
```
gpg --full-gen-key
```

You will be asked questions about the key including:
* Encryption Algorythms
* Key Size (1024 - 4096)
* Key Expiration (If any at all)
* Real name (Just something that identifies you, like a username)
* Email address (Recommended)
* Comment (Optional)

When you are finished, enter 'O' to generate and password protect your key.

## Generating A Revocation Certificate
[Read The Docs](https://www.gnupg.org/gph/en/manual/c14.html)

Revocation certificates are used to revoke usage of your key if it is lost or compromised. It is important to generate this certificate each time you create a new key BEFORE you need it and store it in a safe place.

To Generate a revocation certificate:
```
gpg --output revocation.crt --gen-revoke <alias_email_or_fingerprint>
```

It's best to store the recovation certificate and any private keys offline on your own storage medium. If you store it in the cloud, it is not fully yours.

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

If an output location is not specified the decrypted content will be printed to STDOUT.

## Making & Verifying Signatures

## This talks about detached signatures, there are multiple types. Proceed with caution.
[Read The Docs](https://www.gnupg.org/gph/en/manual/x135.html)

Signatures are used to cryptographically verify that the content was encrypted by the owner and has not been tampered with since its origin. This is important when downloading applications and reading encryption messages. The person who encrypted the data will have also provided a signature if they have some sense. To verify a detached signature (which is better used for messages and communication):

```
gpg --decrypt message.sig
```

To learn more about using signatures in other ways, click the link to the documentation above. For most applications that use GPG to verify their origin, you will need to import a public key before you are able to verify the signature. To create a detached signature, use the command below:

```
gpg --output message.sig --detach-sign encrypted_message.gpg
```

## Importing & Exporting Keys
[Read The Docs](https://www.gnupg.org/gph/en/manual/x56.html)

When you create a key pair via the GPG command line utility it is stored on your systems keyring by default. You can use them from here in whatever way you need. If you want to export the keys and use them on other systems however, you will need to know how to import and export keys to files.


### Exporting Keys

To export a public key as bytes
```
gpg --export <key>
```
To export a public key as GPG block
```
gpg --export --armor <key>
```

To export a private key as bytes
```
gpg --export-secret-keys <key>
```
To export a public key as GPG block
```
gpg --export-secret-keys --armor <key>
```

### Importing Keys

To import a public key:
```
gpg --import pub.key
```

You do not always need to manually trust a key however some keys require it. Fingerprints are human readable strings that cryptogaphically verify the owner.

### Fingerprint
You cen get the fingerprint of a key with:
```
gpg --fingerprint <key>
```

To manually trust a key use the `--edit-key` switch.
```
gpg --edit-key <key>
```

Then if you haven't already you can check the fingerprint at the prompt by entering `fpr`. Once you have verified the fingerprint you can trust the key by entering `sign` and proceeding. Once you have signed it you can check your signatures for the key with `check`.


# Helpful Bullets
* When referring to a key you can use the name of the owner, email of the owner, or a slice of the fingerprint. It's typically best to use the last 8 characters when using the fingerprint.
* If you are using GPG on a Unix based system, run `man gpg` at the command line to see a set of instructions on your system at any time. Alterntatively, you can run `gpg --help`.


