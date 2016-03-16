open_vm_tools
=============

Ansible role which helps to install the Open Source version of the VMware
Tools for RedHat-based guest systems.


Usage
-----

```
# Basic usage of this role
- name: My play
  hosts: all
  roles:
    - open_vm_tools

# Example of how to foce uninstallation of the VMware Tools
- name: My play
  hosts: all
  vars:
    # Force uninstallation of the VMware Tools
    open_vm_tools_uninstall_vt_uninstall_vt: yes
  roles:
    - open_vm_tools

# Example of how to install the VMware deployPkg Tools plug-in
- name: My play
  hosts: all
  vars:
    # Enable installation of the VMware deployPkg Tools plug-in
    open_vm_tools_plugin_deploypkg_install: yes
  roles:
    - open_vm_tools

# Example of how to change the default yumrepo module parameters
# for the VMware deployPkg Tools plug-in YUM repo
- name: My play
  hosts: all
  vars:
    # Overwrite some of the yumrepo parameters
    open_vm_tools_plugin_deploypkg_yumrepo_params:
        gpgcheck: no
  roles:
    - open_vm_tools
```


Role variables
--------------

```
# Whether to uninstall the proprietary VMware Tools installation
open_vm_tools_uninstall_vt: no

# Custom list of packages to uninstall when VMware Tools installed via RPMs
open_vm_tools_uninstall_vt_rpms_pkgs__custom: []

# Default list of packages to uninstall when VMware Tools installed via RPMs
open_vm_tools_uninstall_vt_rpms_pkgs__default:
  - vmware-tools-esx
  - vmware-tools-esx-nox
  - vmware-tools-esx-kmods

# Final list of packages to uninstall when VMware Tools installed via RPMs
open_vm_tools_uninstall_vt_rpms_pkgs: "{{
    open_vm_tools_uninstall_vt_rpms_pkgs__default +
    open_vm_tools_uninstall_vt_rpms_pkgs__custom }}"

# Path to the installer when VMware Tools installed manually
open_vm_tools_uninstall_vt_manual_installer: /etc/vmware-tools/installer.sh

# Open VM Tools package (you can specify exact version here)
open_vm_tools_pkg: open-vm-tools

# Whether to install the VMware deployPkg Tools plug-in
open_vm_tools_plugin_deploypkg_install: no

# URL for the YUM repo of the VMware deployPkg Tools plug-in
# (RHEL7 package works also on RHEL6, x86_64 only supported)
open_vm_tools_plugin_deploypkg_yumrepo_url: http://packages.vmware.com/packages/rhel7/x86_64/

# Allow to overwrite the YUM repo parameters
open_vm_tools_plugin_deploypkg_yumrepo_params: {}

# URL of the GPG key for the RPM packages from the YUM repo
open_vm_tools_plugin_deploypkg_gpgkey_url: http://packages.vmware.com/tools/keys/VMWARE-PACKAGING-GPG-RSA-KEY.pub

# Packege containing the VMware deployPkg Tools plug-in
# (you can specify exact version here)
open_vm_tools_plugin_deploypkg_pkg: open-vm-tools-deploypkg
```


License
-------

MIT


Author
------

Jiri Tyr
