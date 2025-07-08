# wazuh-kafka-integration-

Monitor Apache Kafka logs using the Wazuh SIEM platform with custom decoders and rules.

This repository contains a complete set of **custom Wazuh decoders** and **alert rules** to detect key Kafka events such as **topic creation**, **topic deletion**, **broker restarts**, and more. It complements the full walkthrough available in the blog post below.

>  **Read the full blog**:  
> [How to Monitor Kafka Logs with Wazuh SIEM](https://medium.com/@your-username/kafka-wazuh-guide-url)

---

## **Repository Structure**

```bash
wazuh-kafka-integration/
├── decoders/
│   └── kafka_decoder.xml       # Custom decoder for Kafka server.log & controller.log
├── rules/
│   └── kafka_rules.xml         # Wazuh rules for alerting on Kafka events
└── README.md


**Features**
Kafka log collection using the Wazuh agent

Custom decoder for parsing server.log and controller.log

- Real-time alerts for:

- Topic creation and deletion

- Broker shutdowns/restarts

- Controller state changes

- Partition events

**Compatible with Kafka 2.8.2+ and Wazuh 4.x

Clean and extensible XML structure**

**Setup Instructions**
1. Copy Decoder
Move the decoder XML file to the Wazuh manager:
sudo cp decoders/kafka_decoder.xml /var/ossec/etc/decoders/

2. Copy Rules
Move the rules XML file as well:
sudo cp rules/kafka_rules.xml /var/ossec/etc/rules/

3. Restart Wazuh Manager
Apply the changes:
sudo systemctl restart wazuh-manager


Agent Configuration
To collect logs from Kafka, edit the Wazuh agent configuration:
File: /var/ossec/etc/ossec.conf

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

Then restart the agent:
sudo systemctl restart wazuh-agent

Log Paths
These files are parsed by the decoder:

- /home/kafka/kafka/logs/server.log

- /home/kafka/kafka/logs/controller.log

Make sure Kafka is configured to write logs to these locations.

Tested On
Component	Version
Kafka	2.8.2
Wazuh OVA	4.6.0+
OS	Ubuntu 20.04
Agent	Wazuh Agent 4.6

Blog Companion
This repository is a companion to the blog post:

📖 How to Monitor Kafka Logs with Wazuh SIEM

The post includes full setup steps, screenshots, decoder/rule explanations, and testing tips.

Contributing
Found a missing Kafka event? Open an issue or submit a PR to extend decoder coverage.

License
This project is licensed under the MIT License.
Feel free to use, modify, and distribute.

Credits
Made with ❤️ by Padmja
Follow me on Medium for more Wazuh + SIEM content.


