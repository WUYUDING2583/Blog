# How to set multiple git account on mac

When we have multiple git account, for example one company account one private account. How to use them in our own computer?

## 1. Generate SSH key

Firstly, we need to generate ssh keys for our different account. 

When we generate ssh keys, should notice need to generate it with different names, otherwise, the later one will overwrite former.

For example, we have tow git accounts **company** and **private**. Before we create keys, we need to go **~/.ssh** folder.

 Below is the command to generate their keys.

```
ssh-keygen -t rsa -f ~/.ssh/id_rsa_company -C "company email address"
ssh-keygen -t rsa -f ~/.ssh/id_rsa_private -C "private email address"
```

It will generate 4 files in **~/.ssh** folder

```
id_rsa_company      //company account private key
id_rsa_company.pub  //company account public key
id_rsa_private      //private account private key
id_rsa_private.pub  //private account public key
```

## 2. Add SSH key into our git account.

Open each key's public key and copy paste it into our git account.

## 3. Add config file

First look for `config` file in **~/.ssh** folder, if it don't exist we need to create it otherwise we just edit it. Below is its content:

What we need to change is the `Host` and `IdentityFile`.

**Host**: this prefix can define by ourselves for whatever. i.e. **xxx.github.com**.

**IdentityFile**: this should point out to our private key path.

```
# company account
Host company.github.com 
HostName github.com
PreferredAuthentications publickey
User git
IdentityFile ~/.ssh/id_rsa_company

# private account
Host private.github.com
HostName github.com
PreferredAuthentications publickey
User git
IdentityFile ~/.ssh/id_rsa_private
```

## 4. Test connection

After setting the config file, we can test if we can connect our git account by SSH or not.

```
ssh -T git@private.github.com 
```

When the terminal display below message, it means we connect our git account successfully.

```
Hi yuyi2583! You've successfully authenticated, but GitHub does not provide shell access.
```

## 5. Config repository

### 5.1 Delete global git config

Firstly we need to remove the global git config we have set before.

```
git config --global --unset 'user.name'
git config --global --unset 'user.email'
```

### 5.2 Config on each repository

Since we have different git account in our computer, we need to config git account on each repository we have.

```
git config user.name `xxx`
git config user.email `xxx@xxx.com`
```

## 6. Add remote repository

```
git remote add origin git@private.github.com:yuyi2583/Blog.git # private account
```

The `private.github.com` is the `Host` we set in `config` file.