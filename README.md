# Wazuh Kafka Integration

Monitor Apache Kafka logs using the Wazuh SIEM platform with custom decoders and rules.

This repository provides **custom Wazuh decoders** and **alert rules** to detect critical Kafka events, including **topic creation**, **topic deletion**, **broker restarts**, and more. It serves as a companion to the detailed walkthrough in the blog post linked below.

> **Read the full blog**:  
> [How to Monitor Kafka Logs with Wazuh SIEM](https://medium.com/@your-username/kafka-wazuh-guide-url)

---

## Repository Structure

```
wazuh-kafka-integration/
├── decoders/
│   └── kafka_decoder.xml       # Custom decoder for Kafka server.log & controller.log
├── rules/
│   └── kafka_rules.xml         # Wazuh rules for alerting on Kafka events
└── README.md
```

## Features

- Kafka log collection using the Wazuh agent
- Custom decoder for parsing `server.log` and `controller.log`
- Real-time alerts for:
  - Topic creation and deletion
  - Broker shutdowns/restarts
  - Controller state changes
  - Partition events
- Compatible with Kafka 2.8.2+ and Wazuh 4.x
- Clean and extensible XML structure

## Setup Instructions

### 1. Copy Decoder
Move the decoder XML file to the Wazuh manager:
```bash
sudo cp decoders/kafka_decoder.xml /var/ossec/etc/decoders/
```

### 2. Copy Rules
Move the rules XML file to the Wazuh manager:
```bash
sudo cp rules/kafka_rules.xml /var/ossec/etc/rules/
```

### 3. Restart Wazuh Manager
Apply the changes by restarting the Wazuh manager:
```bash
sudo systemctl restart wazuh-manager
```

### 4. Agent Configuration
To collect logs from Kafka, edit the Wazuh agent configuration file (`/var/ossec/etc/ossec.conf`):
```xml
<localfile>
  <log_format>syslog</log_format>
  <location>/home/kafka/kafka/logs/server.log</location>
  <out_format>$(timestamp) $(log)</out_format>
</localfile>

<localfile>
  <log_format>syslog</log_format>
  <location>/home/kafka/kafka/logs/controller.log</location>
  <out_format>$(timestamp) $(log)</out_format>
</localfile>
```

Then restart the Wazuh agent:
```bash
sudo systemctl restart wazuh-agent
```

### Log Paths
The decoder parses the following Kafka log files:
- `/home/kafka/kafka/logs/server.log`
- `/home/kafka/kafka/logs/controller.log`

Ensure Kafka is configured to write logs to these locations.

## Tested On

| Component       | Version         |
|-----------------|-----------------|
| Kafka           | 2.8.2           |
| Wazuh OVA       | 4.6.0+          |
| OS              | Ubuntu 20.04    |
| Agent           | Wazuh Agent 4.6 |

## Blog Companion
This repository complements the blog post:  
📖 [How to Monitor Kafka Logs with Wazuh SIEM](https://medium.com/@your-username/kafka-wazuh-guide-url)

The blog includes detailed setup steps, screenshots, explanations of decoders/rules, and testing tips.

## Contributing
Found a missing Kafka event? Open an issue or submit a pull request to extend decoder coverage.

## License
This project is licensed under the [MIT License](LICENSE).  
Feel free to use, modify, and distribute.

## Credits
Made with ❤️ by Padmja  
Follow me on [Medium](https://medium.com/@your-username) for more Wazuh and SIEM content.

</xaiArtifac

```t>