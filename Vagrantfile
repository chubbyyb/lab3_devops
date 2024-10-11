Vagrant.configure("2") do |config|
  config.vm.box = "archlinux/archlinux"
  
  # Port forwarding from the VM's port 5000 to host's port 8080
  config.vm.network "forwarded_port", guest: 5000, host: 8080
  
  # Provision with shell commands
  config.vm.provision "shell", inline: <<-SHELL
    # Install necessary packages
    sudo pacman -Syu --noconfirm git nano vim python python-virtualenv python-pip
    
    # Navigate to the home directory
    cd ~
    
    # Set up a virtual environment in the home directory
    python -m venv flask_venv
    source flask_venv/bin/activate
    
    # Install Flask within the virtual environment
    ~/flask_venv/bin/pip install Flask
    
    # Move hello.py to the home directory from /vagrant
    cp /vagrant/hello.py ~/hello.py
    
    # Start the Flask application
    nohup ~/flask_venv/bin/flask --app ~/hello run --host=0.0.0.0 &
  SHELL
  
  # Upload hello.py to the VM's /vagrant directory initially
  config.vm.provision "file", source: "./hello.py", destination: "/vagrant/hello.py"
end
