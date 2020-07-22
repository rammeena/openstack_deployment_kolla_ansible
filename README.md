# openstack_deployment_using_kolla_ansible

# Prepare Python 3 Virtual Environment for kolla-ansible

- clone this repo in home directory of installer host

- make sure installer host uses '/usr/libexec/platform-python' instead of /usr/bin/python.
  check with below commands:
   - which python
    # there shold be no python on CentOS8 systems

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
  mkdir /etc/ansible/ansible.cfg
  [defaults]
  host_key_checking=False
  pipelining=True
  forks=100

- Now Copy kolla-ansible config files from this repo to /etc/kolla directory
  mkdir /etc/kolla
  cp -v globals.yml /etc/kolla/
  cp -v passwords.yml /etc/kolla/
  cp -vr config /etc/kolla/

- Copy inventory file multinode at location where you want to run kolla ansible commands.

- Now run kolla ansible precheck command or ansible ping command to check if things are working.
