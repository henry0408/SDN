This is for lab1 material, which is a preparation for configuring Mininet VM.


## Step 1. Download Mininet:
From https://github.com/mininet/mininet/releases, choose and download mininet-2.3.0-210211-ubuntu-16.04.6-server-i386-ovf.zip
## Step 2. Download VirtualBox:
From http://www.virtualbox.org/wiki/Downloads

![image](https://user-images.githubusercontent.com/58734009/184638211-f0f82035-7486-4904-a0ed-606c933ec8f1.png)

## Step 3. Import Mininet into VirtualBox

## Step 4. (Optional) Donwload and install Putty and Xming for Windows

### 1. Install Xming:
  1. Click "XLaunch", click next page until: 
  
    ![image](https://user-images.githubusercontent.com/58734009/184642711-8abd1c0b-2ab6-423b-ad23-09e899de3ce9.png)
    
  2. Click "Save Configuration" and the path should be the same as your Xming.
    As for me, it is at Program Files (x86) then Xming:
    
    ![image](https://user-images.githubusercontent.com/58734009/184642942-ef01d14b-bd64-4eaa-a974-88442302de45.png)
    
### 2. Install Putty
  

## Step 5. (Optional but recommand) If you donnot want to use Putty and Xming, you can download and set up a Ubuntu 16.04 VM in the VirtualBox

`Step 4 or Step 5 will be used in Step 8`

## Step 6. Set up VM

### 1. Run the Mininet VM and choose File --> Perference

![image](https://user-images.githubusercontent.com/58734009/184639530-76a17efe-144f-4cba-89d6-0612033a891f.png)

### 2. Click on the “Network” icon in the Preferences panel to add a new network adapter

### 3. In "Settings", select “Adapter 2” tab and, in the “Attached to:” field, select “Host-only network”. Click the OK button and start the Mininet VM.

![image](https://user-images.githubusercontent.com/58734009/184640088-32d07d1f-7f01-40cf-80ab-e2e87db9c072.png)

## Step 7. Log in to VM

### 1. Note that the initial username and password are both: mininet

### 2. Type "ifconfig" to show a list of available interfaces on Mininet VM
We do not see an interface that is connected to the host-only interface, we need to configure eth1.

### 3. Type "ifconfig -a" to see all the availabel interfaces
Now we can see three interfaces: lo, eth0 and eth1. But eth1 is not up and does not have an IP address assigned

### 4. Type "sudo dhclient eth1" to assign an IP address to an interface ("eth1")

### 5. Verify, run the ifconfig command again

Now you can see the eth1 interface has been assigned an IP address

![image](https://user-images.githubusercontent.com/58734009/184641296-52462f0d-442e-4d1c-9aa6-1a03f0fa6326.png)

## Step 8. Use SSH to connect Mininet VM
There will be two optionals for Windows users, but I recommend to use the second method.

### Method 1: Excute Xming and remote login the Mininet using PuTTY:

  1. Excute Xming (check your status bar on your PC)
  2. Excute PuTTY
  
   ![image](https://user-images.githubusercontent.com/58734009/184643618-c87c1c61-68c6-4485-9465-b44616f1c188.png)

  3. Enter the IP address for eth0
    
   ![image](https://user-images.githubusercontent.com/58734009/184643699-2936c067-fe09-4b92-a2c1-dbf38fef0029.png)
    
    `Note that the IP address should be the same as you have seen using "ifconfig" in Mininet VM:`
    
   ![image](https://user-images.githubusercontent.com/58734009/184644030-cd136f69-f04b-47a3-aaaf-a222b1389ac0.png)

  4. Click SSH and click the "Enable X11 forwarding" box, then click "Open"
    
   ![image](https://user-images.githubusercontent.com/58734009/184644056-5ea55c5c-6c9a-44b4-af38-14184b7f3cf2.png)
    
    
    
  5. Enter your username and password for Mininet and you can successfully
    
   ![image](https://user-images.githubusercontent.com/58734009/184644229-4fb3e354-1144-4ce6-a47e-b1f02cc257d1.png)

### Method 2: Remote the Mininet using Ubuntu

  1. After installing the Ubuntu on any VM (VituralBox or VMWare), excute it
  
  2. In terminal, type "dpkg -l|grep ssh" and check if there is a SSH sever

  3. If not:
  
    1) sudo apt-get update
    
    2) sudo apt-get upgrade
    
    3) sudo apt-get install -y openssh-server

## Step 9.

In Ubuntu terminal, type "ssh –X mininet@192.168.56.101", and you will login to Mininet VM.
