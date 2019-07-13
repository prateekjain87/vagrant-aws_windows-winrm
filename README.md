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

6. Setup Ansible.
