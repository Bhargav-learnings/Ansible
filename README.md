# Ansible
what and why and how to implemt Ansible

                        ANSIBLE 
                   Similar tools are → Chef, puppet etc..

→ Configuration Management Tool, which helps to automate the tasks on remote servers by using Control
     Node[Master Node]
→ In ansible we call it  Control Node [Master Node]  and  Manage Node [remote servers].
     By using Control nodes we execute the tasks and automates the things on Manage Nodes.
→ We provide instructions to control node to execute on control nodes through Ad Hoc commands
     or playbooks(which are written in yaml).

Inventory is the heart of Ansible, & Inventory is nothing but a file where we mention our remote or manage nodes details.
Ansible will be Installed in Control nodes & no need to install on Manage nodes

Inventory

We can create inventory either in a playbook which is yaml or creating files by ini extension.
We can create inventory in any location of the server but while executing the ansible command we must pass the location of the inventory.ini to execute those on remote servers which are mentioned in inventory.ini.
These are useful when we work multiple requirements so we can create custom inventory.ini and can execute based on the requirement.

If we don't want to pass like this we can use the ansible default path which is   /etc/ansible/hosts,
            if we mention the manage node details here we don't need to specify path of the inventory
            separately because by default ansible takes the managed node details from this location.
We can't mention the playbook in .ini and execute like a Ad hoc commands



Ad hoc commands →

These are useful when we want do simple tasks like installing java or updating packages,
Playbooks → these are useful when we want to do complicated tasks on remote servers, so a playbook is a good option(these are written in yaml, which are sharbale and also we can use it as modules).

          SSH setup for control node and manage node

Login into Control Node & Update the required Packages and Install Ansible.
Create a user if required and create a password.
Create ssh key pair by using command ssh-keygen -t rsa and give enter to store in default location,

Login to manage nodes & update the packages and no need to install ansible.
Edit the /etc/ssh/sshd_config & add the data here 

Protocol 2
PasswordAuthentication yes
ChallengeResponseAuthentication no
UsePAM yes
X11Forwarding no
PrintMotd no
PermitUserEnvironment no
ClientAliveInterval 300
ClientAliveCountMax 0
AcceptEnv LANG LC_*
Subsystem       sftp    /usr/lib/openssh/sftp-server
LogLevel INFO
MaxAuthTries 4
IgnoreRhosts yes
HostbasedAuthentication no
PermitEmptyPasswords yes
MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512,hmac-sha2-256,umac-128@openssh.com
PubkeyAuthentication yes
PermitRootLogin no

Restart ssh → Ubuntu → systemctl restart ssh
                        Linux → systemctl restart sshd

Go back to control Node & now execute ssh-copy-id user@IP of server [pvt or pub]
First time you will be asked password for the login and enter password and you will be logged into server successfully,

Inventory based execution 
Create inventory.ini
We can specify a group as [first-group] and below we can mention the manage node server list with user@IP
Same as we can mention the number of groups and servers and save it.

Now we can execute the Ad hoc commands on this servers mention in .ini by using command 
Ansible -i inventory.ini -m shell -a “touch bhargav” first-group
Now, ansible will execute the command touch bhargav on all servers which are under the first group.

Also we can mention the single server instead of the group name.


