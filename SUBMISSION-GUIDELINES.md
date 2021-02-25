## Submission Guidelines

There are two ways to submit your activities. The primary method is to use the form on our [website](#website-form), while the other is to send your summary by [email](#email) to `founding.members (at) jsgenesis.com`.

Note that in either case, make sure you include all your activities up until the end of the scoring round. When you have submitted for round `n`, you can no longer include any activity that **took place before the end of that round**. Hence, anything that was concluded in round `n-1` or `n`, will not be accepted. This rule is to prevent us awarding points for the same activity more than once.


### Text File
Your activities must be written up in a .txt file structured like this:

```
Scoring Period n`

1. Title
Date:
Description:
Link:
2. Title
Date:
Description:
Link:
...
m. Title
Date:
Description:
Link:

Scoring Period n+1
1. Title
Date:
Description:
Link:
...
```
Remember to include the person who "referred" you (made you aware of Joystream and/or the program) if applicable.

### Text Example
**Referred by**
Member ID: 1337
Member handle: `elite`
(skip this if not applicable)

**Scoring Period 1**
1. Community Assistance
Date: 01.02.2021
Description: I assisted a user on Discord with how to become a validator.
Link: some.discord.link

2. Solved bounty #3
Date: 02.02.2021
Description: I completed bounty #3, and all success events were passed fully.
Link: some.github.link

**Scoring Period 2**
1. Validator
Date: 05.02.2021-09.02.2021
Description: I was a validator from block #1337 to #11337, with stash account `5myStashAccount`. I have signed the message: `I am memberId n` with `5myStashAccount`, producing the signature `0x5a0fc80ec663ba3bf95e19f434ef999d86ec7ff8a95848f74d2111d1d54f62690bc1d31a13a9a156543e68401f87202a9ba73154aa20a4a8753baab850be038d`
Link: link.to.block.found
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
4. sign with your membership key and submit (membership key is the address 48 characters long, with it you paid for membership)

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
348a7fc8e95024edf2b21b0c95df0118950e70e67c1c7662f6c41859731ad4e2 /path/to/example.txt
```
Signing `e69eebba487a5ae13c0124d5b2bd38a4b289e23738f8b82ee0b7cb531e6761b3` with account `5CJzTaCp5fuqG7NdJQ6oUCwdmFHKichew8w4RZ3zFHM8qSe6`, returns the signature `0xc2db97479a07155416e2326b072cd4bfa16c0e6bd00025b38e4097552f431d46de01bcc9ee753e9c4aac0c51d53b1a1b70cf4d503685a948a5a88982ff7f2280`.

Which you can verify [here](https://testnet.joystream.org/#/toolbox/verify).
