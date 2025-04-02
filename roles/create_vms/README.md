# create_vms

Provisions libvirt network, storage pools and the KVM Nodes.

## Multiple Network Support

This role now supports creating and attaching multiple networks to VMs. The default network behavior is preserved for backward compatibility.

### Configuration Variables

- `create_vms_additional_networks`: A list of additional networks to create and attach to VMs. Each network should have:
  - `name`: Network name
  - `mode`: Network mode ('bridge' or 'nat')
  - `bridge_name`: Bridge device name for bridge mode or bridge name for NAT mode
  - `cidr`: CIDR for NAT mode networks

### Example

```yaml
# Define additional networks
create_vms_additional_networks:
  - name: "storage-net"
    mode: "nat" 
    bridge_name: "storage-bridge"
    cidr: "192.168.123.0/24"
  - name: "management-net"
    mode: "bridge"
    bridge_name: "management-bridge"
```

With this configuration, all VMs will be attached to both the default network and the additional networks specified.