| [Home](../README.md) |
|-----------------------------------------------------------------------------------------------------------------|

# Installation

1. To install a solution pack, click **Content Hub** > **Discover**.
2. From the list of solution packs that appears, search for and select **Modbus Discovery**.
3. Click the **Modbus Discovery** solution pack card.
4. Click **Install** on the bottom to begin the installation.

## Operation Modes
The Solution Pack operates either in:

- **Simulation Mode:** This mode allows you to run the `Modbus Devices Discovery` playbook without scanning your network. To turn demo mode on, you simply need to edit the `Modbus Devices Discovery` playbook, edit the step `Configuration` and set the `UseMockOutput` variable to `true`.
- **Live Mode:** If you want to use the solution pack in your production, the above variable has to be set to `false`. Furthermore some prerequisites are required, the list is available under Prerequisites section of this document

## Prerequisites

The **Modbus Discovery** solution pack depends on the following connector that is installed automatically &ndash; if not already installed.

| Connector Name                | Purpose                                                             |
|:----------------------------------|:--------------------------------------------------------------------|
| Modbus                     | Required for Modbus Discovery                              |
| NMAP Scanner                     | Required for network Discovery                              |


### Prerequisites for Live Mode
Edit the `Modbus Devices Discovery` playbook available in your Playbook Collection `10 - SP - Modbus Discovery`.<br>
Edit the `Configuration` step to modify:
- Simulation mode turned off : `UseMockOutput` variable to `false`<br>

# Configuration

The `Modbus` and `NMAP Scanner` connectors need a default configuation. No parameter required to configure them.<br>
<br>
Edit the `Modbus Devices Discovery` playbook available in your Playbook Collection `10 - SP - Modbus Discovery`.<br>
Edit the `Configuration` step to modify:
- IPrange (Range or unique IP): ie 172.18.20.5-40 or 192.168.3.0/24.
- modbus_port (Range or unique port): ie 502-504 or 502.
- startId (address_ID of the modbus devices to scan): ie 1.
- endId (address_ID of the modbus devices to scan): ie 10.
- timeout (time to wait in second for the modbus answer): ie 2.
- modbus_address (Registry address used for the modbus scan): ie 0.<br>
<br>
Note: The step `Modbus Scan Gateway` performs (in parallel for each NMAP positive result) a Modbus address discovery to the discovered IP/Port from the addressID `startId` to `endId`. It consists in executing a "READ_HOLDING_REGISTERS (0x03)=Func03" of the `modbus_address` and wait the defined `timeout` for an answer with a default of 3 retries.

# Usage
## Start a Discovery
You can start a discovery manually or with the scheduler by executing the `Modbus Devices Discovery` playbook.<br>
If a new modbus asset is discovered then a new asset is created in the `Asset` module.
<img width="1484" height="774" alt="image" src="https://github.com/user-attachments/assets/a031392a-e840-4176-a1eb-e9e2372abdb0" /><br>
<br>
You can execute the playbook `Get modbus Device Information` or `Get PM5561 Details` to retreive more asset information via the Modbus function Read Device Information (0x2B/0x0E).
<img width="1101" height="623" alt="image" src="https://github.com/user-attachments/assets/0f552bcd-3790-49d6-b790-c1ec764b1254" /><br>

## Raise an Alert
If you enable the playbook `Alerts for new Asset discovery` then an Alert is raised each time a new Modbus Asset is discovered by FortiSOAR.<br>
<img width="923" height="650" alt="image" src="https://github.com/user-attachments/assets/05d927fa-5251-4485-a059-d1ead1b3f72f" />

