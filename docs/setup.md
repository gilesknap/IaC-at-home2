# Initial setup of your infrastructure as code environment

## Set up a master keypair

We will first create a master keypair that will be used to access all of the nodes in the cluster including the BMC.

Here we call it ansible_master, if you choose a different name then update the variable public_key in the hosts file.
```bash
ssh-keygen -t rsa -b 4096 -C "ansible master key" -f ~/.ssh/ansible_master
```

You should create a passphrase for this keypair.

## Authorize your keypair for each Turing Pi

Do the following for each of your turing pi boards. The name will be turingpi or turingpi.local for the first board and turingpi-2, turingpi-3 etc for the others (maybe?).

```bash
# copy over the public key to the turing pi
scp ~/.ssh/ansible_master.pub root@turingpi:.ssh/authorized_keys
# connect - you will be asked for your passphrase from above
ssh root@turingpi
passwd # change the password to something secure
exit
```
