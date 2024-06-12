## Configuration setup:

### Set static network details:
1. `sudo nmtui`
   - set network connections
   - set hostname

### Set timezone and verify time is being syncd from NTP:
1. `sudo timedatectl set-timezone CST6CDT` #Set timezone
2. `sudo timedatectl status` and `sudo chronyc sources` #Test time sync

### Create folder structure for containers/VMs:
1. `mkdir /home/duckman/containers /home/duckman/vms`
2. `mkdir /home/duckman/containers/pihole /home/duckman/containers/unifi`

### Update server and install baseline software:
1. `sudo dnf update -y`
2. `curl -LO https://github.com/docker/compose/releases/download/v2.27.0/docker-compose-linux-x86_64`
3. `chmod +x docker-compose-linux-x86_64`
4. `sudo mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose`
5. `sudo dnf -y install dnf-automatic podman podman-docker virt-v2v dnf-plugins-core cockpit cockpit-system cockpit-podman cockpit-machines cockpit-storaged`
6. `sudo systemctl enable --now cockpit.socket`
7. `sudo ln -s /usr/libexec/docker/cli-plugins/docker-compose /usr/local/bin/docker-compose`

### Remove DHCPv6:
1. `sudo firewall-cmd --remove-service=dhcpv6-client --permanent`
2. `sudo firewall-cmd --reload`

### Configure automatic updates:
1. Update `sudo vi /etc/dnf/automatic.conf`
2. Change the upgrade type from `upgrade_type = default` to security patches only with `upgrade_type = security`
3. `sudo systemctl enable dnf-automatic-install.timer`

### Setup Podman:
1. `sudo systemctl enable --now podman.socket`
2. `systemctl --user enable --now podman.socket`
3. We also need to define and export the DOCKER_HOST environment variable. The traditional way to do this is by adding the line below to ~/.bash_profile or ~/.profile, depending on the shell we are using:
- 'export DOCKER_HOST=unix:///run/user/1000/docker.sock'
4. 'source ~/.bash_profile'
