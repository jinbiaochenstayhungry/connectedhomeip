# Matter Linux Light-switch Example

This example demonstrates the Matter Light-switch application on Linux platforms.

## Building

-   Install tool chain

          $ sudo apt-get install git gcc g++ python pkg-config libssl-dev libdbus-1-dev libglib2.0-dev ninja-build python3-venv python3-dev unzip

-   Build the example application:

          $ cd ~/connectedhomeip/examples/lighting-app/linux
          $ git submodule update --init
          $ source third_party/connectedhomeip/scripts/activate.sh
          $ gn gen out/debug --args="chip_build_libshell = true"
          $ ninja -C out/debug

## Testing the example

-   After successful commissioning, use the chip-tool to write the ACL in
    Lighting device to allow access from Lighting-switch device and chip-tool.

        $ ./out/debug/chip-tool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null },{"fabricIndex": 1, "privilege": 3, "authMode": 2, "subjects": [<LIGHT SWITCH NODE ID>], "targets": null }]' <LIGHTING APP NODE ID> 0

-   After successful commissioning, use the chip-tool for binding in
    Lighting-switch.

        $ ./out/debug/chip-tool binding write binding '[{"fabricIndex": 1, "node":<LIGHTING APP NODE ID>, "endpoint":1, "cluster":6}]' <LIGHT SWITCH NODE ID> 1

-   Test onoff cluster:

     Using matter shell toggle:
        matter switch onoff toggle


    Using matter shell on:

        matter switch onoff on

    off:

        matter switch onoff off
