[![Release](https://img.shields.io/badge/release-v1.0-blue.svg)](https://github.com/scaleflex/filerobot-uploader/releases)
[![Free plan](https://img.shields.io/badge/price-includes%20free%20plan-green.svg)](https://www.filerobot.com/en/home#2de3fb9f-dd4a-457a-999a-025ad9bd5f3b)
[![Contributions welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)](#contributing)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Scaleflex team](https://img.shields.io/badge/%3C%2F%3E%20with%20%E2%99%A5%20by-the%20Scaleflex%20team-6986fa.svg)](https://www.scaleflex.it/en/home)

[![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Manage%20and%20Accelerate%20your%20images%20and%20Digital%20Assets&url=https://scaleflex.github.io/filerobot-uploader/&via=filerobot&hashtags=uploader,reverse_CDN,image_resizing,image_editor,image_tagging,image_acceleration,image_compression,file_manager,asset_management)

<p align="center">
	<img
		height="175"
		alt="The Lounge"
		src="https://scaleflex.airstore.io/filerobot/robot-filerobot.png?sanitize=true">
</p>

<h1 align="center">
   Filerobot CLI
</h1>

This CLI provides all the functionality of the Filerobot and all of it's APIs.

<p align="center">
		<img
			width="600"
			alt="Filerobot CLI help"
			src="https://scaleflex.airstore.io/filerobot/cli/config.png?sanitize=true">
</p>


## Introduction

The purpose of the Command Line Interface is to provide a simple way of using the Filerobot APIs programmatically.

An example of argument of command:
```bash

filename.png
```
Where "filename.png" is an argument.

An example of flag to a specific command can be:

```bash
filerobot upload filename.png --method=PUT
```
Where "--method" is flag.

## Installation

### macOS 
```bash
sudo curl -L "https://github.com/scaleflex/filerobot-cli/releases/latest/download/filerobot-cli-darwin-x86_64" -o /usr/local/bin/filerobot && sudo chmod +x /usr/local/bin/filerobot
```

### Linux 
```bash
sudo curl -L "https://github.com/scaleflex/filerobot-cli/releases/latest/download/filerobot-cli-linux-x86_64" -o /usr/local/bin/filerobot && sudo chmod +x /usr/local/bin/filerobot
```

## Alias

If you want to add a different name of the command, you need to make an alias in your terminal profile, pointing to the executable file.
For example:

MacOS:
- Go into ~/.zshrc file and copy this command:
```bash
alias frb="/usr/local/bin/filerobot"
```

Linux:
- Go into ~/.bashrc file and copy this command:
```bash
alias frb="/usr/local/bin/filerobot"
```

Verify that installation works with:
```bash
filerobot version 
```

## Quick Start

```bash
# Set up your credetentials
filerobot config --token=mytoken --key=mysupersecretkey

# Enter into a directory and upload a file
filerobot upload face.png

# List a specific folder from Filerobot
filerobot list /test

# Inspect a specific resource
filerobot inspect bb1ce06f-2677-581a-85e7-28c00ec50000
```

## Commands
This section provides a general overview and example of the main commands.

You can check the list of all commands with:
```bash
filerobot --help
```

If you want to see a specific help message and instructions for a specific command, you can run:
```bash
filerobot upload --help
```

### ✔ config
Config command is used to set token and key provided by Scaleflex, needed for using Filerobot CLI.

#### Flags
    - token - token provided from Scaleflex
    - key - key provided from Scaleflex

#### Examples

```bash
filerobot config --token=mytoken --key=mysupersecretkey
```

### ✔ upload
Upload command is used to upload file to the Filerobot store. There are two types of uploading with POST and PUT requests.

#### Arguments
- filename - the name of the file that will be uploaded

#### Flags
- method - type of request POST or PUT, if it's not set default is POST.
- folder - location where the file will be uploaded, if it's not set default is "/".
- postprocess - type of postprocess that will be included, if it's not set postprocess will not be added.

#### Examples

```bash
filerobot upload face.png
```

```bash
filerobot upload face.png --method=PUT
```

```bash
filerobot upload face.png --method=PUT --folder=/test
```

```bash
filerobot upload http://sample.li/face.png -m URL -f test_folder --info "key":"value" --info "some":"other" --tags tag1 --tags tag2
```

```bash
filerobot upload face.png -m POST --tags other_tag
```

```bash
filerobot upload face.png -m POST --product-reference 10 --product-position 0
```

### ✔ list
List command is used to list all files and directories from the Filerobot store.

#### Arguments
  - Directory from where files and directories will be listed.

#### Flags
  - limit - The number of files and directories that will be listed. The range of limit is between 0 and 4000 (default 100).
  - offset - The number of offset (default 0).

**Note:** if you have directory or file that contains special characters, they need to be encoded.
Example folder named - `Crispy Menu` must be passed like this - `filerobot list Crispy%20Menu`

#### Examples

```bash
filerobot list /test
```

```bash
filerobot list /docs --limit=150 --offset=0
```

```bash
filerobot list /docs --limit=500
```
*Note*

### ✔ inspect
Inspect command is used to list information about given file by uuid

#### Arguments
  - file uuid

#### Examples

```bash
filerobot inspect bb1ce06f-2677-581a-85e7-28c00ec50000
```

### ✔ download
Download command is used to download file by uuid or filepath

#### Arguments
    - uuid/filepath of file

#### Flags
    - type - type of downloading(by filepath or uuid of file) default is uuid

#### Examples

```bash
filerobot download docs/boat.jpg --type=filepath
```

```bash
filerobot download bb1ce06f-2677-581a-85e7-28c00ec50000
```

- Download folder
```bash
filerobot download 907e26a8-4f62-58ca-8014-17aed514d84e
```

### ✔ move
Move command is used to move file to new directory(if not exist, it will be created)

#### Arguments
    - uuid of file to be moved
    - uuid/name of the new folder

#### Flags
    - type - the type of the new folder where file will be located (uuid or folder name) (default is folder name) 

#### Examples

```bash
filerobot move 5b12134e-70c6-5bd8-b49c-6264a08de5d7 /hello/world
```

### ✔ rename
Rename command is used to rename given file by uuid

#### Arguments
  - uuid of file
  - the new file name

#### Flags
  - name - new name of the file

#### Examples

```bash
filerobot rename bb1ce06f-2677-581a-85e7-28c00ec50000
```

```bash
filerobot rename bb1ce06f-2677-581a-85e7-28c00ec50000 --name=new_filename.jpg
```

### ✔ delete
Delete command is used to delete file by given uuid

#### Arguments
    - uuid of file

#### Examples

```bash
filerobot delete 22e8155e-4bdc-5476-9a0b-dbb09e750000
```

### ✔ version
Print the version number of Filerobot CLI

#### Examples

```bash
filerobot --version
```

```bash
filerobot version
```

### ✔ product
Product command gives possibility to operate with product ref and product position on files

#### Examples

```bash
filerobot product
```

```bash
filerobot product list
```

```bash
filerobot product list assets [product referrence]
```

```bash
filerobot product assign [uuid] -p 2 -r B012
```

### Advanced Usage

You can find advanced methods that can be used in Filerobot CLI.

#### Upload all your images that are located in the current directory and are with 'jpg' extension
```bash
for i in *.jpg; do filerobot upload $i -f /cli/upload; done
```

#### List all directories that are included in the custom dirs array
```bash
dirs=(/test /); for i in ${dirs[*]}; do filerobot list $i --limit=100 --offset=0; done
```

#### create text file (uuids.txt) that you want to inspect array of files uuids
  
- uuids.txt:

```bash
8bf63d53-f867-5b11-bcf9-7b4f13f50000
b6f4609b-6036-554f-b5e6-efa110f50001
3b6630bd-20a9-5813-8ece-b431bc250003
m26300bm-k872-57n1-8kl1-g831bc251234
```
```bash
file="uuids.txt"; while IFS=: read -r line; do filerobot inspect $line; done <"$file"
```
