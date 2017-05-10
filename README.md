# Demo of CI/CD pipeline

## What's it do?

The playbooks here will setup the following:
- a jenkins server with
  - specific jobs pre-configured
  - packer installed
  - vmware workstation installed
- enable building of packer images
- enable pushing those images to vsphere
- enable operating on resulting vms using these playbooks


## Getting Started

```bash
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

mkdir pipeline
cd pipeline
repo init -g pipeline -u git@github.com:VMware-PSO-DevOps-CNA/devops-pipeline-demo.git
repo sync

cd playbooks
```

Edit the `inventory` file as needed

```text
# these hosts will get packer, vmware workstation,
# and tools needed for pushing images to vsphere
[packer]
10.153.252.224
192.168.1.115
192.168.1.84

# These hosts will get jenkins installed and confiigured.
# Add them to the packer group if building packer images
[jenkins]
192.168.1.84

# Machines that will download and host any needed binaries.
[assets]
192.168.1.115
```

Deploy all the things:

```bash
ansible-playbook  -i inventory  site.yml
```

See individual playbooks for various smaller chunks.
