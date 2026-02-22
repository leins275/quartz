---
title: GPG
date: 2026-02-22
draft: false
tags: []
aliases:
---

# Installation

on linux just install gpg program, for example `gnupg`

```bash
gpg --expert --edit-key <KEY_ID> addkey
gpg --export-secret-subkeys <SUBKEY_ID>! > secret.gpg
```


# list secret subkeys with fingerprints

```bash
gpg --list-secret-keys --with-subkey-fingerprints
```

# Verify installation

```bash
gpg --version
gpg -k # show public keys
gpg -K # show provate keys
```

# Delete private subkeys

```
gpg edit-key --expert <key_id>
```
to delete key with number n (1, 2, 3 etc. the first keys is on top after public key)
select this key `key <n>`, for example key 4.
then execute `delkey` and `save` commands.

# Delete primary key from pc to secret place
```bash
gpg -a --export-secret-key <key-id> > secret_key # export primary secret key
gpg -a --export <key-id> > public_key.gpg # export public key
gpg -a --export-secret-subkeys <key-id> > secret_subs.gpg # export secret subs
gpg --delete-secret-keys <key-id> # delete secret key
gpg --import secret_subs.gpg # import secret subs back

```

# Export subkeys for laptop
```bash
gpg -a --export-secret-keys johenews > laptop_keys_secret.gpg
gpg -a --export johenews > laptop_keys_public.gpg
```

# Export single secret subkey 
```bash
gpg -a --output secret-subkeys.gpg --export-secret-subkeys SUBKEYID!
```

# Add new secret subkey

Generate new secret subkey
```bash
gpg --expert --edit-key <key-id> addkey
```
use option 6 to encrypt only or choose your own permissions

# Import keys from file

```bash
gpg --import public_key.gpg
gpg --import secret_subs.gpg
```

# Trust imported keys

```bash
gpg --edit-key <KEY_ID>
gpg> trust
```

---
1. [Статья dewpew o gpg](https://devpew.com/blog/gpg)
2. [Статья на archwiki](https://wiki.archlinux.org/index.php/GnuPG)
3. [gpg cheatsheet](https://gock.net/blog/2020/gpg-cheat-sheet/)
