## Submission Guidelines

There are two ways to submit your activities. The primary method is to use the [website](#website-form), whereas the secondary is to send by [email](#email) to `founding.members (at) jsgenesis.com`.

What they both have in common is that you provide a .txt file that should be structured like this:

Scoring Period ID
Item ID, Date, Description, Link

eg.

### Text Example

**Scoring Period 1**
1. Community support
  - 01.02.2021
  - I assisted a user on telegram with how to become a validator.
  - some.telegram.link
2. Solved bounty #3
 - 02.02.2021
 - I completed bounty #3, and all success events were passed fully.
 - some.github.link

**Scoring Period 2**
1. Validator
  - 05.02.2021-09.02.2021
  - I was a validator from block #1337 to #11337
  - https://testnet.joystream.org/#/explorer
2. Content Creation
  - 05.02.2021-09.02.2021
  - Between these two dates, I created the channel "My Channel" with ID 1337, and uploaded videos:
    - 1342, 1347 and 1352
    - All videos are of high quality, and was approved by the curator in this forum post:
  - https://testnet.joystream.org/#/forum/threads/202?replyIdx=2

### Website Form

Using [this form](https://www.joystream.org/founding-members/form/) on the project website, there are four steps:
1. type/paste in the your membership `handle`
2. upload the .json to your browser (local storage only, your file will not be exposed)
3. type in your [keybase](https://keybase.io/) handle, and upload a .txt file of your activities
4. sign with your membership key and submit

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
- the .json is encrypted with [this]() pgp key, and sent to us


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
5. **Optional** encrypt the email with [this pgp]() key
6. Send!
