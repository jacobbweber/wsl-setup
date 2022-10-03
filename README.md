# wsl-setup

## WSL 20.04 Setup
new ubuntu wsl 
```bash
sudo apt -y update 
sudo apt -y install ansible 
sudo pip3 install ansible 
```

## kerberos authentication support
```bash
sudo apt -y install python3-pip
sudo apt-get -y install python3-dev libkrb5-dev krb5-user
pip3 install pywinrm[kerberos]
```

### https://access.redhat.com/solutions/3486461
### fix "kerberos: Bad HTTP response returned from server. Code 500"
```bash
pip install --upgrade {pywinrm,pykerberos,requests-kerberos,requests-ntlm}
```

### configure realms in krb5.conf
```bash
/etc/krb5.conf
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
