1. Install Vagrant

#yum -y install https://releases.hashicorp.com/vagrant/1.9.6/vagrant_1.9.6_x86_64.rpm (RHEL 7)

2. Install Plugins (Ruby will be required):

Vagrant-aws 

vagrant plugin install –plugin-version 1.0.1 fog-ovirt

vagrant-share

vagrant-winrm-syncedfolders


E.g. vagrant plugin install vagrant-share



3. Add dummy box

vagrant box add dummy https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box


4. Get AWS info:
https://anzpiper.blogspot.com/2017/08/use-vagrant-to-deploy-to-aws.html
http://www.riturajcse.com/2017/12/using-ansible-for-deploying.html

5. Powershell (WinRM setup):
https://gist.github.com/mkubenka/33b542cbd82614fe7f8b#file-vagrantfile-L1
(Only user_data.txt file required)

6. Setup Ansible: Preferably using pip.

7. Winrm password and username can be changed by editing user_data.txt lines:
	$user = [adsi]"WinNT://$ComputerName/Administrator,user"
	$user.setpassword("VagrantRocksInAWSec2")

7. Finally run: vagrant up





Common Errors:

1. While installing aws-plugin, ruby related issues might come. Look if ruby is installed or 

2. One issue might be time syncing: Even though credentials would be correct, authentication error can come. Try syncing time using NTP.

3. Most common issue is "waiting for ssh". In that case, check if port 22 is open in the choosen security group in Vagrantfile.

4. {"failed": true, "msg": "winrm or requests is not installed: cannot import name UnrewindableBodyError"}"
	a. install pywinrm and requests using pip with version of ansible installed specified
		pip install ansible==2.7 pywinrm
		pip install ansible==2.7 requests

	b. That error may indicate that `winrm` library cannot locate the `requests` library. Try python -c 'import requests'.If it doesnt work try performing `pip install -I requests.





Note: 

All other information related to instance and how to access that instance is stated in a hidden file in same directory where Vagrantfile is situated under provisioner directory like-
.vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory 

We need not worry about stuffs like IP address, ansible user, password etc. Everything needed will be automatically set.





You might be pondering: Why winrm over ssh?

You may know that the way to connect to a Windows ec2 instance is different from UNIX instances method. The reason is it is not possible to SSH to a Windows instance out of the box. However you can install a SSH server on the Windows instance and do the necessary configurations (Open SSH port from Windows firewall, Make ssh-daemon service automatically starting up, etc) and make it possible to SSH.

OpenSSH is one such SSH server that can be used with Windows. You can get the MSI installer from this page. The good thing with OpenSSH is that you don’t need to do any manual configuration; the installer does them all. So once you successfully complete the installing wizard, you can SSH from a remote location.

Windows Remote Management is a powerful feature to administer your Windows systems remotely. WinRM is enabled by default on all Windows Server operating systems (since Windows Server 2012 and above), but disabled on all client operating systems like Windows 10, Windows 8 and Windows 7.


