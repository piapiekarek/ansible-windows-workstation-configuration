# Lab ansible cad-workstation configuration

This Ansible playbook is an example for automated software installation. It is used to configure CAD-Workstations in the Lab.

## Requirements for Ansible host

On Linux install pywinrm:

``` bash
sudo dnf install python3-winrm
```

## WinRM Setup

To access the client machines from remote winrm is used.

[Windows setup guide](https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html)

Run as administrotor in powershell!

``` powershell
$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)

powershell.exe -ExecutionPolicy ByPass -File $file
```

## Run

``` bash
ansible-playbook \
  windows-rtlab-test.yml \
  -i "192.168.120.235,"
```

## Alternatives

https://www.opsi.org/