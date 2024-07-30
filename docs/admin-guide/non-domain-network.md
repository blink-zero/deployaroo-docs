# Adding a Non-Domain Network

## 1. Accessing the Non-Domain Network Settings

### Navigate to Non-Domain Networks

> **Tip**: Ensure you have the necessary permissions to add and manage networks before proceeding.

1. **Access the Non-Domain Menu:**
    * Locate and click on the **Non-Domain** item in the left-hand navigation menu.

2. **Initiate Network Addition:**
    * Look for and select the **Add Network** option within the Non-Domain section.

![Non-Domain Add Network](../assets/screenshots/non_domain_add_network.png)

## 2. Configuring Network Details

### Fill in Network Information

> **Important:** Accurate network details are crucial for successful VM deployments. Double-check all information before saving.

1. **Enter Network Specifics:**
    * Fill in all relevant details related to the network where you will deploy virtual machines.
    * This will include:
        - Network name
        - IP address range
        - Subnet mask
        - Default gateway
        - DNS servers

2. **Customize Network Name:**
    * Choose a network name that aligns with your VMware environment naming conventions.
    * Ensure the name is descriptive and easily identifiable for future reference.

![Non-Domain Add Network Details](../assets/screenshots/non_domain_add_network_details.png)

## 3. Finalizing Network Creation

### Save and Verify Network Configuration

> **Note:** The dropdown items in the network configuration form will be populated with information retrieved from the VMware vCenter API.

1. **Create the Network:**
    * After entering all required details, locate and press the **Create Network** button.
    * This action will add the network under the Non-Domain menu item.

2. **Verify Network Addition:**
    * Check that the newly added network appears in the list of Non-Domain networks.
    * Confirm that all details are correct as entered.

3. **Add Multiple Networks (Optional):**
    * If needed, repeat this process to add multiple non-domain networks.
    * Each network can be customized to suit different deployment requirements or environments.

## Next Steps

After adding your non-domain network(s), you may want to:

* [Deploy VMs on Non-Domain Networks](../../admin-guide/deploying-vms)
* [Add a Domain Network](../../admin-guide/domain-network)

---

**Simplify your VM deployments with Deployaroo**

[Get Started](getting-started/overview.md) | [View Demo (Coming soon)](#) | [Report Bug](https://github.com/blink-zero/deployaroo/issues) | [Request Feature](https://github.com/blink-zero/deployaroo/issues)
