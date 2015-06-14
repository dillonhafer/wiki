## Properly configure SSH

**1. Setup key-based authentication**

Key based logins work like a guest list at a party, if you're name (ssh public key) is on the guest list (authorized_keys files), you won't be asked for your password.

Your public key is in your home directory (~/.ssh/id_rsa.pub)
Append the contents of this file to the remote server user's folder (~/.ssh/authorized_keys)

```
scp ~/.ssh/id_rsa.pub remote.server.com:new_id_rsa.pub
```

then

```
ssh remote.server.com
cat ~/new_id_rsa.pub >> ~/.ssh/authorized_keys
rm ~/new_id_rsa.pub
```

**2. Disable password login**

```PasswordAuthentication no```

**3. Disable root login**

```PermitRootLogin no```