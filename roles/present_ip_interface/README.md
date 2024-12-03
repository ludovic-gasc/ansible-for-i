present_ip_interface
=========
The role is to present an IP interface and make it active. The workflow is:

1. If the internet_address does exist, make it active.
2. If the internet_address doesn't exist, create it based on the given line_description.
3. If the given line_description doesn't exist, create it
4. If the next_hop is provided, create a router based on it.

Role Variables
--------------

| Variable                                               | Type          | Required  | Default Value  | Description           |
|--------------------------------------------------------|---------------|-----------|----------------|-----------------------|
| `present_ip_interface_ip_address`      | str          | True  |     |The internet address that will be added. |
| `present_ip_interface_line_description`      | str          | False |     |The name of the line description associated with the new interface.  If the value is not provided but an IP interface need to be created, then a default line description 'DEF + Resource name of Ethernet Port', for example, DEFCMN03 is used.                      |
| `present_ip_interface_vlanid`               | str          | False |  *NONE   |The virtual LAN identifier of the associated line. |
| `present_ip_interface_netmask`           | str          | False |     |Defines the subnet mask. |
| `present_ip_interface_associated_local_interface` | str          | False |  *NONE   | Use this parameter to associate the IPv4 interface being added with an existing local IPv4 TCP/IP interface.                      |
| `present_ip_interface_type_of_service`       | str          | False | *NORMAL    |The type of service specifies how the internet hosts and routers should make trade-offs. |
| `present_ip_interface_max_transmission_unit` | str          | False | *LIND    | Specifies the maximum size (in bytes) of IP datagrams that can be transmitted through this interface. |
| `present_ip_interface_auto_start`            | str          | False | *YES    | Specifies whether the interface is automatically started. Default                     |
| `present_ip_interface_preferred_interface`   | str           | False |  *NONE   | A list of preferred IPv4 interfaces that are to be used with the IPv4 interface being added for proxy. |
| `present_ip_interface_text_description`       | str     | False   | *BLANK         | Specifies the text to briefly describe the interface. |
| `present_ip_interface_sec_to_wait`      | int          | False |  0   | The number of seconds that the module waits after executing the task before returning the information of the internet address..                      |
| `present_ip_interface_extra_params`          | str           | False | ''  |  The extra parameters that the user wants to pass into ibmi_tcp_interface module. |
| `present_ip_interface_location_code_of_ethernet_port`      | str          | False |  ''    |The location code of the ethernet port that will be used to find or create a line description. |
| `present_ip_interface_resource_name_of_ethernet_port`      | str          | False |  ''   |The resource name of the ethernet port that will be used to find or create a line description.                      |
| `present_ip_interface_mac_address_of_ethernet_port`      | str          | False |  ''   |The mac address of the ethernet port that will be used to find or create line description.                      |
| `present_ip_interface_present_ip_interface_addition_options_for_crtlineth`     | str          | False |  　''   |Addtion options for CRTLINETH. |
| `present_ip_interface_route_destination`      | str          | False  |  *DFTROUTE   |Specifies the route destination being added. |
| `present_ip_interface_next_hop`      | str          | False |     |Specifies the internet address of the next system (gateway) on the route.                          .                      |
| `present_ip_interface_addition_options_for_addtcprte`               | str          | False |  ''  |Addtion options for ADDTCPRTE. |

Example Playbooks
----------------
```
- name: To acitive an existing IP interface
  hosts: ibmi 

  roles:
    - role: present_ip_interface
      vars:
        present_ip_interface_ip_address: '10.10.10.10'
```

```
- name: To activate an IP interface, if it doesn't exist, create one interface then activate it using line description DEFCMN03. If DEFCMN03 doesn't exist, create it based on CMN03 firstly. 
  hosts: ibmi

  roles:
    - role: present_ip_interface
      vars:
        present_ip_interface_ip_address: '10.10.10.10'
        present_ip_interface_netmask: '255.255.255.0'
        present_ip_interface_resource_name_of_ethernet_port: 'CMN03'
```

```
- name: To activate an IP interface, if it doesn't exist, create one interface then activate it using line description ETHLINE1. If ETHLINE1 doesn't exist, create it based on CMN03 firstly.  
  hosts: ibmi

  roles:
    - role: present_ip_interface
      vars:
        present_ip_interface_ip_address: '10.10.10.10'
        present_ip_interface_netmask: '255.255.255.0'
        present_ip_interface_line_description: 'ETHLINE1'
        present_ip_interface_resource_name_of_ethernet_port: 'CMN03'
```

```
- name: To activate an IP interface, if it doesn't exist, create one interface then activate it using line description DEFCMN03. If DEFCMN03 doesn't exist, create it based on CMN03 firstly. Create a new router whose description is '*DFTROUTE' and next hop is '10.10.10.1'
  hosts: ibmi

  roles:
    - role: present_ip_interface
      vars:
        present_ip_interface_ip_address: '10.10.10.10'
        present_ip_interface_netmask: '255.255.255.0'
        present_ip_interface_resource_name_of_ethernet_port: 'CMN03'
        present_ip_interface_next_hop: '10.10.10.1'
```

License
-------

Apache-2.0
