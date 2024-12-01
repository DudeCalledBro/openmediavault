# OpenMediaVault

[![CI](https://github.com/DudeCalledBro/openmediavault/actions/workflows/ci.yml/badge.svg)](https://github.com/DudeCalledBro/openmediavault/actions/workflows/ci.yml)

This repository contains my Ansible deployment for OpenMediaVault - an opensource network attached storage solution. Therefore i am using two Raspberry Pi 5 with the Radxa Penta SATA HAT and some SSDs.

**Important!** The installation of OpenMediaVault is currently only supported on Debian Linux (See [docs](https://docs.openmediavault.org/en/stable/)).

## Prerequisites

- Ensure you have Ansible installed (e.g. `pip3 install ansible`)
- **Development**: Install the pip packages listed in [requirements.txt](requirements.txt)

## Installation

The installtion is described without any custom configurations which must be made (e.g. boot-config for the SATA HAT) in order to get your hardware working.

1. Copy the `example.inventory.yml` file to `inventory.yml` and setup setup a variables file for your configuration. Therefore you have to `copy example.config.yml` to `config.yml`. Also have a look into the roles defaults.

2. Run the Ansible playbook to deploy OpenMediaVault

```bash
ansible-playbook play-omv.yml
```

3. (**Optional**) Install OpenMediaVault Extras (e.g. ZFS-Support). Read more about the OMV-Extras [here](https://wiki.omv-extras.org/).

```bash
ansible-playbook play-omv-extras.yml
```

4. Open a new Browser Window and navigate to the OpenMediaVault GUI

    * URL: `http://omv.local`
    * Username: `admin`
    * Password: `openmediavault`

    **Important!** Change the default OpenMediaVault admin password immediately!

## Additional

To get the Radxa Penta SATA HAT working on the Raspberry Pi 5, you need to configure some boot options. Therefore you can use my Raspberry Pi ansible configuration role [here](https://github.com/DudeCalledBro/ansible-role-rpi).

```yaml
rpi_config:
- regexp: "^#?dtparam=pciex1$"
  line: "dtparam=pciex1"
- regexp: "^#?dtparam=pciex1_gen"
  line: "dtparam=pciex1_gen=3"
```

## License

Copyright © 2024 Niclas Spreng

Licensed under the [MIT license](LICENSE).
