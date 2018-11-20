Role Name
=========

Replacement of OpenShift FluentD/Logging stack with JournalD and rsyslog in order to centralize logs from multiple clusters into an external logging solution like LogInsight

Requirements
------------

* Change Docker Logging Driver from --log-driver=json to --log-driver=journald
* Add the External Endpoint variable to your openshift inventory file
```
ext_logging_endpoint: <EXTERNAL-LOG-ENDPOINT>
```
* Adjust journald variables to your liking. These variables are also part of your openshift inventory
```
journald_vars_to_replace:
- { var: Storage, val: persistent }
- { var: Compress, val: yes }
- { var: SyncIntervalSec, val: 1s }
- { var: RateLimitInterval, val: 0 }
- { var: RateLimitBurst, val: 0 }
- { var: SystemMaxUse, val: 8G }
- { var: SystemMaxFileSize, val: 500M }
- { var: SystemKeepFree, val: 5G }
- { var: MaxRetentionSec, val: 1month }
- { var: MaxFileSec, val: 1day }
- { var: ForwardToSyslog, val: no }
- { var: ForwardToWall, val: no }
```

Role Variables
--------------

Dependencies
------------

Copy roles/journald-rsyslog-logging to your roles path

Example Playbook
----------------

```
- hosts: nodes
  roles:
    - journald-rsyslog-logging
```
or 
copy `deploy-journald-rsyslog-logging.yml` to your Ansible host and run it
```
ansible-playbook -i inventory deploy-journald-rsyslog-logging.yml
```

License
-------

GPLv3

Author Information
------------------

Freddy Montero
