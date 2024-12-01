# Home Assistant Shelly State Refresh Automation Generator

This project generates the automation YAML content to handle **Shelly device state refreshes** in Home Assistant. Sometimes, Shelly devices remain in an "unknown" or "unavailable" state, and this automation will reboot the Shelly devices to ensure their state is correctly updated.

### What it does:
- Generates the automation YAML content for monitoring Shelly devices and rebooting them when their state becomes "unknown" or "unavailable."
- Automates the reboot process to refresh the state and ensure proper status reporting to Home Assistant.
- The devices are listed in the `all.yml` file, and the generated automation includes all listed devices.

### Quickstart:

1. **Prepare the `all.yml` file**:
   - Copy the `all.yml.tpl` file to `all.yml`.
   - Populate `all.yml` with your Shelly devices.

2. **Register in inventory your ssh connection to Home Assistant or only copy it over from local created file later**

3. **Run the Ansible playbook** to generate the automation:
   ```bash
   ansible-playbook main.yml
   ```

4. **If you dont use ssh connection to Home Assistant, copy the generated `automation.yaml` files content into your automation file in Home Assistant**

### Automation Logic:

The generated automation does the following:
- **Triggers**: Watches for Shelly device states (`unavailable` or `unknown`) as well as the startup of Home Assistant.
- **Actions**: If a Shelly device is in an undesirable state (i.e., "unknown" or "unavailable"), it triggers a reboot via MQTT.
  
### Why is this necessary?
Occasionally, Shelly devices can get stuck in an "unknown" or "unavailable" state, which prevents Home Assistant from getting accurate status updates. This automation forces a reboot to refresh the device state and allow Home Assistant to receive updated information.