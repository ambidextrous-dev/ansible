# Sonarqube_Upgrade

An Ansible role which can upgrade on-premises Sonarqube installations on Linux boxes

## Role Variables
--------------

[vars/main.yml](vars/main.yml)

| Variable                | Required | Default             | Comments                            |
| ----------------------- | -------- | ------------------- | ----------------------------------  |
| `sonar_target_version`  | Yes      | `9.8.0.63668`       | Target Sonarqube version            |
| `sonar_db_host `        | Yes      | `dbserverhost`      | Sonarqube Database Host             |
| `sonar_db_name`         | Yes      | `dbname`            | Sonarqube Database Name             |
| `sonar_db_port `        | Yes      | `5432`              | Sonarqube Database Port             |
| `sonar_db_user`         | Yes      | `dbusername`        | Sonarqube Database User             |
| `sonar_db_password`     | Yes      | `dbpassword`        | Sonarqube Database Password         |

## Dependencies
------------

None

## Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: sonarqube_upgrade
      kompose_version: 1.0.0
```

# Usage:
-----------------
Run the ansible-playbook command to run the ansible role:

``` 
ansible-playbook -v -i  "inventories/dev/hosts" site.yml -u username
```

# Notes: 
---------------
* Somtimes sonarqube does not allows us to upgrade directly from an old version to the latest version. In that case, you may have to run this ansible role two times, once for a middle version and then for the latest version
* After upgrade, if the database schema needs to be updated, you may have to go to http://yourSonarQubeServerURL/setup URL and follow setup instructions to manually upgrade database
* Before running this role, it is highly recommended to take a backup of the database
* Commands to encrypt/decrypt the sensitive files (prompt will ask for vault password):
  ```
     ansible-vault encrypt roles/sonarqube_upgrade/vars/main.yml
     ansible-vault decrypt roles/sonarqube_upgrade/vars/main.yml
  ```

Note: Detailed documentation about this role and how to run this can be found here  - https://medium.com/@sushil.dev/automated-sonarqube-upgrades-with-ansible-8ee3a21f7c11