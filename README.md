# openstack_deployment_using_kolla_ansible

- dnf install git -y

- cat .ssh/config
  Host *
    StrictHostKeyChecking no
    UserKnownHostsFile /dev/null
    User centos

  Host github.com
        Hostname ssh.github.com
        Port    443

- clone this repo in home directory of installer host
  git clone git@github.com:rammeena/openstack_deployment_kolla_ansible.git

- make sure installer host uses '/usr/libexec/platform-python' instead of /usr/bin/python.
  check with below commands:
   - which python  # it returns no python found.
     there should be no python on CentOS8 systems, it has its inbuilt python interpreter.

   - it could that default python is setup using alternatives command, remove it.
     alternatives --list
     alternatives --remove python /usr/bin/python3

- Now install dependencies to run kolla-ansible.
  dnf install python3-devel libffi-devel gcc openssl-devel python3-libselinux

- Now create python3 virtual Environment
  mkdir  ~/.venvs
  python3 -m venv .venvs/kolla
  source .venvs/kolla/bin/activate
  pip install -U pip
  pip install ansible
  pip install kolla-ansible

- create ansible config file
  mkdir /etc/ansible
  vim /etc/ansible/ansible.cfg
  [defaults]
  host_key_checking=False
  pipelining=True
  forks=100

- Now Copy kolla-ansible config files from this repo to /etc/kolla directory
  mkdir /etc/kolla
  mkdir /etc/kolla/config
  cp -v node_custom_config/globals.yml /etc/kolla/
  cp -v node_custom_config/passwords.yml /etc/kolla/
  cp -vr node_custom_config/* /etc/kolla/config/

- Copy inventory file multinode at location where you want to run kolla ansible commands.

# Follow instruction in node_custom_config/README.md

- Now run kolla ansible precheck command or ansible ping command to check if things are working.
