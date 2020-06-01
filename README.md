# Install-Ansible-on-RHEL-7 and Centos
This is  installation ansible offline on RHEL 7 and Centos

1. Create 3 Server (1 Server master and 2 Server client)
10.19.1.13      master
10.19.1.2       client-1
10.19.1.10      client-2

3. Setup hostname master server and client server
# vi /etc/hosts
[project-hore]
10.19.1.13      master
10.19.1.2       client-1
10.19.1.10      client-2

4. For start download rpm package depedency rpm
- https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/ansible-2.9.9-1.el7.ans.noarch.rpm
- http://mirror.centos.org/centos/7/extras/x86_64/Packages/python2-jmespath-0.9.0-3.el7.noarch.rpm
- http://mirror.centos.org/centos/7/extras/x86_64/Packages/python-httplib2-0.9.2-1.el7.noarch.rpm
- http://mirror.centos.org/centos/7/extras/x86_64/Packages/python-paramiko-2.1.1-4.el7.noarch.rpm
- http://mirror.centos.org/centos/7/extras/x86_64/Packages/python-passlib-1.6.5-2.el7.noarch.rpm
- http://mirror.centos.org/centos/7/extras/x86_64/Packages/sshpass-1.06-2.el7.x86_64.rpm

5. Install your packages on master server
# yum install -y ansible-2.9.9-1.el7.ans.noarch.rpm
# yum install -y python2-jmespath-0.9.0-3.el7.noarch.rpm
# yum install -y python-httplib2-0.9.2-1.el7.noarch.rpm
# yum install -y python-paramiko-2.1.1-4.el7.noarch.rpm
# yum install -y python-passlib-1.6.5-2.el7.noarch.rpm
# yum install -y sshpass-1.06-2.el7.x86_64.rpm

* Check ansible:
- ansible --version

6. Setup hostname client server to a ansible host on master server
# vi /etc/ansible/hosts
[project-hore]
master
client-1
client-2

7.  Copy the key to a master server 
- press enter until finish
# ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ylo/.ssh/id_rsa): mykey
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in mykey.
Your public key has been saved in mykey.pub.
The key fingerprint is:
SHA256:GKW7yzA1J1qkr1Cr9MhUwAbHbF2NrIPEgZXeOUOz3Us ylo@klar
The key's randomart image is:
+---[RSA 2048]----+
|.*++ o.o.        |
|.+B + oo.        |
| +++ *+.         |
| .o.Oo.+E        |
|    ++B.S.       |
|   o * =.        |
|  + = o          |
| + = = .         |
|  + o o          |
+----[SHA256]-----+

8. Ping master server to ansible client host until all hosts are successfully pinged
# ansible project-hore -m ping -u root

master | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
client-1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
client-2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}

* Finish
