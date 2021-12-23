# Time-Conscious Network Verification

## UPPAAL Model
`packet-based.xml` and `host-based.xml` are the files for UPPAAL system. The former is the one currently developed. 

Steps to reproduce verification:
1. Download and run UPPAAL
2. Click on "Open System" in the menu bar
3. Point to the desired XML file
4. Click on the "Verifier" tab 
5. Select on a property and click "Check"
    - Only the top 2 blocks of properties are used
    - Properties with "Train" template is only used for development reference

## NetDice Model
`netdice_network_config.json` is the file for NetDice system.

To run it, follow the tutorial for running NetDice and run it with this config file. The result should be printed in standard output.