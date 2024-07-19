# Prerequisites

**Disclaimer:** This document is a working draft. Please submit an issue on the [GitHub page](https://github.com/blink-zero/deployaroo/issues) if you find any problems with it.

---

## VMware

Before installing Deployaroo, ensure your environment is correctly set up to handle the deployment and configuration of each Virtual Machine Image. Deployaroo relies on a VMware environment for deploying and configuring machines using Ansible.

### Recommended Setup

- **VMware vCenter Server 7.0.x+** installed
- At least one templated virtual machine for deployment

## Create a User in VMware vCenter

Creating a user in vCenter for deploying and configuring VMs ensures minimal privileges are assigned to your VMware environment.

### Required Privileges

Go to **Administration** > **Access Control** > **Roles** on your vCenter Server.

Clone the default **Read-Only** vSphere role and add the following privileges, Name your role (e.g., `deployaroo_role`).

| Category                       | Privilege                                                 | Reference                                          |
| ------------------------------ | --------------------------------------------------------- | -------------------------------------------------- |
| **Datastore**                  | Allocate space                                            | `Datastore.AllocateSpace`                          |
|                                | Browse datastore                                          | `Datastore.Browse`                                 |
|                                | Low level file operations                                 | `Datastore.FileManagement`                         |
| **Host**                       | Configuration > System Management                         | `Host.Config.SystemManagement`                     |
| **Network**                    | Assign network                                            | `Network.Assign`                                   |
| **Resource**                   | Assign virtual machine to resource pool                   | `Resource.AssignVMToPool`                          |
| **Virtual Machine**            | Change Configuration > Add new disk                       | `VirtualMachine.Config.AddNewDisk`                 |
|                                | Change Configuration > Add or remove device               | `VirtualMachine.Config.AddRemoveDevice`            |
|                                | Change Configuration > Advanced configuration             | `VirtualMachine.Config.AdvancedConfig`             |
|                                | Change Configuration > Change CPU count                   | `VirtualMachine.Config.CPUCount`                   |
|                                | Change Configuration > Change memory                      | `VirtualMachine.Config.Memory`                     |
|                                | Change Configuration > Change settings                    | `VirtualMachine.Config.Settings`                   |
|                                | Change Configuration > Change Resource                    | `VirtualMachine.Config.Resource`                   |
|                                | Change Configuration > Modify device settings             | `VirtualMachine.Config.EditDevice`                 |
|                                | Change Configuration > Set annotation                     | `VirtualMachine.Config.Annotation`                 |
|                                | Edit Inventory > Create from existing                     | `VirtualMachine.Inventory.CreateFromExisting`      |
|                                | Edit Inventory > Create new                               | `VirtualMachine.Inventory.Create`                  |
|                                | Edit Inventory > Remove                                   | `VirtualMachine.Inventory.Delete`                  |
|                                | Interaction > Configure CD media                          | `VirtualMachine.Interact.SetCDMedia`               |
|                                | Interaction > Configure floppy media                      | `VirtualMachine.Interact.SetFloppyMedia`           |
|                                | Interaction > Connect devices                             | `VirtualMachine.Interact.DeviceConnection`         |
|                                | Interaction > Inject USB HID scan codes                   | `VirtualMachine.Interact.PutUsbScanCodes`          |
|                                | Interaction > Power off                                   | `VirtualMachine.Interact.PowerOff`                 |
|                                | Interaction > Power on                                    | `VirtualMachine.Interact.PowerOn`                  |
|                                | Provisioning > Mark as virtual machine                    | `VirtualMachine.Provisioning.MarkAsVM`             |
|                                | Provisioning > Clone Template                             | `VirtualMachine.Provisioning.CloneTemplate`        |
|                                | Provisioning > Customize Guest                            | `VirtualMachine.Provisioning.CustomizeGuest`                     |
|                                | Provisioning > Deploy Template                            | `VirtualMachine.Provisioning.DeployTemplate`       |

### Assign Global Permissions

1. Log in to the vCenter Server at `https://<management_vcenter_server_fqdn>/ui` as `administrator@vsphere.local`.
2. Select **Menu** > **Administration**.
3. Create a service account in vSphere SSO if it does not exist:
    - In the left pane, select **Single Sign On** > **Users and Groups** and click on **Users**.
    - From the dropdown, select the domain to create the user (e.g., `example.com` or `vsphere.local`) and click **ADD**.
    - Fill in the username (e.g., `service_deployaroo`) and required details, then click **ADD** to create the user.
4. In the left pane, select **Access control** > **Global permissions** and click the **Add permissions** icon.
5. In the **Add permissions** dialog box, enter the service account (e.g., `service_deployaroo`), select the custom role (e.g., Deployaroo_role), and click **OK**.

## Virtual Machine Templates

Deployaroo comes with pre-written Ansible playbooks that use VMware templates. If these templates do not exist, the playbooks will fail. Ensure that:

- VM templates allow customization of the OS when deployed, this can be done by ensuring that WinRM and/or SSH are enabled respectively.
- The administrator account's username and password are consistent across all templates for playbook functionality. Change passwords after initial deployment on individual VM's.

### Option 1: Create VM Templates (Automated) - Recommended

A valuable repository: [vmware-samples/packer-examples-for-vsphere](https://github.com/vmware-samples/packer-examples-for-vsphere). It may be complex to set up initially but is extremely useful once configured. This tool contains all of the Deployaroo default Operating Systems plus more. Just be sure to convert from the VMware content store to a VM template after completion of build.

### Option 2: Create VM Template - Windows (Manual)

#### Summary

Manually creating and configuring a VM involves installing the OS, setting up unattended installation for Windows, running PowerShell scripts, installing VMware Tools, applying updates, setting up administrator account and converting the VM to a template.

#### Steps

1. **Create a New Virtual Machine in vSphere**
    - **Log in to vSphere Client**: Connect to the vCenter Server using the vSphere Client.
    - **Create a New VM**: Right-click on the cluster or host, select "New Virtual Machine," and follow the wizard:
        - **Name and Location**: Enter the VM name.
        - **Compute Resource**: Select the cluster or host.
        - **Storage**: Select the datastore.
        - **Compatibility**: Select the VM compatibility level.
        - **Guest OS**: Choose "Microsoft Windows" and "Windows Server (64-bit)".
        - **Customize Hardware**: Configure hardware settings (CPUs, memory, disk size, network, etc.).
        - **Finish**: Create the VM.

2. **Boot the VM and Install Windows**
    - **Power on the VM** and access the console.
    - **Boot from ISO**: Start the Windows installation and use `autounattend.xml` if available.

3. **Configure Unattended Installation** (Optional)
    - Ensure `autounattend.xml` is available during installation for necessary configurations.

5. **Install VMware Tools**
    - Manually install VMware Tools
    - [windows-vmtools.ps1](https://github.com/vmware-samples/packer-examples-for-vsphere/blob/develop/scripts/windows/windows-vmtools.ps1) (Optional)

6. **Run PowerShell Scripts for Configuration**
    - **Prepare and Execute Scripts**: Use the PowerShell below to configure the VM.
    - [windows-init.ps1](https://github.com/vmware-samples/packer-examples-for-vsphere/blob/develop/scripts/windows/windows-init.ps1)

7. **Apply Windows Updates**
    - **Run Windows Update**: Use PowerShell to apply updates:
      ```powershell
      Install-WindowsUpdate -AcceptAll -AutoReboot
      ```

8. **Enable local administrator account**
    - **Set password**
    - **Disable passsword expiration**
    - **Enable remote desktop** (Optional): This is personal preference

9. **Convert the VM to a Template**
    - **Shut Down the VM** and convert it to a template.

### Option 2: Create VM Template - Linux Ubuntu (Manual)

#### Summary

Manually creating and configuring a VM involves installing the OS, setting up cloud-init, Post-Installation configuration and converting the VM to a template. Similar proceedures apply to other distributions.

#### Steps

1. **Create a New Virtual Machine in vSphere**
    - **Log in to vSphere Client**: Connect to the vCenter Server.
    - **Create a New VM**: Right-click on the cluster or host, select "New Virtual Machine," and follow the wizard:
        - **Name and Location**: Enter the VM name.
        - **Compute Resource**: Select the cluster or host.
        - **Storage**: Select the datastore.
        - **Compatibility**: Select the VM compatibility level.
        - **Guest OS**: Choose "Linux" and "Ubuntu 64-bit".
        - **Customize Hardware**: Configure hardware settings (CPUs, memory, disk size, network, etc.).
        - **Finish**: Create the VM.

2. **Boot the VM and Install Ubuntu**
    - **Power on the VM** and access the console.
    - **Boot from ISO**: Start the Ubuntu installation and complete the setup.

3. **Configure Cloud-init**
    - Ensure `meta-data` and `user-data` files are available for initial configuration.

4. **Post-Installation Configuration**
    - **Create Administrator Account**: Create a user account named `administrator` and set a password:
      ```bash
      sudo adduser administrator
      sudo passwd administrator
      ```
    - **Grant Administrator Privileges**: Add the `administrator` user to the sudo group:
      ```bash
      sudo usermod -aG sudo administrator
      ```
    - **Enable SSH**: Ensure SSH is installed and enabled:
      ```bash
      sudo apt-get update
      sudo apt-get install openssh-server
      sudo systemctl enable ssh
      sudo systemctl start ssh
      ```
    - **Access the VM via SSH**: Connect using an SSH client.

5. **Install VMware Tools**
    - **Install VMware Tools**: Install VMware Tools for better performance and management:
      ```bash
      sudo apt-get update
      sudo apt-get install open-vm-tools
      ```

6. **Convert the VM to a Template**
    - **Shut Down the VM**: Shut down the VM from the vSphere Client.
    - **Convert to Template**: Right-click on the VM and select "Convert to Template".

---

**Disclaimer:** This document is a working draft. Please submit an issue on the [GitHub page](https://github.com/blink-zero/deployaroo/issues) if you find any problems with it.

---

## Next Step

To get started with Deployaroo, please refer to the [Installation Guide](../installation).