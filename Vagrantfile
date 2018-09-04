Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/xenial64"

  # To automatically configure a private network uncomment following line.
   config.vm.network "private_network", ip: "192.168.33.30"

  config.vm.provider "virtualbox" do |vb|
  # Customize the amount of memory on the VM:
     vb.memory = "4024"
  end

  # Port forwarding: If unneeded comment or remove following lines
  config.vm.network "forwarded_port", guest: 80, host: 8001
  config.vm.network "forwarded_port", guest: 8000, host: 8000
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provision "shell", inline: <<-SHELL
    add-apt-repository ppa:openjdk-r/ppa -y
    apt-get update
	
	echo "\n----- Installing Apache and Java 8 ------\n"
    apt-get -y install apache2 openjdk-8-jdk
    update-alternatives --config java
	
	echo "\n ---Downloading resources for Jenkins --- "
	wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
	sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
	sudo apt-get update && sudo apt-get upgrade
	echo "\n --- Installing Jenkins -- "
	
	sudo apt-get install -y jenkins
	
  SHELL
end