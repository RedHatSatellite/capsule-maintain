# capsule-maintain
Install/upgrade a Satellite6 Capsule server using ansible playbooks.

## Getting Started

#### What you need: ####
- Satellite 6.2/6.3 server. The Satellite server will be used as the Ansible control node.
- Target server(s) for Capsule installation/upgrade.
- Password-less ssh from Satellite to all required capsules.
- You can run install/upgrade on one or more capsule servers at one time.
- Make sure that the required firewall ports are opened in your Capsule and Satellite servers.
- Activation Key / Content view with the following repos: rhel-7-server-rpms, rhel-server-rhscl-7-rpms, rhel-7-server-satellite-capsule-<capsule_version>-rpms, rhel-7-server-satellite-tools-<capsule_version>-rpms where capsule_version is 6.2 or 6.3.


#### Supported Scenaios: ####
- Capsule 6.2/6.3 installation.
- Capsule 6.2 to 6.3 upgrade.
- Capsule z-stream upgrade

#### Setup ####
On the Satellite server:

1. Install `ansible` package.  Ansible should be installed from Satellite maintenance channel.
   ```console
     # subscription-manager repos --enable rhel-7-server-satellite-maintenance-6-rpms
     # yum install -y ansible
   ```

2. git clone this project.
  ```console
    # git clone https://github.com/sthirugn/capsule-install.git
    # cd capsule-install
  ```

3. Copy the vars configuration file.
  ```console
    # cp vars.sample.yml vars.yml
  ```

4. In `vars.yml` file, update the following parameters:
   - `capsule_version` - Version of the capsule (`6.2` or `6.3`)to be installed.
   - `satellite_org_label` - (applicable to install only) Label of the Satellite Organization to which the capsule needs to be registered.
   - `satellite_activation_key` - (applicable to install only) Activation key of the Satellite Organization to which the capsule needs to be registered.

5. Update `inventory` file with the capsule(s) hostname(s).

6. Use the Capsule install or upgrade playbook:
  * Capsule Install:
    ```console
      ansible-playbook capsule-install-playbook.yml
    ```
  * Capsule Upgrade (y-stream):
    ```console
      ansible-playbook capsule-upgrade-playbook.yml
    ```
  * Capsule Upgrade (z-stream):
    ```console
      ansible-playbook capsule-zupgrade-playbook.yml
    ```
