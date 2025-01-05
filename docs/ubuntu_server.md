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

## to get rid of entering password to login to remote-server

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
