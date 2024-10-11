Vagrant.configure("2") do |config|
    config.vm.box = "archlinux/archlinux"
    
    # Set up port forwarding
    config.vm.network "forwarded_port", guest: 5000, host: 8080
    
    # Provision with shell commands to install packages and set up Flask
    config.vm.provision "shell", inline: <<-SHELL
      sudo pacman -Syu --noconfirm git nano vim python python-virtualenv python-pip
      cd /vagrant
      python -m venv flask_venv
      source flask_venv/bin/activate
      pip install Flask
    SHELL
    
    # Provision to upload the hello.py file to the VM
    config.vm.provision "file", source: "./hello.py", destination: "~/hello.py"
  end
  