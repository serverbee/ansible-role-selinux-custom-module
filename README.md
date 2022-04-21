## SELinux custom module role

This role installs custom [SELinux](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/selinux_users_and_administrators_guide/index) modules and set SELinux to Enforcing mode.

#### Variables

##### General

* `selinux_config_dir`: [default: `/etc/selinux`]: Directory where will be store all SELinux module files from this role

##### SELinux custom modules settings

* `selinux_custom_modules`: [default: `{}`]: SELinux modules declarations
* `selinux_custom_modules.key`: [required]: The identifier of the module (e.g. `first-custom-module:`)
* `selinux_custom_modules.key.value`: [required]: Declarate the source code of custom SELinux modules

## Dependencies

None

#### Example

```yaml
---
- host: localhost
  roles:
    - serverbee.selinux_custom_module
  vars:
    selinux_custom_modules:
      first-custom-module: |
        module first-custom-module 1.0;
        require {
                type myapp_t;
                type myapp_port_t;
                class tcp_socket name_bind;
        }
        allow myapp_t myapp_port_t:tcp_socket name_bind;
```

#### License

GPLv3 license

#### Author Information

Bohdan Saienko
