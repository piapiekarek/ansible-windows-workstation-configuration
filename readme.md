# Ansible Windows workstation configuration

This Ansible playbook is an example for automated software installation. It is used to configure my Workstation.

## Requirements for Ansible host
The ansible host has to be a Linux machine. For the case that only a Windows (10!!!) Machine is availible, [install the Linux Subsystem](https://docs.microsoft.com/en-us/windows/wsl/install-win10) on the device.

Afterwards install pywinrm:

``` bash
## for debian and ubuntu
sudo apt-get install python3-winrm
## for fedora
sudo dnf install python3-winrm
```

## WinRM Setup

To access the client machines from remote winrm is used.

[Windows setup guide, see Chapter Setup WinRM](https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html)

Run as administrator in powershell!

``` powershell
$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)

powershell.exe -ExecutionPolicy ByPass -File $file
```
## Requirements for yml file
Change ansible_user and ansible_password in the vars section before running the script!

## Run on Ansible host

``` bash
ansible-playbook \
  windows-rtlab-test.yml \
  -i "<ip-address>," --user "<user_name>" --ask-pass

  #ansible-playbook windows-rtlab-test.yml -i "192.168.120.235," --user "John Doe" --ask-pass
```


Warning: The command above needs a comma separated list of arguments, thus the comma at the end of the IP Address.

instead of passing the arguments in the command line, you can set them inside the yml file (uncomment the lines ansible_user and ansible_password, and set both)
Afterwards run the following command:

``` bash
ansible-playbook \
  windows-rtlab-test.yml \
  -i "192.168.120.235,"

  #ansible-playbook windows-rtlab-test.yml -i "192.168.120.235,"
```

## Using inventory

Instead of passing the ip-addresses as arguments, they can be written into the inventoryfile (default: `/etc/ansible/hosts`)
```bash
# IP without any group
192.168.120.144

[group_name_1]
192.168.120.48
192.168.120.77

[group_name_2]
192.168.120.77 #same IP linke in Group group_name_1
192.168.120.79
192.168.120.119
```
Afterwards, the following shell commands can be used:
```bash
$ ansible-playbook <File_Name>
# or with a group
$ ansible-playbook <File_Name> -l group_name_1
```

## Alternatives

https://www.opsi.org/
