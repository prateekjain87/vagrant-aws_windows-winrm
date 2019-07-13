Vagrant.configure(2) do |config|
 config.vm.box = "dummy"
 config.vm.provider :aws do |aws, override|
   aws.access_key_id = "AKIAJPLJSOKOCOYWDIYA"
   aws.secret_access_key = "hDayyHmbvUEt3U4CAeBrNjNKObSynSb7+Vh2rNqH"
   aws.keypair_name = "prateek"
   aws.ami = "ami-08ffedbc0cfe344ac"
   aws.region = "ap-south-1"
   aws.instance_type = "t2.micro"
   aws.security_groups = ['default']
  
   aws.user_data = File.read("user_data.txt")
   
   override.nfs.functional = false
   override.winrm.username = "Administrator"
   override.winrm.password = "VagrantRocksInAWSec2"
   override.vm.communicator = :winrm
 end
 config.vm.provision "ansible_local" do |ansible|
   ansible.playbook = "playbook.yml"
 end
end

