# Ubuntu-server

## ssh

To enable `ssh` in system in linux system;

```shell
sudo apt install openssh-server # for server
sudo apt install openssh-client # for client
```

To enable `ssh` in windows system;

> Navigate to System -> Optional Features -> Add an optional feature in windows settings and find `OpenSSH Server` and enable it.
> 
> Go to services and make the service run `automatically`.
> 
> Similar steps could be followed to enable `OpenSSH Client` feature in Optional Features. Or `PuTTY` can be used as a client.

To `ssh` from a Debian WSL to an Ubuntu-Server first you need to have `openssh-client` in the WSL. Now type the below command to enter into your server.

```shell
ssh username@<ip-add of server>
```

## To get rid of entering password to login to remote-server

Use SSH public key encryption to get rid of typing the password all the time when you login to your server. This requires you to generate ssh keypairs.

To generate the SSH public and Private key

```shell
ssh-keygen -t rsa
```

`rsa` is one algorithm among the list of algorithms `[dsa | ecdsa | ecdsa-sk | ed25519 | ed25519-sk | rsa]`. You can provide the `passphrase` if you wish. The default storage location of the public/private key file is `C:\User\\<user-name\.ssh`.

Copy the content of  `id_rsa.pub` file to a file called `authorized_keys` in `~/.ssh` folder in linux server.

## scp

`scp` is a file copy/file transfer protocol unlike ftp. It is most secure way of transferring files between the remote systems.

```shell
scp "D:\girishree studio\KIS_9487.JPG" jeevan@192.168.30.6:/home/jeevan/Movies
```

## users

### add user

```shell
sudo adduser kite
```

This asks the `sudo` password and the new password to be created for the new user.

### change password

```shell
sudo passwd <username>
```

### remove user

```shell
sudo deluser <username>
```

### to see list of user

```shell
cat /etc/passwd
```

## X11

In order to run a GUI application in server X11 server can be used. 

- Start an X11 server in windows system Ex; Xming server

- Open PuTTY and enable the X11 configuration and login to server.

- Start a GUI application Ex; gedit

```shell
sudo apt install gedit
gedit
```

- This will open the GUI in windows machine.

## Public-Private key encryption

Public key encrypts the data. Private key decrypts the data.

### How Public-Private Key Cryptography Works

If A wants to send a message to B, A takes public key of B and encrypts the message with it and sends it to B. B uses the private key associated with his public key to decrypt the message. Since message is encrypted with B's Public key, it can only be decrypted by B's private key. So no middle man in between can decrypt the message and message is safe.

However, with this form of messaging there is no way to authenticate the source of the message. Anonymous person C can act like A to send message to B. Bjust thinks that the message came from A but actually its not.

To overcome this problem below methods are followed:

### Digital signature

B would not trust any message with which do not have a digital signature. In addition to message, A sends a Digital signature with it created by his private key. Since B knows A's public key, B can make sure the private key belongs to A by using A's public key. 

## Adding a new repository to `apt`

When `apt install python` is run, `apt` directs to standard repositories that are configured in `/etc/apt/sources.list` directory to find python package.

If certain intended package is not found while running `apt install <app-name>` command, that signifies that the package that you are finding is not part of the standard links that are configured in the `source.list` file.

For example;

```bash
sudo apt install cloudflared

OUTPUT:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package cloudflared
```

> apt is unable to locate the package because the application cloudflare is not part of the standard repository links pre-configured in the source.list file

### Add new configurations to source.list.d

New repository links must be added in case a package is not found in the standard links. User added links must be added to a folder called `source.list.d` by creating a new file. User defined repository links must not be added in the standard `source.list` file.

Example, In case of `cloudflare` below commands are run inorder to add a new repository to `apt`

```bash
# Add cloudflare gpg key
sudo mkdir -p --mode=0755 /usr/share/keyrings
curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg | sudo tee /usr/share/keyrings/cloudflare-main.gpg >/dev/null

# Add this repo to your apt repositories
echo 'deb [signed-by=/usr/share/keyrings/cloudflare-main.gpg] https://pkg.cloudflare.com/cloudflared any main' | sudo tee /etc/apt/sources.list.d/cloudflared.list

# install cloudflared
sudo apt-get update && sudo apt-get install cloudflared
```

The **GPG key** (GNU Privacy Guard key) is a **cryptographic key used to verify the authenticity** of software packages and the repository they're coming from.

### 📌 Why Add a GPG Key Before Adding a Repository?

When you install software using `apt` from an external source (like Cloudflare), you want to make sure:

- The packages really came from Cloudflare.

- The packages haven't been tampered with.

To do this, **apt uses GPG keys to verify the digital signatures of the packages** in the repository.

So the flow is:

1. Cloudflare signs its packages with its private GPG key.

2. You add the **public GPG key** to your system (the first command).

3. When you run `apt`, it:
   
   - Checks the signature of the packages.
   
   - Verifies the signature using the public key you installed.
   
   - Refuses to install if the signature doesn’t match.
