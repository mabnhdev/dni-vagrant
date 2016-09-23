# dni-vagrant

Use the vagrant file to create a vagrant image based on Ubuntu-Core (Xenial).

* DNI development
  * /home/vagrant/DNI/
    * dni-snappy
      * Repository for building custom Ubuntu-Core ONIE NOS Installer for DNI switches.
    * xpliant-driver-snappy
      * Repository for building Cavium/Xpliant xp80 driver using snapcraft.
    * Vagrant setup has pre-configured the repositories for target DNI L9032NXB.

* Building a custom Ubuntu-Core ONIE NOS Installer for DNI L9032NXB.
  * cd /home/vagrant/DNI/dni-snappy
  * snapcraft login
    * enter your Ubuntu One credentials 
  * snapcraft clean && snapcraft
  * When you are prompted to build the driver...
  * Open a second ssh session to the vagrant image.
  * cd /home/vagrant/DNI/xpliant-driver-snappy
  * snapcraft clean && snapcraft
  * exit
  * In original ssh session...
  * Hit any key to continue.
  * When snapcraft completes, you have a custom kernel snap that includes the xp80 driver.
  * sudo tools/make_onie_installer deltanetworks-l9032nxb-kernel_4.4.16-ops-1_amd64.snap
  * When this completes, you'll have an ONIE NOS Installer - snappy-onie-installer-x86_64-deltanetworks-l9032nxb.bin

* See ONIE website for directions on how to install an ONIE NOS.

* Simplest manual way to install...
  * Copy your ONIE NOS installer file to a tftp server reachable from the target.
  * Reboot the target switch.
  * Select 'onie' from the boot menu.
  * Select 'ONIE:Rescue' from the ONIE menu.
  * Hit ENTER to activate the console.
  * onie-nos-install tftp://<tftp address>/snappy-onie-installer-x86_64-deltanetworks-l9032nxb.bin

* Known Issues
  * The base vagrant image 'boxcutter/ubuntu1604' has not been built correctly to support private or public networks.  Only the default is available.
