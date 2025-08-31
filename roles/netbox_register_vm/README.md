# netbox_register_vm

This role registers or unregisters a virtual machine in NetBox, optionally handling IPAM assignment for the primary interface.

## Requirements

requires collection:

- `netbox.netbox`

## Role Variables

### `netbox_register_vm` Role Variables

The `netbox_register_vm` role automates the process of registering or unregistering a virtual machine in NetBox. The following variables can be used to configure its behavior.

---

#### General Options

These are the primary variables for the role.

| Parameter               | Type   | Required | Default   | Description                                                                                     |
| ----------------------- | ------ | -------- | --------- | ----------------------------------------------------------------------------------------------- |
| **`state`**             | `str`  | no       | `present` | Determines whether to register or unregister the VM. Options are `present` or `absent`.         |
| **`assign_primary_ip`** | `bool` | no       | `true`    | Set to `false` to skip IP address request and assignment.                                       |
| **`netbox_url`**        | `str`  | yes      |           | The URL of the NetBox instance.                                                                 |
| **`netbox_token`**      | `str`  | yes      |           | The API token for authenticating with NetBox. This is a sensitive value and will not be logged. |

---

#### `vm` (Virtual Machine Details)

This is a **`required`** dictionary containing all details about the virtual machine.

| Parameter            | Type   | Required | Default                    | Description                                     |
| -------------------- | ------ | -------- | -------------------------- | ----------------------------------------------- |
| **`name`**           | `str`  | yes      |                            | The name of the virtual machine.                |
| **`cluster`**        | `str`  | yes      |                            | The name of the NetBox cluster.                 |
| **`tenant`**         | `str`  | yes      |                            | The name of the NetBox tenant.                  |
| **`site`**           | `str`  | yes      |                            | The NetBox site for the VM.                     |
| **`vcpus`**          | `int`  | no       | `2`                        | The number of virtual CPUs.                     |
| **`memory`**         | `int`  | no       | `4096`                     | The amount of memory in MB.                     |
| **`disk`**           | `int`  | no       | `50`                       | The disk size in GB.                            |
| **`interface_name`** | `str`  | no       | `eth0`                     | Name for the primary network interface.         |
| **`interface_mac`**  | `str`  | no       |                            | Optional MAC address for the primary interface. |
| **`tags`**           | `list` | no       | `['ansible', 'automated']` | A list of tags to apply to the VM in NetBox.    |

---

#### `ipam` (IPAM Details)

This is a dictionary for IPAM details. It is **`required`** only if `assign_primary_ip` is set to `true`.

| Parameter        | Type  | Required | Default | Description                                                       |
| ---------------- | ----- | -------- | ------- | ----------------------------------------------------------------- |
| **`prefix`**     | `str` | yes      |         | The CIDR prefix to request an IP from (e.g., `'192.168.1.0/24'`). |
| **`dns_domain`** | `str` | yes      |         | The domain to append to the hostname for the DNS record.          |

## Dependencies

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: "Register a new web server in NetBox"
  hosts: localhost
  gather_facts: false

  tasks:
    - name: register vm with role
      include_role:
        name: lanefu.armlab.netbox_register_vm
      vars:
        netbox_url: https://netbox.example.com
        netbox_token: "MYTOKEN"
        state: "present"
        vm:
          name: "test-netbox-role-01"
          cluster: "my_cluster"
          tenant: "My Tenant"
          interface_name: "eth0"
          vcpus: 6
          memory: 8192
          disk: 200
          site: "mysite"
        ipam:
          prefix: "10.254.0.0/24"
          dns_domain: "testsubdomain.example.com"
```

```yaml
- name: "Register a new web server in NetBox"
  hosts: localhost
  gather_facts: false

  tasks:
    - name: register vm with role
      include_role:
        name: lanefu.armlab.netbox_register_vm
      vars:
        netbox_url: https://netbox.example.com
        netbox_token: "MYTOKEN"
        state: "absent"
        vm:
          name: "test-netbox-role-01"
          cluster: "my_cluster"
          tenant: "My Tenant"
```

## License

TBD

## Author Information

@lanefu
