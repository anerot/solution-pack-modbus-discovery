# Release Information

- **Version**:  1.0.0
- **Certified**: No
- **Publisher**: ArnaudN
- **Compatible Version**: FortiSOAR v8.0.0 and above

# Overview

The **Modbus Discovery** solution pack has been developped to address a customer requirement to scan his network and search for new Modbus devices behind a Modbus gateway or directly reachable via IP.<br>
If a new Asset is discovered, FortiSOAR creates a new entry in the Asset module then raises an Alert.<br>
You can collect extra informations with the `Get modbus Device Information` playbook that use the Modbus function "Read Device Information (0x2B/0x0E)".<br>
It includes a specific playbook to collect the PM5561 details via Modbus.

# Next Steps

| [Installation](./docs/setup.md#installation) | [Configuration](./docs/setup.md#configuration) | [Usage](./docs/setup.md#usage) 
|------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
