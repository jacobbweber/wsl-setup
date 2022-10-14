# wsl-setup

## From an elevated Powershell
```bash
wsl --install
```

new ubuntu wsl 
```bash
sudo apt -y update 
sudo apt -y install ansible 
** didnt need to do this step? sudo pip3 install ansible 
```

## kerberos authentication support
```bash
sudo apt -y install python3-pip
** Already installed from previous step sudo apt-get -y install python3-dev libkrb5-dev krb5-user
** Already installed from previous step pip3 install pywinrm[kerberos]
```

### https://access.redhat.com/solutions/3486461
### fix "kerberos: Bad HTTP response returned from server. Code 500"
```bash
pip install --upgrade {pywinrm,pykerberos,requests-kerberos,requests-ntlm}
```

### configure realms in krb5.conf
```bash
sudo vi /etc/krb5.conf
```

### Optional - If needed, create krb5.conf.d directory with permissions DO NOT USE 777 unless trash lab and dont care
```bash
touch /etc/krb5.conf.d/
sudo mkdir /etc/krb5.conf.d/
sudo chmod 777 /etc/krb5.conf.d/
```
To remove a dir:
```bash
rm -d /etc/krb5.conf.d/
```

### to persist DNS resolv.conf after WSL reboot (may only be needed with wsl2 win11) , add this
run:
```bash
sudo touch /etc/wsl.conf
sudo vim /etc/wsl.conf
```
add:
```yaml
[network]                                                                        
generateResolvConf = false
```

## configure resolve.conf for dns lookup, replace with Internal DC ipaddr
```bash
sudo vi /etc/resolv.conf
```
### Exmaple:
This file was automatically generated by WSL. To stop automatic generation of this file, add the following entry to /etc/wsl.conf:
```yaml
#[network]
#generateResolvConf = false
nameserver 8.8.8.8
nameserver 8.8.4.4
```

### if needed restart wsl
Restart wsl (Windows powershell) using
```powershell
wsl --shutdown
```

### Notes:
https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-git
If you are seeking to access the Windows file directory from your WSL distribution command line, instead of C:\Users\username, the directory would be accessed using /mnt/c/Users/username, because the Linux distribution views your Windows file system as a mounted drive.

### Setup Git in WSL

For the latest stable Git version in Ubuntu/Debian, enter the command:
```bash
sudo apt-get install git
```
### Git config file setup:
To set up your Git config file, open a command line for the distribution you're working in and set your name with this command (replacing "Your Name" with your preferred username):
```bash
git config --global user.name "Your Name"
```
Set your email with this command (replacing "youremail@domain.com" with the email you prefer):
```bash
git config --global user.email "youremail@domain.com"
````
To set up GCM for use with a WSL distribution, open your distribution and enter this command: This needs troubleshooting, not working
```bash
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager-core.exe"
```
For AzureDevops Repos
```bash
git config --global credential.https://dev.azure.com.useHttpPath true
```

