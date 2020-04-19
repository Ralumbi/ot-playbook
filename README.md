<p align="center"> <a href="https://worldofcoding.net/" target="_blank" rel="noopener"> <img width=300px height=200px src="https://worldofcoding.net/worldofcoding.png" alt="WorldofCoding"></a> </p>

<h3 align="center">OT-Playbook Automatic Server Installation</h3>

---

<p align="center"> This project is made for the ease of installing your ubuntu 20.04 lts server optimized for tibia otserver hosting without breaking your head. This playbook should work from ubuntu 16.04 lts up to 20.04 lts. <br> </p>

## 📝 Table of Contents

* [About](#about)
* [Configure](#configure)
* [Deployment](#deployment)
* [Usage](#usage)
* [Built Using](#built_using)
* [Authors](#authors)

## 🧐 About <a name = "about"></a>

The project started with the idea I've gotten from <a href="https://github.com/DevelopersPL/" target="_blank">DevelopersPL</a> which made the very first version of such playbook tibia otserver related. The reason I have made a new one is because I've been working with many different servers. The needs were getting very huge as in many server installs and testing new server company's. Installing a complete server over and over manually gets you freaked out so I needed something which was just having what I demanded to have. Where the one which was already out there having too many extra's up for installation.

## 🏁 Getting Started <a name = "getting_started"></a>

We will need to setup ansible on your machine first before we can continue. I will describe on how-to setup ansible on windows and ubuntu linux. When you have got this setup then the rest will be peanuts! 

See [deployment](#deployment) for notes on how to deploy the project on a live system.

Note: Setting up ansible on your own machine is required when you are in need to install multiple servers. Or need to install it many times because you are running virtualbox on your machine to do tests/development in your linux system. Deploying the playbook on just one machine will also be described, but is not recommended. 

### Prerequisites windows

1. Open PowerShell as Administrator and run:

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

2. Restart your computer when prompted.
3. Open the Microsoft Store and search for ubuntu.
4. Install ubuntu 18.04 or higher.

   Once installed you must run it and follow the instruction in the terminal.\
   When everything is setup please continue with the Prerequisites ubuntu below:

### Prerequisites ubuntu

What things you need to install the software and how to install them.

Ansible-Playbook

```
sudo apt update && sudo apt upgrade -y
sudo apt install git
sudo apt install ansible
git clone https://github.com/ralumbi/ot-playbook
cd ot-playbook
```
Now continue with the next steps

## 🔧 Configure the playbook <a name = "configure"></a>

In the hosts file you must configure the server(s) you want to install.

### Break down into pieces

<img src="https://worldofcoding.net/github-img/folder-structure.png" alt="folder-structure">

Open the hosts file there you will see:

vim hosts
```
[setupserver]
IPADDRESSHERE ansible_user=SERVERUSERNAME ansible_sudo_pass=SERVERPASSWORD
```
Press the insert key on your keyboard so you make the file able for editting.
```
change IPADDRESSHERE to the ip-address of your server
change SERVERUSERNAME to your servers username (for example root)
change SERVERPASSWORD to your servers password
```
Now you must press CTRL+C and write :wq after so you will write the changes and quit the file.
We are set now!
## 🎈 Usage <a name="usage"></a>

Pre-sets:
   php version: 7.4

You can change the php version manually by editting the following file:
```
vim roles/setupserver/vars/main.yml
```
You will need to set the php version to the version you will run!
(defaults:
ubuntu 16.04 = 7.0​
ubuntu 18.04 = 7.2​
ubuntu 20.04 = 7.4​
);
(Note: This is on the to-do list to make it automatically search for the php version and set it automatically as well)

- Website location: /home/otadmin/www/public/
- GameServer location: /home/otadmin/forgottenserver/
- Database: http://yourip:2344
- Database password: Login the terminal with the otadmin user. You will find the mysql password in the begin screen.

## 🚀 Deployment <a name = "deployment"></a>

To use the playbook we will need to open the terminal we setup on windows or just open your terminal on ubuntu by CTRL+ALT+T.
- Navigate to the directory. 
- Set the hosts in the file.

Before we can run the playbook we got to open up our ssh connection one-way towards the server.
First we create a ssh key;
```
ssh-keygen
presh enter 3 times (you don't need to protect this key, if you do you have to make sure you save the password to it!!!)
I personally never do.
```
Then we have to copy the public key to the server;
```
ssh-copy-id -i ~/.ssh/id_rsa.pub YOURNAME@YOURSERVER
```
YOURNAME    = your username (example: root)
YOURSERVER  = your servername (example: 127.0.0.1 or domain.com)

Now we simply write:
```
ansible-playbook letsplay.yml -i hosts
```
The server will now install and you will be able to login to the server with:
```
username: otadmin
password: otadmin
```
Once you have logged in for the first time please change your password immediately by typing 'passwd' in the terminal.


## ⛏️ Built Using <a name = "built_using"></a>

* [Ansible](https://www.ansible.com/) - Ansible-Playbook by Redhat
* [Virtualbox](https://www.virtualbox.org/) - Virtualization for Operation-Systems
* [DevelopersPL](https://github.com/developersPL) - othosting-provisioning

## ✍️ Authors <a name = "authors"></a>

* [@ralumbi](https://github.com/ralumbi)
