configure_and_start_teleport
=========

Configure and start a teleport server or node

Requirements
------------

None.

Role Variables
--------------

Default variables used **by the role**:
- `systemd_unit_name`: name of the systemd service, defaults to `teleport.service`
- `start_the_service`: whether the role should start the service (default: true)
- `enable_the_service`: whether the role should enable the service (default:true)

Variables used to configure teleport on **both servers and nodes**:
- `teleport_data_directory`: `data_dir` setting of teleport, defaults to `/var/lib/teleport`
- `log_output`: log output, defaults to `stderr`
- `log_severity`: log severity, default `INFO`
- `log_format_output`: log output format, defaults to `text`
- `enable_ssh_service`: Boolean to enable the `ssh_service`
- `labels`: dictionary (key-value pairs) containing labels and their values
- `command`: list of dictionaries (key-value pairs), where each contains:
  - `name`: name of the command
  - `command`: actual command
  - `period`: interval like `1m` or `30s`
- `enable_app_service`: Boolean to enable the `app_service`

Variables used to configure teleport on **servers**:
- `cluster_name`: name of the new teleport cluster
- `tls_key_file`: path to the TLS key file, defaults to `/etc/pki/tls/private/teleport-server.key`
- `tls_cert_file`: path to the TLS certificate file, defaults to `/etc/pki/tls/private/teleport-server.crt`
- `enable_auth_service`: Boolean to enable the `auth_service`
- `teleport_auth_listen_address`: address to listen to, default to `0.0.0.0:3025`
- `auth_service_authentication`: set this if you want to change authentication related settings. This list will be looped-over and included in the `authentication` section (see example playbook below)
- `auth_service_tokens`: list of tokens that you want to define
- `proxy_listener_mode`: defaults to multiplex
- `teleport_proxy_listen_address`: address to listen on, defaults to `0.0.0.0:443`
- `teleport_public_address`: public IP address, defaults to using the default IPv4 address that Ansible found for the machine (`ansible_default_ipv4.address` or `ansible_all_ipv4_addresses[0]`)
- `enable_proxy_service`: Boolean to enable the `proxy_service`
- `proxy_acme`: ACME settings, defaults to `{}` (do not use ACME)

Variables used to configure teleport on **nodes**:
- `auth_token`: token used to join the cluster
- `auth_servers`: list of auth servers, either `IP:Port` or `FQDN:Port`

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
        - { role: 'johanneskastl.configure_and_start_teleport' }

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
