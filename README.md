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



### File: `defaults/main.yml`

| Variable | Default Value | Description |
|----------|---------------|-------------|
| `tomcat_user` | `tomcat` | None |
| `tomcat_group` | `tomcat` | None |
| `tomcat_home_link_dir` | `/opt/tomcat` | None |
| `tomcat_versioned_dir` | `/opt/tomcat-{{ tomcat_version }}` | None |
| `tomcat_webapp_path` | `/opt/webapp.war` | None |
| `tomcat_root_path` | `{{ tomcat_versioned_dir }}/webapps/ROOT` | None |
| `tomcat_root_link_path` | `{{ tomcat_versioned_dir }}/webapps/ROOT.war` | None |
| `tomcat_log_dir` | `/var/log/tomcat` | None |
| `tomcat_log_link_path` | `{{ tomcat_versioned_dir }}/logs` | None |
| `tomcat_environment_variables` | `[]` | None |
| `tomcat_version` | `9.0.105` | None |
| `tomcat_major_version` | `{{ tomcat_version.split('.')[0] }}` | None |
| `tomcat_download_current_url` | `https://dlcdn.apache.org/tomcat/tomcat-{{ tomcat_major_version }}/v{{ tomcat_version }}/bin/apache-tomcat-{{ tomcat_version }}.tar.gz` | None |
| `tomcat_download_archive_url` | `https://archive.apache.org/dist/tomcat/tomcat-{{ tomcat_major_version }}/v{{ tomcat_version }}/bin/apache-tomcat-{{ tomcat_version }}.tar.gz` | None |
| `tomcat_java_opts` | `[]` | None |
| `tomcat_java_opts.0` | `-Xms512m` | None |
| `tomcat_java_opts.1` | `-Xmx512m` | None |
| `tomcat_java_additional_opts` | `[]` | None |
| `tomcat_catalina_opts` | `[]` | None |
| `tomcat_catalina_opts.0` | `-Xms512M` | None |
| `tomcat_catalina_opts.1` | `-Xmx1024M` | None |
| `tomcat_catalina_opts.2` | `-server` | None |
| `tomcat_catalina_opts.3` | `-XX:+UseParallelGC` | None |
| `tomcat_catalina_additional_opts` | `[]` | None |
| `tomcat_roles` | `[]` | None |
| `tomcat_roles.0` | `admin-gui` | None |
| `tomcat_roles.1` | `manager-gui` | None |
| `tomcat_roles.2` | `manager-script` | None |
| `tomcat_roles.3` | `manager-jmx` | None |
| `tomcat_roles.4` | `manager-status` | None |
| `tomcat_users` | `[]` | None |
| `tomcat_users.0` | `{}` | None |
| `tomcat_users.0.username` | `admin` | None |
| `tomcat_users.0.password` | `secure_pass` | None |
| `tomcat_users.0.roles` | `[]` | None |
| `tomcat_users.0.roles.0` | `admin-gui` | None |
| `tomcat_users.0.roles.1` | `manager-gui` | None |
| `tomcat_users.1` | `{}` | None |
| `tomcat_users.1.username` | `deployer` | None |
| `tomcat_users.1.password` | `deploy_password` | None |
| `tomcat_users.1.roles` | `[]` | None |
| `tomcat_users.1.roles.0` | `manager-script` | None |
| `tomcat_users.2` | `{}` | None |
| `tomcat_users.2.username` | `monitor` | None |
| `tomcat_users.2.password` | `monitor_pass` | None |
| `tomcat_users.2.roles` | `[]` | None |
| `tomcat_users.2.roles.0` | `manager-status` | None |
| `tomcat_webapp_manager_remote_access` | `True` | None |
| `tomcat_webapp_manager_remote_access_ip_whitelist` | `[]` | None |
| `tomcat_webapp_manager_remote_access_ip_whitelist.0` | `10\.50\.\d+\.\d+` | None |




## Task Overview


This role performs the following tasks:


### `main.yml`


- **Create tomcat group**
- **Create tomcat user**
- **Check current download URL status**
- **Check archive download URL status**
- **Set download url and availability facts**
- **Check If Expected Tomcat Version Is Already Installed**
- **Get Installed Tomcat Version**
- **Set Installation Required Fact**
- **Create Tomcat Versioned Directory**
- **Download And Extract Tomcat**
- **Create version file**
- **Check If Folder Exists**
- **Create/Update Symbolic Link To Active Tomcat Version**
- **Get Default Java Path**
- **Set Java Home Path**
- **Create Tomcat Service File**
- **Create Setenv.sh**
- **Create Tomcat Users And Roles**
- **Configure Manager/META-INF/Context.xml**
- **Configure Host-Manager/META-INF/Context.xml**
- **Check current ROOT link status**
- **Remove Existing ROOT.war If Present**
- **Create Link For Webapp To ROOT.war**
- **Create Tomcat Log Directory**
- **Check current log link status**
- **Remove existing Tomcat logs directory**
- **Create Log Dir Symbolic Link**
- **Start Tomcat Service**




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

## Documentation Maintenance

### Updating Dependencies

1. **Update** `meta/main.yml`:
   ```yaml
   documented_requirements:
     - src: https://github.com/user/role.git
       version: master
     - name: collection.name
       version: 1.0.0
   ```

2. **Sync** `meta/install_requirements.yml` with the same requirements

3. **Regenerate** documentation:
   ```bash
   pre-commit run --all-files
   ```

### Template Updates

- Edit `.docsible_template.md` for structure changes
- Test with: `docsible --role . --md-template .docsible_template.md -nob -com -tl`
- Commit both template and generated README.md

### Quick Checklist

When updating dependencies:
- [ ] Add to `meta/main.yml` → `documented_requirements`
- [ ] Add to `meta/install_requirements.yml`
- [ ] Run `pre-commit run --all-files`
- [ ] Verify generated README.md
- [ ] Commit all changes

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
