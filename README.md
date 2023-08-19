# SIMPLE HARDENING FOR LINUX SERVER

### Process

1 - Create new user

```
adduser ubuntu
```

2 - Add user to sudo group

```
usermod -aG sudo ubuntu
```

3 - Remove user password

```
passwd -d ubuntu
```

4 - Open sshd config file

```
nano /etc/ssh/sshd_config
```

5 - Remove all lines from the file and include the content available in the link below

https://raw.githubusercontent.com/IsraelXabregas/linux-hardening/main/sshd_config

To remove the lines just press ctrl + k until the file is blank

6 - Restart ssh service

```
service ssh restart
```

7 - Install fail2ban service to protect the ssh access

```
apt install fail2ban
```

8 - Open the jail file to edit

```
nano /etc/fail2ban/jail.conf
```

9 - Find for [sshd] block and uncomment the line to activate the ssh jail

```
enabled = true
```

10 - Enable the fail2ban service

```
systemctl enable fail2ban
```

11 - Create a SSH keypair on your computer with WSL, Mac or Linux

```
ssh-keygen
```

12 - Go to the server, change the user to ubuntu and create the .ssh directory with authorized_keys file

```
su ubuntu

cd

mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh
```

13 - Go back to your computer and copy the generated public key file content

```
chmod 0400 israel-linode

cat israel-linode.pub
```

14 - Go back to your server and paste the public key file content on file authorized_keys

```
nano .ssh/authorized_keys
```

15 - Logout from ubuntu user and remove the root password

```
passwd -d root
```

Now the access from root is disabled, you must to login with ubuntu user, with your private key
