| [Home](../README.md) |
|-----------------------------------------------------------------------------------------------------------------|

# Installation

1. To install a solution pack, click **Content Hub** > **Discover**.
2. From the list of solution packs that appears, search for and select **Modbus Discovery**.
3. Click the **Modbus Discovery** solution pack card.
4. Click **Install** on the bottom to begin the installation.

## Operation Modes
The Solution Pack operates either in:

- **Simulation Mode:** This mode allows you to run the "Modbus Devices Discovery" playbook without adding Assets nor connector config in FortiSOAR and observe the User Input workflow. To turn demo mode on, you simply need to edit the `Start Group` playbook, edit the step `Configuration` and set the `UseMockOutput` variable to `true`.
- **Live Mode:** If you want to use the solution pack to handle your production Asset Upgrade, the above variable has to be set to `false`. Furthermore some prerequisites are required, the list is available under Prerequisites section of this document

## Prerequisites

The **Asset Upgrade Management** solution pack depends on the following connector that is installed automatically &ndash; if not already installed.

| Connector Name                | Purpose                                                             |
|:----------------------------------|:--------------------------------------------------------------------|
| Asset Upgrade                     | Required for Asset Upgrade Management                              |


### Prerequisites for Live Mode
- Demo mode turned off : `UseMockOutput` variable to `false`
- `Asset Upgrade` connector with as many configuration name as different username/password tuple to authenticate on your devices.
- The firmware file added as Attachment with `Type` defined as `Firmware`
- Assets in the Asset List

# Configuration

- The `Asset Upgrade` connector will store the username/password you will use to authenticate. If you use some different username/password for other devices then you have to create multiple `Configuration` in your connector. The Configuration name case is important and has to be the same than your Asset Config Name value.


# Usage
## Preparing for an Upgrade
Before starting your upgrade, verify that :
- You have a valid Firmware uploaded in `Attachments`
- Your Asset Upgrade Status is `To Be Upgraded` (Mandatory for the `Start Group` playbook)
### Add Asset
Add your Assets in the Asset List by specifying:
- IP Address : a valid IPv4 address or FQDN to access your Asset
- Asset Config Name: the EXACT Configuration name to use as username/password that you created your `Asset Upgrade` connector.
- Asset Group ID: The Group/Deployment that your asset is part of. You can manage multiple switches deployment in different location or zone by specifying a different Asset Group ID
- Rank: The position of your Asset related to the order/rank/position you want to upgrade it compared with your other Assets in the same Asset Group ID.
- Vendor: It will determine witch upgrade scenario the "Start Group" playbook will use.
- Upgrade Status:
    - Failed - A previous Upgrade attempt Failed. See your Asset Comments for details.
    - Success - The default value.
    - To Be Upgraded - Your Asset is ready for Upgrade.
- Asset Category: This filed is optional but could be used for future scenario.
- Display Name: The name of your Asset
- Hostname: The hostname of your Asset

### Add a Firmware
In your navigation pane, go to `Attachments` page and add a new attachment.<br>
Define a name, upload the firmware in the "File" section and select `Firmware` in the drop/down list of Attachment `Type`. <br>
Note: The upgrade playbook will filter the available Attachment based on Attachment Type = Firmware



## Start an Upgrade
You can start your upgrade in two ways:
- Click on the Playbook button <img width="110" height="35" alt="image" src="https://github.com/user-attachments/assets/c36995d1-7dad-49ce-aeac-78782ba9c436" /> located in your `Asset Upgrade Management/Asset List` navigation menu to start an upgrade based on Group and Rank.
- Select one or multiple Assets in your Asset List and execute the playbook `Upgrade Selected`.

### Upgrade with <img width="110" height="35" alt="image" src="https://github.com/user-attachments/assets/c36995d1-7dad-49ce-aeac-78782ba9c436" /> playbook
#### Once you start the upgrade you will be prompted to specify the AssetGroup you want to upgrade
<img width="860" height="534" alt="image" src="https://github.com/user-attachments/assets/14469025-e1d7-4866-88cc-e14811cf842f" /> <br>
- Specify the Asset Group ID to upgrade and click OK.<br>
Note: The User Input provides you the Asset count() in each Asset Group
#### Select the rank to upgrade
<img width="861" height="463" alt="image" src="https://github.com/user-attachments/assets/9bbe8085-e01f-47e1-b009-c36d50a49d53" /> <br>
- Specify the Rank number and click OK.<br>
Note: The User Input provides you the Asset count() in each Rank
#### Select the Firmware
<img width="863" height="612" alt="image" src="https://github.com/user-attachments/assets/b1036ae5-eca9-41a6-80b3-067f7b5c77ba" /> <br>
- Specify the Firmware ID you want to use for the upgrade process and click OK.<br>
Note: The User Input provides you the Asset list in your selected Asset Group and Rank

Once the Upgrade finishes, the `Upgrade Status` of your Assets will change according with the Playbook execution result.<br>
- Success: the Upgrade is a success. If you edit your Asset you will see the `Configuration Backup` attached to the `Asset`.
- Failed: the Upgrade Failed. If you edit your Asset and open the Workspace for `Comments` you will see the failure reason.
<img width="1786" height="717" alt="image" src="https://github.com/user-attachments/assets/e1bacc97-1ba1-4448-b7e9-3d06f105bfb3" />

### Upgrade by selecting one or multiple Assets 
#### Select the Assets in the `Asset List`, click `Execute` and select `Upgrade Selected`
<img width="1503" height="495" alt="image" src="https://github.com/user-attachments/assets/e9e0435c-f4da-4feb-8637-251e65167fa5" /><br>
#### Specify the Firmware to use
<img width="859" height="630" alt="image" src="https://github.com/user-attachments/assets/fc871f05-9997-4521-8c25-fffba59975d9" /><br>
- Specify the firmware ID you want to use for the upgrade and click OK.<br><br>
Note: The User Input shows you Attachments of "Firmware" type, but also all the selected switches even if they are not marked as `To Be Upgraded`. The Upgrade is executed simultaneously on BOTH selected Assets.
