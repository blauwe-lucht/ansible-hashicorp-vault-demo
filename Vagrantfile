Vagrant.configure(2) do |config|
    config.vm.define "acs" do |acs|
        acs.vm.box = "bento/ubuntu-22.04"
        acs.vm.hostname = "acs"
        acs.vm.network "private_network", ip: "192.168.14.8"

        # Make sure all sensitive info is only readable by user.
        acs.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]    

        acs.vm.provision "shell" do |shell|
            shell.inline = <<-SHELL
                set -euxo pipefail

                export DEBIAN_FRONTEND=noninteractive
                apt-get update
                apt-get upgrade -y

                apt-get install -y python3.10-venv

                # Pip prefers to run in a virtual environment, so we create one for the vagrant user
                # and use that pip to install ansible and ansible-lint.
                sudo -u vagrant bash -c '
                    set -euxo pipefail

                    python3.10 -m venv /home/vagrant/venv-ansible
                    . /home/vagrant/venv-ansible/bin/activate
                    pip install --upgrade pip
                    pip install ansible ansible-lint

                    # Make sure we are always using python from the virtual environment.
                    echo ". ~/venv-ansible/bin/activate" >> ~/.bashrc
                '
            SHELL
        end
    end

    config.vm.define "vault" do |vault|
        vault.vm.box = "bento/ubuntu-22.04"
        vault.vm.hostname = "vault"
        vault.vm.network "private_network", ip: "192.168.14.9"
    end
end
