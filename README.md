<!-- DOCSIBLE START -->
# Ansible Role: role_tomcat


role_tomcat to configure Tomcat settings


## Table of Contents

- [Requirements](#requirements)
- [Dependencies](#dependencies)
- [Role Variables](#role-variables)
- [Task Overview](#task-overview)
- [Example Playbook](#example-playbook)
- [Documentation Maintenance](#documentation-maintenance)
- [License](#license)
- [Author Information](#author-information)

## Requirements



- Ansible >= 2.9


- Supported platforms:
  - Ubuntu (noble)
  - AlmaLinux (8)



## Dependencies


This role requires the following roles and collections:




  
    
  

  
    
  

  
    
  

  
    
  

  
    
  



**Roles:**

- [role_base](https://github.com/ginanck/role_base.git) (version: master)

- [role_java](https://github.com/ginanck/role_java.git) (version: master)




**Collections:**

- `community.docker` (>= 4.8.1)

- `community.general` (>= 6.6.1)

- `ansible.posix` (>= 1.5.4)



To install all dependencies:
```bash
ansible-galaxy install -r meta/install_requirements.yml
```


## Role Variables

**These are static variables with lower priority**



#### File: defaults/main.yml

| Var | Type | Value |
|-----|------|-------|
| [tomcat_catalina_additional_opts](defaults/main.yml#L45) | list |  |
| [tomcat_catalina_opts](defaults/main.yml#L39) | list |  |
| [tomcat_catalina_opts.0](defaults/main.yml#L40) | str | `-Xms512M` |
| [tomcat_catalina_opts.1](defaults/main.yml#L41) | str | `-Xmx1024M` |
| [tomcat_catalina_opts.2](defaults/main.yml#L42) | str | `-server` |
| [tomcat_catalina_opts.3](defaults/main.yml#L43) | str | `-XX:+UseParallelGC` |
| [tomcat_download_archive_url](defaults/main.yml#L24) | str | `https://archive.apache.org/dist/tomcat/tomcat-{{ tomcat_major_version }}/v{{ tomcat_version }}/bin/apache-tomcat-{{ tomcat_version }}.tar.gz` |
| [tomcat_download_current_url](defaults/main.yml#L23) | str | `https://dlcdn.apache.org/tomcat/tomcat-{{ tomcat_major_version }}/v{{ tomcat_version }}/bin/apache-tomcat-{{ tomcat_version }}.tar.gz` |
| [tomcat_environment_variables](defaults/main.yml#L16) | list |  |
| [tomcat_group](defaults/main.yml#L5) | str | `tomcat` |
| [tomcat_home_link_dir](defaults/main.yml#L6) | str | `/opt/tomcat` |
| [tomcat_java_additional_opts](defaults/main.yml#L30) | list |  |
| [tomcat_java_opts](defaults/main.yml#L26) | list |  |
| [tomcat_java_opts.0](defaults/main.yml#L27) | str | `-Xms512m` |
| [tomcat_java_opts.1](defaults/main.yml#L28) | str | `-Xmx512m` |
| [tomcat_log_dir](defaults/main.yml#L13) | str | `/var/log/tomcat` |
| [tomcat_log_link_path](defaults/main.yml#L14) | str | `{{ tomcat_versioned_dir }}/logs` |
| [tomcat_major_version](defaults/main.yml#L21) | str | `{{ tomcat_version.split('.')[0] }}` |
| [tomcat_roles](defaults/main.yml#L62) | list |  |
| [tomcat_roles.0](defaults/main.yml#L63) | str | `admin-gui` |
| [tomcat_roles.1](defaults/main.yml#L64) | str | `manager-gui` |
| [tomcat_roles.2](defaults/main.yml#L65) | str | `manager-script` |
| [tomcat_roles.3](defaults/main.yml#L66) | str | `manager-jmx` |
| [tomcat_roles.4](defaults/main.yml#L67) | str | `manager-status` |
| [tomcat_root_link_path](defaults/main.yml#L11) | str | `{{ tomcat_versioned_dir }}/webapps/ROOT.war` |
| [tomcat_root_path](defaults/main.yml#L10) | str | `{{ tomcat_versioned_dir }}/webapps/ROOT` |
| [tomcat_user](defaults/main.yml#L4) | str | `tomcat` |
| [tomcat_users](defaults/main.yml#L69) | list |  |
| [tomcat_users.0](defaults/main.yml#L70) | dict |  |
| [tomcat_users.0.password](defaults/main.yml#L71) | str | `secure_pass` |
| [tomcat_users.0.roles](defaults/main.yml#L72) | list |  |
| [tomcat_users.0.roles.0](defaults/main.yml#L73) | str | `admin-gui` |
| [tomcat_users.0.roles.1](defaults/main.yml#L74) | str | `manager-gui` |
| [tomcat_users.0.username](defaults/main.yml#L70) | str | `admin` |
| [tomcat_users.1](defaults/main.yml#L75) | dict |  |
| [tomcat_users.1.password](defaults/main.yml#L76) | str | `deploy_password` |
| [tomcat_users.1.roles](defaults/main.yml#L77) | list |  |
| [tomcat_users.1.roles.0](defaults/main.yml#L77) | str | `manager-script` |
| [tomcat_users.1.username](defaults/main.yml#L75) | str | `deployer` |
| [tomcat_users.2](defaults/main.yml#L78) | dict |  |
| [tomcat_users.2.password](defaults/main.yml#L79) | str | `monitor_pass` |
| [tomcat_users.2.roles](defaults/main.yml#L80) | list |  |
| [tomcat_users.2.roles.0](defaults/main.yml#L80) | str | `manager-status` |
| [tomcat_users.2.username](defaults/main.yml#L78) | str | `monitor` |
| [tomcat_version](defaults/main.yml#L20) | str | `9.0.105` |
| [tomcat_versioned_dir](defaults/main.yml#L7) | str | `/opt/tomcat-{{ tomcat_version }}` |
| [tomcat_webapp_manager_remote_access](defaults/main.yml#L82) | bool | `True` |
| [tomcat_webapp_manager_remote_access_ip_whitelist](defaults/main.yml#L83) | list |  |
| [tomcat_webapp_manager_remote_access_ip_whitelist.0](defaults/main.yml#L83) | str | `10\.50\.\d+\.\d+` |
| [tomcat_webapp_path](defaults/main.yml#L9) | str | `/opt/webapp.war` |




## Task Overview


This role performs the following tasks:


### File: `tasks/main.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Create tomcat group](tasks/main.yml#L) | ansible.builtin.group | No | N/A |
| [Create tomcat user](tasks/main.yml#L) | ansible.builtin.user | No | N/A |
| [Check current download URL status](tasks/main.yml#L) | ansible.builtin.uri | No | N/A |
| [Check archive download URL status](tasks/main.yml#L) | ansible.builtin.uri | Yes | N/A |
| [Set download url and availability facts](tasks/main.yml#L) | ansible.builtin.set_fact | No | N/A |
| [Check If Expected Tomcat Version Is Already Installed](tasks/main.yml#L) | ansible.builtin.stat | No | N/A |
| [Get Installed Tomcat Version](tasks/main.yml#L) | ansible.builtin.slurp | Yes | N/A |
| [Set Installation Required Fact](tasks/main.yml#L) | ansible.builtin.set_fact | No | N/A |
| [Create Tomcat Versioned Directory](tasks/main.yml#L) | ansible.builtin.file | Yes | N/A |
| [Download And Extract Tomcat](tasks/main.yml#L) | ansible.builtin.unarchive | Yes | N/A |
| [Create version file](tasks/main.yml#L) | ansible.builtin.copy | Yes | N/A |
| [Check If Folder Exists](tasks/main.yml#L) | ansible.builtin.stat | No | N/A |
| [Create/Update Symbolic Link To Active Tomcat Version](tasks/main.yml#L) | ansible.builtin.file | Yes | N/A |
| [Get Default Java Path](tasks/main.yml#L) | ansible.builtin.stat | No | N/A |
| [Set Java Home Path](tasks/main.yml#L) | ansible.builtin.set_fact | No | N/A |
| [Create Tomcat Service File](tasks/main.yml#L) | ansible.builtin.template | No | N/A |
| [Create Setenv.sh](tasks/main.yml#L) | ansible.builtin.template | No | N/A |
| [Create Tomcat Users And Roles](tasks/main.yml#L) | ansible.builtin.template | No | N/A |
| [Configure Manager/META-INF/Context.xml](tasks/main.yml#L) | ansible.builtin.template | No | N/A |
| [Configure Host-Manager/META-INF/Context.xml](tasks/main.yml#L) | ansible.builtin.template | No | N/A |
| [Check current ROOT link status](tasks/main.yml#L) | ansible.builtin.stat | No | N/A |
| [Remove Existing ROOT.war If Present](tasks/main.yml#L) | ansible.builtin.file | Yes | N/A |
| [Create Link For Webapp To ROOT.war](tasks/main.yml#L) | ansible.builtin.file | Yes | N/A |
| [Create Tomcat Log Directory](tasks/main.yml#L) | ansible.builtin.file | No | N/A |
| [Check current log link status](tasks/main.yml#L) | ansible.builtin.stat | No | N/A |
| [Remove existing Tomcat logs directory](tasks/main.yml#L) | ansible.builtin.file | Yes | N/A |
| [Create Log Dir Symbolic Link](tasks/main.yml#L) | ansible.builtin.file | Yes | N/A |
| [Start Tomcat Service](tasks/main.yml#L) | ansible.builtin.systemd_service | No | N/A |






## Example Playbook

```yaml
---
- hosts: all
  become: yes
  roles:
    - role: role_tomcat

      vars:
        tomcat_user: tomcat
        tomcat_group: tomcat
        tomcat_home_link_dir: /opt/tomcat

```

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
