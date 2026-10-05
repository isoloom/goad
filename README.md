<div align="center">
  <h1><img alt="GOAD (Game Of Active Directory)" src="./docs/mkdocs/docs/img/logo_GOAD3.png"></h1>
  <br>
</div>

**GOAD (v3)**

:bookmark: Documentation : [https://orange-cyberdefense.github.io/GOAD/](https://orange-cyberdefense.github.io/GOAD/)

## Run GOAD-Light with Isoloom

This fork describes GOAD-Light once, in [`isoloom.yml`](isoloom.yml)
([Isoloom](https://www.isoloom.com)): three Windows Server 2019 machines (`dc01`, `dc02`, `srv02`)
on one network, WinRM prepared on each, then GOAD's own Ansible playbooks run from a controller VM
with the GOAD-Light inventory. Isoloom generates the Vagrant files (`.isoloom/vagrant/`).

```bash
isoloom generate
cd .isoloom/vagrant && vagrant up
```

Built end to end this way on VirtualBox: `sevenkingdoms.local` on KINGSLANDING, the child domain
`north.sevenkingdoms.local` on WINTERFELL, CASTELBLACK joined, with MSSQL and IIS, and no failed
task. Fixes made on the way (in `ansible/roles/`):

- `child_domain`: any error reading the child domain counts as "not created yet" (an unanswered
  AD Web Services call stopped the promotion silently); a failed promotion now fails the task; a
  stale NTDS database from a failed attempt is removed before retrying; the NAT adapter's DNS
  points at the parent DC during the promotion (8524 DNS lookup failures otherwise).
- `mssql`: Microsoft's permanent download link (the direct SQL Server 2019 Express path is gone).
- `mssql_ssms`: SSMS 20 from Microsoft's permanent link (the SSMS link now serves SSMS 21, whose
  installer fails on Windows Server 2019).

Needs about 13 GB of memory: 11.7 GB for the three Windows VMs (`isoloom resources`), 1 GB for the controller.

## Description
GOAD is a pentest active directory LAB project.
The purpose of this lab is to give pentesters a vulnerable Active directory environment ready to use to practice usual attack techniques.

> [!CAUTION]
> This lab is extremely vulnerable, do not reuse recipe to build your environment and do not deploy this environment on internet without isolation (this is a recommendation, use it as your own risk).<br>
> This repository was build for pentest practice.

![goad_screenshot](./docs/img/goad_screenshot.png)

## Licenses
This lab use free Windows VM only (180 days). After that delay enter a license on each server or rebuild all the lab (may be it's time for an update ;))

## Available labs

- GOAD Lab family and extensions overview
<div align="center">
<img alt="GOAD" width="800" src="./docs/img/diagram-GOADv3-full.png">
</div>

- [GOAD](https://orange-cyberdefense.github.io/GOAD/labs/GOAD/) : 5 vms, 2 forests, 3 domains (full goad lab)
<div align="center">
<img alt="GOAD" width="800" src="./docs/img/GOAD_schema.png">
</div>

- [GOAD-Light](https://orange-cyberdefense.github.io/GOAD/labs/GOAD-Light/) : 3 vms, 1 forest, 2 domains (smaller goad lab for those with a smaller pc)
<div align="center">
<img alt="GOAD Light" width="600" src="./docs/img/GOAD-Light_schema.png">
</div>

- [MINILAB](https://orange-cyberdefense.github.io/GOAD/labs/MINILAB/): 2 vms, 1 forest, 1 domain (basic lab with one DC (windows server 2019) and one Workstation (windows 10))

- [SCCM](https://orange-cyberdefense.github.io/GOAD/labs/SCCM/) : 4 vms, 1 forest, 1 domain, with microsoft configuration manager installed
<div align="center">
<img alt="SCCM" width="600" src="./docs/img/SCCMLAB_overview.png">
</div>

- [NHA](https://orange-cyberdefense.github.io/GOAD/labs/NHA/) : A challenge with 5 vms and 2 domains. no schema provided, you will have to find out how break it.
<div align="center">
<img alt="SCCM" width="600" src="./docs/img/logo_NHA.jpeg">
</div>

- [DRACARYS](https://orange-cyberdefense.github.io/GOAD/labs/DRACARYS/) : A challenge with 3 vms and 1 domains. no schema provided, you will have to find out how break it.
<div align="center">
<img alt="SCCM" width="600" src="./docs/img/dracarys_logo.png">
</div>