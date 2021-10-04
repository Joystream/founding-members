Technical Help
===

Table of Contents
===

<!-- TOC START min:1 max:3 link:true asterisk:false update:true -->
  - [Overview](#overview)
    - [Node Operators](#node-operators)
    - [Validators](#validators)
    - [Signing Messages](#signing-messages)
<!-- TOC END -->

## Overview
This page will provide some technical help which should be useful for filling out your scoring summary and earning points.

### Node Operators
Running a node that is not a Validator will also earn you points, but in order for us to process such activity, you have to "report" to the [Joystream Telemetry](https://telemetry.joystream.org/#/Joystream) in addition to the official [Polkadot Telemetry](https://telemetry.polkadot.io). This also requires you identify yourself.

In order to that, name your node using the format `memberId-memberHandle`.
So if you are the member with id `133`, and handle `joystream` set it to `133-joystream`.

After your node is reporting to our telemetry, you will be able to get some information from it [here](https://telemetry.joystream.org/tracker/). Note that this page may see some changes going forward.

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
        --chain joy-testnet-5.json \
        --pruning archive \
        --validator \
        --name <memberId-memberHandle> \
        --log runtime,txpool,transaction-pool,trace=sync
Restart=on-failure
RestartSec=3
LimitNOFILE=10000

[Install]
WantedBy=multi-user.target
```
After you made the changes and saved, type:

```
$ systemctl daemon-reload
$ systemctl restart joystream-node
```

Make sure to verify your node appears on both the telemetry servers, as you will not get points otherwise.

### Validators
There are a couple of ways in which a Validator can find out when they started validating for themselves, but that require using the API. To make it a little easier, we will keep updated logs of all validators in each era and uploaded the data [here](/technical-help/validators.js). We will update this regularly, and you can find the blocks included at the top.

Open the file, and search for your `stash` key. Below it, you can find all the eras you were an _active_ Validator in. (The `totalEraPoints` denotes your cumulative `eraPoints`, meaning divide by 20 to get all the blocks you've ever produced!) Scroll to the bottom to find an overview of the eras, which includes the blockheight and timestamp of which it started. Now you should have all the information needed!


### Signing Messages

Under some circumstances, you may need to sign a message with your `membershipControllerAccount`, to identify yourself. Steps shown below:
1. Go to [pioneer](https://testnet.joystream.org/) (if you haven't already, click "Settings" and set "interface operation mode" to "Fully featured" and save.
2. Click "Toolbox", then select "Sign message". Choose your `membershipControllerAccount`, and unlock if necessary.
3. Paste in the data you want to sign, hit "Sign message", and copy the output!

#### Verify Signed Messages
1. Go to [pioneer](https://testnet.joystream.org/) (if you haven't already, click "Settings" and set "interface operation mode" to "Fully featured" and save.
2. Click "Toolbox", then select "Verify signature".
3. Paste or choose the address of the signer, paste in the data that has been signed, and finally the signature.
