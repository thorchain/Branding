## Verifying Releases

1) Find the Release Message, copy the message hash
2) Paste into file, save
3) Decrypt and ensure is verified

```
nano msg // new file called "msg"
<paste in the message>
ctrl-X, Y // save, exit
gpg -d msg // decrypt the file to inspect who signed it
```
## Trusted Keys

Ensure the message is decrypted with the following trusted (users should always double check) keys:

```
pub   rsa4096 2022-04-06 [SC]
      F98400561D4636B4A92F07CE5BA40B710C7240C4
uid           [ultimate] thorianite <thorianite@protonmail.com>
```

```
pub   rsa2048 2020-04-16 [SC] [expires: 2030-04-14]
      9A6461A8CAAAA0AEB8EFDDA8C5334FE4FD04D709
uid           [ultimate] thorchain-admin <accounts@thorchain.org>
```

Locate public keys:
```
gpg --keyserver keys.openpgp.org --recv-keys F98400561D4636B4A92F07CE5BA40B710C7240C4
gpg --keyserver keys.openpgp.org --recv-keys 9A6461A8CAAAA0AEB8EFDDA8C5334FE4FD04D709
```


1) Download the files, then check the sha256 hash

```
cd /downloads
Mac: shasum -a 256 <file>
Linux: sha256sum <file>
Windows: certUtil -hashfile <file> SHA256
```

## Admin - how to sign

1) Collect hashes of the executables

```
cd /folder-with-executables
shasum -a 256 * // get them all
```

2) Paste into the following message:

```
The following binaries have been signed by THORChain/ASGARDEX admins listed at https://github.com/thorchain/Resources/blob/master/admin-GPG-keys.md.

<hash> file
<hash> file
<hash> file
```

3) Save to file, the GPG sign, copy the signed contents

```
nano msg // create new file
<paste in the above message
gpg --clear-sign -u <user> msg
ctrl-X, Y
nano msg.asc
```

4) Put in the Github Release

