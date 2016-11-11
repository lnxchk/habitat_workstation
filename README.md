# Habitat Workstation

Cookbooks and Packer config to create a workstation for use during Habitat training.

## Current Amazon Machine Image IDs

Listing AMIs for us-east-1 and eu-west-1

Name|us-east-1|eu-west-1
----|---------|---------
Introduction to Habitat Workstation - RedHat 7|ami-faac8bed|ami-3ad68049
Introduction to Habitat Workstation - Ubuntu 14.04|ami-a62c6cb1|ami-3837664b
Introduction to Habitat Workstation - Ubuntu 16.04|ami-fdf7b7ea|ami-cd3a6bbe
Habitat Workstation - RedHat 7 - with hab 0.11.0 installed|ami-6bad8a7c|ami-a83968db
Habitat Workstation - Ubuntu 14.04 - with hab 0.11.0 installed|ami-47d5f250|ami-463b6a35
Habitat Workstation - Ubuntu 16.04 - with hab 0.11.0 installed|ami-ccfadddb|ami-453b6a36

## Build the Amazon Machine Images (AMIs)

not currently supported for eu-west-1

### Without Habitat installed

`$ packer build packer/rhel-7.json`

`$ packer build packer/ubuntu-1404.json`

`$ packer build packer/ubuntu-1604.json`

### With Habitat installed

The latest version of Habitat will be installed.  The version number should be specified in the AMI name.  The template expects a `hab_version` variable is set.

You can set this manually using the commands below, assuming the latest version is 0.10.2.

`$ packer build -var "hab_version=0.10.2" packer/rhel-7-hab-installed.json`

`$ packer build -var "hab_version=0.10.2" packer/ubuntu-1404-hab-installed.json`

`$ packer build -var "hab_version=0.10.2" packer/ubuntu-1604-hab-installed.json`

If you have the latest version of Habitat installed, you can use these commands instead.

`$ packer build -var "hab_version=$(hab --version | cut -d "/" -f1)" packer/rhel-7-hab-installed.json`

`$ packer build -var "hab_version=$(hab --version | cut -d "/" -f1)"  packer/ubuntu-1404-hab-installed.json`

`$ packer build -var "hab_version=$(hab --version | cut -d "/" -f1)"  packer/ubuntu-1604-hab-installed.json`

## Share the AMIs with other Amazon accounts

```bash
$ export AMI_ID=the_ami_id_generated_by_packer
$ rake ami:share
```

## Build out Workstations for a Classroom

```bash
$ export AMI_ID=the_ami_id_generated_by_packer
$ build_habitat_workstations.sh [number] [name] [department] [contact] [project] [termination-date]
```

e.g.
```bash
$ export AMI_ID=the_ami_id_generated_by_packer
$ build_habitat_workstations.sh 20 "Surge Conf 2016" "Community Engineering" "Nathen Harvey" "Surge" "2016-09-23"
```

For EU:
```
$ export AMI_ID=the_ami_id_generated_by_packer
$ build_habitat_workstations_eu.sh [number] [name] [department] [contact] [project] [termination-date]
```



## List Workstations for a Classroom

```
$ export AMI_ID=the_ami_id_generated_by_packer
$ show_running_instances.sh
```
