### Node Operators
Running a node, that is not a Validator will also earn you points, but in order for us to do so, you have to "report" to the [Joystream Telemetry](https://telemetry.joystream.org/#/Joystream) in addition to the official [Polkadot Telemetry](https://telemetry.polkadot.io). This also requires you identify yourself.

In order to that, name your node using the format `memberId-memberHandle`.
So if you are the member with id `133`, and handle `joystream` set it to `133-joystream`.

After your node is reporting to our telemetry, you will be able to get some information from it [here](https://telemetry.joystream.org/tracker/). Note that this page may see some changes going forward.

At the time of writing, you can submit data to the telemetry server in one of two ways. Using a [flag](#flags), or manually updating the [chain-spec file](#chain-spec-file) (note that we will update the chain spec file in the future, so this may not be necessary anymore).

#### Flags
Add the following two flags when (re-)starting your node:
```
--telemetry-url "wss://telemetry.joystream.org/submit 0" --telemetry-url "wss://telemetry.polkadot.io/submit/ 0"
```
Note that the latter (polkadot) is already on by default, but by adding just the first one (joystream) will override the settings and disable polkadots telemetry.

If you are running as a service using [this example](https://github.com/Joystream/helpdesk/tree/master/roles/validators#example-as-root), your "new" `joystream-node.service` file would be:

```
[Unit]
Description=Joystream Node
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/
ExecStart=/root/joystream-node \
        --chain joy-testnet-4.json \
        --pruning archive \
        --validator \
        --name <memberId-memberHandle> \
        --telemetry-url "wss://telemetry.joystream.org/submit/ 0" \
        --telemetry-url "wss://telemetry.polkadot.io/submit/ 0"
Restart=on-failure
RestartSec=3
LimitNOFILE=8192

[Install]
WantedBy=multi-user.target
```
After you made the changes and saved, type:

```
$ systemctl daemon-reload
$ systemctl restart joystream-node
```

Make sure to verify your node appears on both the telemetry servers, as you will not get points otherwise.

#### Chain Spec File
The other way is to update the chain spec file, namely `joy-testnet-4.json`.
Stop your node (eg. `systemctl stop joystream-node`) first before editing this file!

Lines 11-16 currently shows:
```
  "telemetryEndpoints": [
    [
      "/dns/telemetry.polkadot.io/tcp/443/x-parity-wss/%2Fsubmit%2F",
      0
    ]
  ],
```
This array of `telemetryEndpoints` must be changed to:
```
  "telemetryEndpoints": [
    [
      "/dns/telemetry.polkadot.io/tcp/443/x-parity-wss/%2Fsubmit%2F",
      0
    ],
    [
      "/dns/telemetry.joystream.org/tcp/443/x-parity-wss/%2Fsubmit%2F",
      0
    ]
  ],
```
After you have saved, you can start your node again.
