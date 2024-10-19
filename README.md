# Home Assistant Shelly State Refresh Automation Generator

This project generates the automation YAML content to handle **Shelly device state refreshes** in Home Assistant. Sometimes, Shelly devices remain in an "unknown" or "unavailable" state, and this automation will reboot the Shelly devices to ensure their state is correctly updated.

### What it does:
- Generates the automation YAML content for monitoring Shelly devices and rebooting them when their state becomes "unknown" or "unavailable."
- Automates the reboot process to refresh the state and ensure proper status reporting to Home Assistant.
- The devices are listed in the `vars.yml` file, and the generated automation includes all listed devices.

### Quickstart:

1. **Prepare the `vars.yml` file**:
   - Copy the `vars.yml.template` file to `vars.yml`.
   - Populate `vars.yml` with your Shelly devices.

2. **Run the Ansible playbook** to generate the automation:
   ```bash
   ansible-playbook playbook.yml
   ```

3. **Copy the generated automation**:
   - After the playbook runs, a file called `automation.yaml` will be created.
   - Copy the content of this file into the **YAML view** of a new automation in the Home Assistant UI.

### Automation Logic:

The generated automation does the following:
- **Triggers**: Watches for Shelly device states (`unavailable` or `unknown`) as well as the startup of Home Assistant.
- **Actions**: If a Shelly device is in an undesirable state (i.e., "unknown" or "unavailable"), it triggers a reboot via MQTT after a 1-minute delay.
  
### Why is this necessary?
Occasionally, Shelly devices can get stuck in an "unknown" or "unavailable" state, which prevents Home Assistant from getting accurate status updates. This automation forces a reboot to refresh the device state and allow Home Assistant to receive updated information.