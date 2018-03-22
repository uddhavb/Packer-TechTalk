## Packer Example

### Prerequisites
To run this example, set an environment variable named `DOTOKEN` which contains the API token for your Digital Ocean account.

### Try it out!
1. Copy the `packer` executable file in this directory.
2. Open the terminal and `cd` into this directory.
3. Run 
    * `./packer build basic.json` - Creates a Digital Ocean snapshot with `ansible` and `nodejs` preinstalled.
    * `./packer build ansible.json` - Creates a Digital Ocean snapshot configured using the contents of `packer.yml`