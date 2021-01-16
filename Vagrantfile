Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = "4"
    vb.memory = "4096"
  end
  config.vm.provision "shell", inline: <<-SHELL
    # Add an extra link to the sync folder.
    ln -s /vagrant /src

    apt-get update
    apt-get install -y apt-transport-https ca-certificates gnupg

    curl -sL https://deb.nodesource.com/setup_lts.x | bash -
    apt-get install -y nodejs

    apt-get install -y docker.io
    systemctl enable --now docker
    usermod -aG docker vagrant

    apt-get install -y kubectl

    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    apt-get update
    apt-get install -y google-cloud-sdk

    npm install -g firebase-tools
  SHELL
end
