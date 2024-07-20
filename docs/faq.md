# Frequently Asked Questions (FAQ)

## General

### What is Deployaroo?
Deployaroo is a sleek and intuitive web interface for deploying VMware vSphere virtual machine templates using Ansible. It simplifies the process of VM deployment and management.

### How do I access Deployaroo?
You can access Deployaroo by navigating to the URL where the application is deployed and logging in with your credentials set when installed.

## Installation

### What are the prerequisites for installing Deployaroo?
Deployaroo requires a VMware environment for deploying and configuring machines using Ansible. Make sure you have VMware vCenter Server 7.0.x+ installed and at least one templated virtual machine.

### How do I install Deployaroo?
You can install Deployaroo using Docker or directly on a Linux machine. Follow the detailed installation instructions in the [Installation Guide](installation.md).

## Configuration

### How do I set up VMware configuration in Deployaroo?
Navigate to **Settings > VMware Configuration** and enter the ESXi Host IP, vCenter DNS Name, vCenter User, and vCenter Password. Ensure the configuration is correct; the Host Status should change to **Reachable**.

### How do I set up default VM values?
Navigate to **Settings > Default VM Values**. Update the default values as needed, and make sure to configure the **Passwords (Global)** section with the template passwords for both Windows and Linux machines.

## Usage

### How do I deploy a virtual machine?
Navigate to the **Non-Domain** or **Domain** menu of the app and select your added Network, select an Image Type, configure the required settings, and press **Create VM** to start the deployment process. Detailed logs and progress tracking will be available in the History part of the application.

### How do I scan for VM images?
Navigate to **Settings > Virtual Machine Images** and press **Scan Images**. This will scan for playbooks and ensure they are correctly configured and ready for deployment.

## Troubleshooting

### What should I do if the Host Status is not Reachable?
Ensure that the IP address, DNS name, username and password for the VMware configuration are correctly entered in the settings. Verify network connectivity between Deployaroo and your VMware environment.

### How do I reset my password?
If you need to reset your password, navigate to **Settings > General Tab**, enter your current password followed by the new password and confirmation password, then press **Change Password**. Alternatively, this can also be done through **Settings** > **Users / Groups**.

### I'm recieving "ValueError: Fernet key must be 32 url-safe base64-encoded bytes."
Make sure you have correctly specified the **ENCRYPTION_KEY** in you **docker-compose.yml** file, OR created the appropriate environment variable for it if deploying using one of the other methods. The environment variable is **ENCRYPTION_KEY**.

### How can I get support for Deployaroo?
For support, you can contact me at [support@deployaroo.io](mailto:support@deployaroo.io) or submit an issue on the [GitHub page](https://github.com/blink-zero/deployaroo/issues).

## Contributing

### How can I contribute to Deployaroo?
I would absolutely love anyone to contribute! Please read the [contributing guidelines](contributing.md) to get started. You can also submit issues or feature requests on the GitHub page.

### Where can I find the source code for Deployaroo?
The source code for Deployaroo is available on the [GitHub repository](https://github.com/blink-zero/deployaroo).

---

**Simplify your VM deployments with Deployaroo**

[Get Started](getting-started/overview.md) | [View Demo (Coming soon)](#) | [Report Bug](https://github.com/blink-zero/deployaroo/issues) | [Request Feature](https://github.com/blink-zero/deployaroo/issues)
