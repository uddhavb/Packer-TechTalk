# Packer
Packer by HashiCorp

#### What is Packer?
[Packer](https://www.packer.io/) is an open source tool for creating identical machine images for multiple platforms from a single source configuration. Packer is lightweight, runs on every major operating system, and is highly performant, creating machine images for multiple platforms in parallel. Packer does not replace configuration management like Chef or Puppet. In fact, when building images, Packer is able to use tools like Chef or Puppet to install software onto the image.

A machine image is a single static unit that contains a pre-configured operating system and installed software which is used to quickly create new running machines.

#### Install Packer
Windows:
1. [Download for Windows](https://releases.hashicorp.com/packer/1.2.1/packer_1.2.1_windows_386.zip)
2. Store file in some directory (say `D:/packer`) and unzip it there.
3. To run packer, execute shell command `D:/packer/packer`


Linux:
1. To install Packer:(check [link](https://www.packer.io/downloads.html) for specific OS versions)
```
mkdir ~/packer
cd ~/packer
wget https://releases.hashicorp.com/packer/1.2.1/packer_1.2.1_linux_386.zip?_ga=2.136427760.1195142724.1521659529-903724582.1521659529 -O packerzip
unzip packerzip
rm packerzip
```
2. To run packer:
```
~/packer/packer build config.json
```

#### Packer to create VM image:
1. Create JSON files to create images.
- Create a local VM image for [VirtualBox](https://www.virtualbox.org/):
```
{
  "type": "virtualbox-iso",
  "guest_os_type": "Ubuntu_64",
  "iso_url": "http://releases.ubuntu.com/16.04/ubuntu-16.04.4-desktop-i386.iso",
  "ssh_username": "packer",
  "ssh_password": "packer",
  "shutdown_command": "echo 'packer' | sudo -S shutdown -P now"
}
```

- Create a server image on cloud. [DigitalOcean](https://www.digitalocean.com/) example:
```
{
 "builders": [{
        "type": "digitalocean",
        "droplet_name": "packer",
        "api_token": "YOUR API KEY",
        "image": "ubuntu-16-04-x64",
        "region": "nyc3",
        "size": "1gb",
        "ssh_username": "root"
 }]
}
```

2. Run script using Packer:
```
// cd into the directory where your JSON file lies and run this command.
path_to_packer_file/packer build your_json.json
```

#### Using packer to create machines containing required dependencies:
An example, is to create an image to run ansbible scripts:
```
{
  "provisioners": [
    {
      "type": "ansible",
      "playbook_file": "./playbook.yml"
    }
  ],

  "builders": [
    {
      "type": "digitalocean",
      "api_token": "YOUR_API_TOKEN",
      "image": "ubuntu-14-04-x64",
      "region": "sfo1"
    }
  ]
}
```
## Presentation Slides:
You can find the presentation slides for this talk [here](https://docs.google.com/presentation/d/1DY4p2RDxU34tVHz7GViBL_gEbb5mVXfVw5fCvS-utig/edit?usp=sharing).

## Demonstration:
You can have a look into the usage and working of Packer from [this](https://www.google.com/) example.
