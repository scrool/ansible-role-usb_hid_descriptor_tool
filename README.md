# Ansible Role: `usb_hid_descriptor_tool`

Installs [USB HID Descriptor
Tool](https://www.usb.org/document-library/hid-descriptor-tool) - a tool to
create, edit and validate HID Report Descriptors. Creates XDG desktop file to
launch the tool.

## Requirements

- A recent version of Ansible. Tested on 2.9. It might work on previous versions.
- Fedora 31. It might work on other versions.
- Access to an archive of USB HID Descriptor Tool release. Either URL to
  download or path to a file.
- Package `desktop-file-utils` installed or role installs it from configured
  repositories which might connect to internet.
- Tool is Windows application so a package `wine-core` needs to be installed or
  role installs them from configured repositories which might connect to
  internet.

## Role Variables

All variables which can be overridden are stored in
[defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name                                           | Default Value | Description |
| ---------------------------------------------- | ------------- | ----------- |
| `usb_hid_descriptor_tool_archive_src`          | ""            | Path to an release archive of USB HID Descriptor Tool on a control host or URL to download the archive from. |
| `usb_hid_descriptor_tool_state`                | present       | By default installs the program. Set to "absent" to uninstall. |
| `usb_hid_descriptor_tool_top_dest_name`        | USB\_HID\_Descriptor\_Tool | Base name of installation directory and name part of a desktop file. |
| `usb_hid_descriptor_tool_install_parent_dir`   | /opt          | Parent directory in which program will be installed. See also `usb_hid_descriptor_tool_top_dest_name`. |
| `usb_hid_descriptor_tool_desktop_parent_dir`   | /usr/local/share/applications | Parent directory in which desktop file will be installed. See also `usb_hid_descriptor_tool_top_dest_name`. |
| `usb_hid_descriptor_tool_force_remove`         | no            | If set to "yes", contents of installation directory and desktop file are not compared against contents of `usb_hid_descriptor_tool_archive_src` when uninstall, upgrade or downgrade. |

## Example Playbook

### Install

To install the program, define URL to download USB HID Descriptor Tool release
archive from the internet.

```yaml
- hosts: all
  roles:
    - role: scrool.usb_hid_descriptor_tool
      vars:
        usb_hid_descriptor_tool_src: https://www.usb.org/sites/default/files/documents/dt2_4.zip
```

### Uninstall

To uninstall, set same values as for install. By default role removes content
only if installed directory and desktop file matches what it would install.
Finally set state variable to "absent".

Specify local path to a downloaded release archive file:

```yaml
- hosts: all
  roles:
    - role: scrool.usb_hid_descriptor_tool
      vars:
        usb_hid_descriptor_tool_archive_src: /tmp/dt2_4.zip
        usb_hid_descriptor_tool_state: absent
```

Alternatively you can enable option `usb_hid_descriptor_tool_force_remove` and
again set state variable to "absent". In this case role won't need nor even
check `usb_hid_descriptor_tool_archive_src`. This effectively removes
installation dir and desktop entry file. Example:

```yaml
- hosts: all
  roles:
    - role: scrool.usb_hid_descriptor_tool
      vars:
        usb_hid_descriptor_tool_state: absent
        usb_hid_descriptor_tool_force_remove: yes
```

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more
details.

## Author Information

- [Pavol Babinčák](https://github.com/scrool)
