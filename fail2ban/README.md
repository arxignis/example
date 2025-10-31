# Example Integrations

This directory contains example integrations and configurations for Arxignis.

## Fail2Ban Integration

The `fail2ban/` directory contains a Fail2Ban action file that integrates with the Arxignis API to automatically block malicious IP addresses.

### Setup

1. Copy the action file to your Fail2Ban actions directory:
   ```bash
   sudo cp fail2ban/arxignis.conf /etc/fail2ban/action.d/
   ```

2. Set appropriate permissions (the file contains your API token):
   ```bash
   sudo chmod 640 /etc/fail2ban/action.d/arxignis.conf
   ```

3. Edit the configuration file and add your Arxignis API token:
   ```bash
   sudo nano /etc/fail2ban/action.d/arxignis.conf
   ```
   Set the `axtoken` value in the `[Init]` section.

4. Configure your jail to use the Arxignis action by editing your jail configuration:
   ```bash
   sudo nano /etc/fail2ban/jail.local
   ```
   Add or modify the action parameter:
   ```
   action = iptables-multiport[arxignis]
   ```

### Requirements

- `curl` (required)
- `jq` (optional, for JSON parsing)
- Arxignis API token (available from your Arxignis dashboard)

### Configuration Options

- `axtoken`: Your Arxignis API Bearer token
- `expiration`: Block expiration time in seconds (default: 600 = 10 minutes)

When an IP is banned, it will be automatically reported to Arxignis and blocked via the API. Unban actions will also be sent to remove the block.
