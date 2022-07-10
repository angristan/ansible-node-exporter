# Ansible role for Node exporter

This role will setup [Node exporter](https://github.com/prometheus/node_exporter) on any Linux machine using systemd.

## Role Variables

- `node_exporter_version`: the version of Node exporter that will be installed.

The role will download the Node exporter release on the deployer and upload the binary to the target host.

If the `/usr/local/bin/node_exporter` binary already exists, the role will skip the install steps. You can force them (to update, for instance), by setting `node_exporter_force_install` to true.

- `node_exporter_system_group`: the name of the group that will run Node exporter.(`node-exporter`)
- `node_exporter_system_user`: the name of the user that will run Node exporter. Default to `node_exporter_system_group`.
- `node_exporter_web_listen_address`: the address Node exporter will listen on. (`0.0.0.0:9100`)

Node exporter comes with a default set of enabled and disabled collectors.

You can enable more collectors with `node_exporter_enabled_collectors`.

The default is:

```yaml
node_exporter_enabled_collectors:
  - systemd
  - ntp
  - filesystem:
      ignored-mount-points: "^/(sys|proc|dev)($|/)"
      ignored-fs-types: "^(sys|proc|auto)fs$"
```

To disable collectors, use `node_exporter_enabled_collectors`. It's empty by default.

## Example playbook

```yaml
---
- hosts: myhost
  roles: node-exporter
```

## License

MIT. See LICENSE for more details.

## Credit

This role is largely inspired by [cloudalchemy/ansible-node-exporter](https://github.com/cloudalchemy/ansible-node-exporter).

## Author Information

See my other Ansible roles at [angristan/ansible-roles](https://github.com/angristan/ansible-roles).
