# Enable multiple ceph backend for cinder

# 2 Ceph Clusters:
    - nvme cluster
    - ssd cluster

# nvme ceph cluster
this is the default backend for nova and cinder.
This for performance oriented application

# ssd ceph cluster:
this is the default backen for glance.
extra backend for cinder .
this is for common applications.

# To enable this extra backend below files were modified
# in kolla-ansible source code.

/root/.venvs/kolla/share/kolla-ansible/ansible/roles/cinder/templates/cinder-volume.json.j2
/root/.venvs/kolla/share/kolla-ansible/ansible/roles/cinder/templates/cinder.conf.j2
/root/.venvs/kolla/share/kolla-ansible/ansible/roles/cinder/tasks/external_ceph.yml

# Nova change for ceph multi backend rbd2 cinder
/root/.venvs/kolla/share/kolla-ansible/ansible/roles/nova-cell/tasks/external_ceph.yml

# Note:
```Before preparing cluster make sure you make these changes in kolla-ansible source code.```

# Also globals.yml was modified to include extra variable for multi backend.
