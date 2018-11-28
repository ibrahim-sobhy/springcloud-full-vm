VAGRANTFILE_API_VERSION = "2"

# Start to configure the virtual machine which will have the ful development
# You can run vagrant up on the same level of this file
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    # It will be based on ubuntu to run docker safely and easy
    config.vm.box = "ubuntu/trusty64"

    # Define the shared folder between the host OS and the virtual machine 
    # (docker provider also will auto configured based on that)
    config.vm.synced_folder ".", "/vagrant" # Share the current host path with /vagrant pathon vm

    # Define the forwared ports from the virtual machine to the host
    # You can get the exposed ports from each component as below then
    # Define to which port on the host OS (you have to restart the vm)
    config.vm.network "forwarded_port", guest:8761, host: 8761 # JHipster Registry
    config.vm.network "forwarded_port", guest:5601, host: 5601 # JHipster Consol
    config.vm.network "forwarded_port", guest:9411, host: 9411 # Zipkin

    # Configure the provider properties of the virutal machine
    config.vm.provider "virtualbox" do |vb|
        vb.gui = false # No GUI to be displayed
        vb.name = "spring-cloud-devbox"
        vb.memory = 4096 # 4 GB RAM
        vb.cpus = 1
    end

##############################################################################################
##### Start to configure the dockers for each component of the system ########################
##############################################################################################

    #################################################################
    # Non Functional components

    # Microservices services
    #   1. Config Service
    #   2. Eureka Service
    #   3. Gateway
    #   4. Authentication Service
    config.vm.provision "docker" do |d|
        # 1. Config Service
        # 2. Eureka Service
        d.pull_images "jhipster/jhipster-registry"
        d.run "jhipster/jhipster-registry",
            args: "-p 8761:8761"
        
        # 3. Gateway
        # 4. Authentication Service
    end

    # ELK
    #   1. Elastic Search
    #   2. Kibana
    #   3. Zipkin
    #   4. Kafka
    #   5. Rabbit MQ
    config.vm.provision "docker" do |d|
        # 1. Elastic Search
        # 2. Kibana
        # 3. Zipkin
        d.pull_images "jhipster/jhipster-console"
        d.run "jhipster/jhipster-console",
            args: "-p 5601:5601 -p 9411:9411"
    end

    config.vm.provision "shell" do |sh|
        sh.path = 'provisioning/install-docker-compose.sh'
    end

    config.vm.provision "shell" do |sh|
        sh.inline = 'docker-compose -f /vagrant/docker/docker-compose.yml up -d --build'
    end

    # DevOps
    #   1. Jenkins
    #   2. Maven Repo
    #   3. Docker Repo
    #   4. Monitor Dashboard
end 
    