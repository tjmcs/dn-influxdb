# dn-influxdb
Playbooks/Roles used to deploy InfluxDB

# Installation
To install InfluxDB using the `site.yml` playbook in this repository, first clone the contents of this repository to a local directory using a command like the following:
```bash
$ git clone --recursive https://github.com/Datanexus/dn-influxdb
```
That command will pull down the repository and it's submodules (currently the only dependency embedded as a submodule is the dependency on the `https://github.com/Datanexus/common-roles` repository).

# Use
To run the included playbook, change directories to the `dn-influxdb` subdirectory and run a set of commands that look something like the following (the commands shown here will install the most recent version of the InfluxDB distribution from the main InfluxData package repository, for example, onto a machine with at the IP address "192.168.34.10"):
```bash
$ export INFLUXDB_ADDR="192.168.34.10"
$ echo "[all]\n${INFLUXDB_ADDR}" > hosts
$ ansible-playbook site.yml --inventory-file hosts
```

# Assumptions
It is assumed that this playbook will be run on a recent (systemd-based) version of RHEL or CentOS (RHEL-7.x or CentOS-7.x, for example); no support is provided for other distributions (and the `site.xml` playbook will not run successfully).  The example shown above also assumes that some (shared-key?) mechanism has been used to provide access to the InfluxDB host from the Ansible host that the ansible-playbook is being run on (if not, then additional arguments might be required to authenticate with that host from the Ansible host that are not shown in the example `ansible-playbook` commands shown above).

# Deployment via vagrant
The included Vagrantfile can be used to deploy kafka to a VM using `Vagrant`.  From the top-level directory of this repostory a command like the following will (by default) deploy kafka to a CentOS 7 virtual machine running under VirtualBox (assuming that both vagrant and VirtualBox are installed locally, of course):
```bash
$ VAGRANT_DEFAULT_PROVIDER=virtualbox vagrant -i="192.168.34.10" up
```
Note that the `-i` (or the corresponding `--influxdb-addr`) flag must be used to pass an IP address into the Vagrantfile (this IP address will be used as the IP address of the InfluxDB server that is created by the vagrant command shown above).
