# Installation of basic Consul cluster

- This consul repository create a set of 3 master nodes in HA with a full set of check as memory, cpu load, etc.

### How to use:

- ansible-playbook playbook.yml --skip-tags "reset_connection" -i /MyInventory/ -vvv
- /!\ --skip-tags "new_installation" give us the opportunity to install a new cluster or if it skipped to update the actual one.

### Master Config

- bootstrap 3 master in HA
- The key string to join the consul cluster is registred into the "encryption_key" if you get one.

- Value of  master config file:

| varbiables names | Default Value | Usage |
|-----|:-----|---|
| bootstrap_expect | 3 | How many master are needed for the bootstrap |
| client_addr | 0.0.0.0 | client address |
| datacenter | Your_Company_Name | Name of your "Datacenter" (cluster or location name into Consul to filter where each node is) |
| data_dir | /etc/consul.d/ | Path where you put your configs files |
| CONSUL_DOMAIN  | YOUR_CONSUL_DOMAIN | domain to resolve |
| enable_script_checks | true | enable consul for all our scritps checks on master AND slave |
| dns_config - enable_truncate | true | in case of more than 3 records: indicating to clients that they should re-query using TCP to get the full set of records |
| dns_config - only_passing | true | any nodes whose health checks are warning or critical will be excluded from DNS results |
| encrypt | myEncryptedValue | Encrypted key to join the cluster |
| leave_on_terminate | false | If the node need to be removed or not from the healthcheck if it's down |
| log_level | debug | Level of logging |
| enable_syslog | true | Enable the syslog (like journalctl -r | grep consul ) |
| rejoin_after_leave | true | If the node is off, it will retry to join the cluster
| server | true | If it's a serve or not |
| start_join | all master node IP/DNS | list fo master to join include itself |
| ui | true | define if the master will run the UI |

### Variables availbles

| varbiables names | Default Value | Usage |
|-----|:-----|---|
| consul_version_url | https://releases.hashicorp.com/consul | Hashicorp Consul base url |
| consul_version | 1.2.2 | Consul version |
| consul_path | /usr/share | where consul app is stored |
| consul_data_path | /etc/consul.d | Where we install Consul and our scripts/config |
| encryption_key | EncryptedValue | Encryption key in the config file to join the masters |
| consul_keygen | generated with the script | Used by ansible tasks when you put encryption_key to false |
