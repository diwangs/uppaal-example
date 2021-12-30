# Time-Conscious Network Verification

## NetDice Model
`netdice_network_config.json` is the file for NetDice system.

To run it, follow the tutorial for running NetDice and run it with this config file. The result should be printed in standard output.

## UPPAAL Model
`packet-based.xml` and `host-based.xml` are the files for UPPAAL system. The former is the one currently developed. 

Steps to reproduce verification:
1. Download and run UPPAAL
2. Click on "Open System" in the menu bar
3. Point to the desired XML file
4. Click on the "Verifier" tab 
5. Select on a property and click "Check"
    - Only the top 2 properties are used
    - Properties with "Train" template is only used for development reference

## Details
There are 3 templates in this UPPAAL model:
- Packet 
- Link
- Switch

They all interact via 2 synchronization channels: `appr` and `leave`. `appr` is used by `packet` to give control of the model to a device (i.e. `link`, `switches`, and (later) `host`) and `leave` yields them. Both of these channels are indexed by the device and packet in context (e.g. `appr[device_id][packet_id]`).

### Packet
`packet` is the central template of the model. It describes the state where the packet is located (i.e. `on_sender`, `on_link`, etc.) and keeps track of the total duration the packet spent in-flight (via the `t` and `total` variable). 

Currently, this template also describes the static routing the packet must go through to arrive at a certain host, but this will be moved to the `switch` in the future.

### Link
`link` represents a link between `host` and `switch`. They have 2 features:
- A random delay between 2 threshold
- A random drop odds

For simplicity, currently, there is only one instance of `link` for the entire model (i.e. one instance of delay and drop odds). However, this can easily be made more expressive to declare different properties of multiple links by instantiating them more and changing the routing logic.

### Switch
`switch` represents a switch that will route packets to their desired destination. They have 3 features:
- A queue to hold multiple packets
- A logic to drop packets if the queue exceeds a certain threshold
- A random packet processing delay between two threshold 