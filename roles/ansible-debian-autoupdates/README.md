Role Name
=========

An Ansible role to install/configure unattended-upgrades for Debian based systems.

Requirements
------------

None

Role Variables
--------------

````
---
# defaults file for ansible-debian-autoupdates
debian_autoupdates_auto_reboot: false  #Automatically reboot *WITHOUT CONFIRMATION* if the file /var/run/reboot-required is found after the upgrade
debian_autoupdates_auto_reboot_time: 'now'  #If automatic reboot is enabled and needed, reboot at the specific time instead of immediately Default: "now"...ex. 02:00
debian_autoupdates_autofix_interrupted: true  #Defines if on a unclean dpkg exit unattended-upgrades will automatically run dpkg --force-confold --configure -a (Default: true)
debian_autoupdates_bandwidth_limit: '70'  #Use apt bandwidth limit feature, this example limits the download speed to 70kb/sec
debian_autoupdates_blacklist:  #Define packages to blacklist from upgrading
  - 'vim'
  - 'libc6'
  - 'libc6-dev'
  - 'libc6-i686'
debian_autoupdates_debian_allowed_origins:  #Defines Automatically upgrade packages from these (origin:archive) pairs (Debian)
  - 'Security'
debian_autoupdates_email_address: 'root'  #Defines email address to receive reports
debian_autoupdates_email_on_error_only: false  #Defines if emails should only be sent on errors
debian_autoupdates_installonshutdown: false  #Install all unattended-upgrades when the machine is shuting down instead of doing it in the background while the machine is running
debian_autoupdates_minimalsteps: false  #Split the upgrade into the smallest possible chunks so that they can be interrupted with SIGUSR1
debian_autoupdates_packages:
  - 'apt-listchanges'
  - 'unattended-upgrades'
debian_autoupdates_remove_unused_dependencies: false  #Do automatic removal of new unused dependencies after the upgrade (equivalent to apt-get autoremove)
debian_autoupdates_schedule:  #Define update schedules
  apt_get_autoclean: 21  #Do "apt-get autoclean" every n-days (0=disable)
  apt_get_unattended_upgrade: 1  #Run the "unattended-upgrade" security upgrade script every n-days (0=disabled)
  apt_get_update: 1  #Do "apt-get update" automatically every n-days (0=disable)
  apt_get_upgrade_dl_only: 1  #Do "apt-get upgrade --download-only" every n-days (0=disable)
debian_autoupdates_ubuntu_allowed_origins:  #Defines Automatically upgrade packages from these (origin:archive) pairs (Ubuntu)
#  - 'backports'
#  - 'proposed'
  - 'security'
#  - 'updates'
enable_debian_autoupdates: true  #Defines if updates should be enabled
enable_debian_autoupdates_bandwidth_limit: false  #Defines if bandwidth limits for updates should be enforced...based on debian_autoupdates_bandwidth_limit
enable_debian_autoupdates_blacklist: false  #Defines if packages defined in debian_autoupdates_blacklist should be enabled
enable_debian_autoupdates_email: false  #Defines if emails should be sent to email address configured in debian_autoupdates_email_address
````
Dependencies
------------

None

Example Playbook
----------------

````
- hosts: all
  become: true
  vars:
  roles:
    - role: ansible-debian-autoupdates
  tasks:
````

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
