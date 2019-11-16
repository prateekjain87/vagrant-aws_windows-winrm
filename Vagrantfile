Vagrant.configure(2) do |config|
 config.vm.box = "dummy"
 config.vm.provider :aws do |aws, override|
   aws.access_key_id = ""
   aws.secret_access_key = ""
   aws.keypair_name = ""
   aws.ami = ""
   aws.region = ""
   aws.instance_type = ""
   aws.security_groups = ['']

   aws.user_data = File.read("usertext.txt")

   override.nfs.functional = false
   override.winrm.username = "Administrator"
   override.winrm.password = "VagrantRocksInAWSec2"
   override.vm.communicator = :winrm
 end
 config.vm.provision "ansible" do |ansible|
   ansible.playbook = "playbook.yml"
 end
end
