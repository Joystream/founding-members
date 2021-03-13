Submission Guidelines
===

<!-- TOC START min:1 max:3 link:true asterisk:false update:true -->
  - [Overview](#overview)
    - [Text File](#text-file)
    - [Text Example](#text-example)
    - [Best Practices](#best-practices)
    - [Website Form](#website-form)
    - [Email Submission](#email-submission)
<!-- TOC END -->


## Overview
There are two ways to submit your activities. The primary method is to use the form on our [website](#website-form), while the other is to send your summary by [email](#email) to `founding.members (at) jsgenesis.com`.

Note that in either case, make sure you include all your activities up until the end of the scoring round. When you have submitted for round `n`, you can no longer include any activity that **took place before the end of that round**. Hence, anything that was concluded in round `n-1` or `n`, will not be accepted. This rule is to prevent us awarding points for the same activity more than once.


### Node Operators and Validators
Many have been asking how to add their Validator or node-operating activity to their [text files](#text-file) in order to get points. A previous example was somewhat poor in that regards, so this has now been updated and improved.

More information on how to find out your node or validator "uptime" can be found [here](/technical-help/README.md).

### Text File
Your activities must be written up in a .txt file structured like this:

```
I am
Member ID: <myId>
Member handle: <myHandle>
Membership Controller: <5myMemberShipControllerAccount>

Referred by
Member ID: <referrerId>
Member handle: <referrerHandle>
(skip this if not applicable)

Scoring Period <i>:

1. Title
Date:
Description:
Link?:
Signature?:
2. Title
Date:
Description:
Link?:
Signature?:
...
n. Title
Date:
Description:
Link?:
Signature?:

Scoring Period <i+1>
1. Title
Date:
Description:
Link?:
Signature?:
...
```
Remember to include the person who "referred" you (made you aware of Joystream and/or the program) if applicable.

### Text Example
**I am**
Member ID: `133`
Member handle: `joystream`
Membership Controller: `5CJzTaCp5fuqG7NdJQ6oUCwdmFHKichew8w4RZ3zFHM8qSe6`

**Referred by**
Member ID: `1337`
Member handle: `elite`
(skip this if not applicable)

**Scoring Period 1**
1. Community Assistance
Date: 01.02.2021
Description: I assisted a user on telegram with how to become a validator.
Link: some.telegramOrDiscord.link

2. Solved bounty #3
Date: 02.02.2021
Description: I completed bounty #3, and all success events were passed fully.
Link: some.github.link

**Scoring Period 2**
1. Validator
Date: 05.02.2021-09.02.2021
Description: I was a validator from block/era #1337/2 to #11337/10, with stash account `5myValidatorStashAccount`. (I was active in all the eras in this range, and found a total of 1000 blocks.)
I have signed the message: "I am member id/handle `133/joystream` with `5myValidatorStashAccount`" with my membership ctrl account - `5CJzTaCp5fuqG7NdJQ6oUCwdmFHKichew8w4RZ3zFHM8qSe6`
Signature: `0xbef075b361b6c36c4abbeea47b40b1cc3652c3d6ea7917a83d6ee8231fd1e12286c3d23f475bd98cb001fc182b9a21674cc01b7dbedbb2f59216bb0b6c35138b`

2. Content Creation
Date: 05.02.2021-09.02.2021
Description: Between these two dates, I created the channel "My Channel" with ID 1337, and uploaded videos with ID 1342, 1347 and 1352. All videos are of high quality, and was approved by the curator, ref forum post below.
Link: link.to.forum.post

### Best Practices
- Keep it brief, but include all relevant information.
- In cases when your activity took place of in the form of a pull request, (eg. a bounty, bug fix, etc.), use the date of which the PR was merged or closed.
- If you reported a bugfix, or made an issue for other purposes, use the date on which the issue was opened.
- If you've held a role, the date range should be the dates you are requesting points for. However, you are also encouraged to specify when you got the role.


### Website Form

Using [this form](https://www.joystream.org/founding-members/form/) on the project website, there are four steps:
1. type/paste in the your membership `handle`
2. upload the .json to your browser (local storage only, your file will not be exposed)
3. type in your [keybase](https://keybase.io/) handle (if you don't have keybase, get an account so we can contact you there), and upload a .txt file of your activities
4. [sign with your membership key](https://testnet.joystream.org/#/toolbox/sign) and submit (membership key is the address 48 characters long, with it you paid for membership) 
_Note: You may need to enable access to the Toolbox page here: `Settings -> General -> Interface operation mode` (Change it to Fully featured)_


What happens under the hood is the following:
- your address is looked up on chain, and matched with your membership `handle` and `id`
- your uploaded key is verified to be the "correct" one, and unlocked with your password (if applicable)
- the content of your .txt file is hashed and signed
- along with the remaining information provided, your uploaded .txt file is converted into a .json file structured as so:
```JSON
{
  "membershipHandle": "yourHandle",
  "ctrlAccount": "5yourControllerAddress",
  "keybaseHandle": "yourKeybaseHandle",
  "textFile": {
      "name": "nameOfYourTextFile.txt",
      "data": "contentOfYourourTextFile.txt"
  },
"signature": "0xsignatureInHex"
}
```
- the .json is encrypted with [this pgp key](/data/pubkey.asc), and sent to us


### Email Submission

For sending by email, you need to perform some of the work manually:

1. Create the textfile, following the [example](#text-example)
2. Hash the entire file with SHA256
3. Sign the hash with your membership ctrl key [here](https://testnet.joystream.org/#/toolbox/sign)
4. Compose an email like so:
Membership Handle: `yourHandle`
Ctrl Account: `5yourControllerAddress`
Keybase Handle: `yourKeybaseHandle`
Text file name: `nameOfYourTextFile`
Hashing algorithm: `SHA256`
Signature: `0xsignatureInHex`
5. **Optional** encrypt the email with [this pgp key](/data/pubkey.asc)
6. Send!

---

With the example above, as replicated as [example.txt](/data/example.txt):
```
$ shasum -a256 /path/to/example.txt
2471b5c2bad70e523af98e436ae7ac8416bd4ca4ce4cd4e38d7a058f089fe1fe /path/to/example.txt
```
Signing `2471b5c2bad70e523af98e436ae7ac8416bd4ca4ce4cd4e38d7a058f089fe1fe` with account `5CJzTaCp5fuqG7NdJQ6oUCwdmFHKichew8w4RZ3zFHM8qSe6`, returns the signature `0x14cd1628f2ae8fa9ec549cfcbe899482439183896c2587022b663c59f0e1de3252a07b7f3153152956b9641354490f74a289e94adce38d0d81f0a52bcdc3c48c`.

Which you can verify [here](https://testnet.joystream.org/#/toolbox/verify).  
_Note: You may need to enable access to the Toolbox page here: `Settings -> General -> Interface operation mode` (Change it to Fully featured)_```
