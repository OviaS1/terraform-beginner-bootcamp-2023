# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This project is going to utilize semantic versioning for its tagging [semver.org](https://semver.org/)

The general format

**MAJOR.MINOR.PATCH**, eg.1.0.1

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

## Install terraform CLI

### Considerations with the Terraform CLI changes
THE Terraform installation has changed due to gpg keyring changes. It was therefore required to refer to the latest install CLI instructions via Terraform Documentation and change the scripting for install. 

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)


### Considerations for Linux Distribution

This project is built against Ubuntu. 
Please consider checking your Linux Distribution and change accordingly to distribution needs. 

[How to check OS Version in Linux](
https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/
)

Example checking OS Version
```

$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```



### Refactoring into Bash Scripts 

While fixing the Terraform CLI gpg depreciation issues we noticed the installation that the bash scripts steps were considerable amount more code. So we decided to create a bash script to install the Terraform CLI. 

This bash scripts is located here: [./bin/install_terraform_cli](./bin/install_terraform_cli)

- This will keep the Gitpod Task File ([.gitpod.yml](.gitpod.yml)) tidy. 
- This allow us an easier to debug and execute manually Terraform CLI install
- This will allow better portability for other projects that need to install Terraform CLI. 

#### Shebang Considerations
A Shebang (pronounced Sha-bang) tells bash scripts what program that will interpret the script. eg. `#!/bin/bash`

ChatGPT recommended this format for bash: `#!/usr/bin/env bash`

- for Portability for different OS distributions
- will serch the user's PATH for the bash executable


https://en.wikipedia.org/wiki/Shebang_(Unix)

### Executions Considerations

When executiong the bash script we can use the `./` shorthand notation to execute the bash scripts.

eg. `./bin/install_terraform_cli`

If we are using a script in .gitpod.yml we need to point the script to a program to interpret it. 

eg. `source ./bin/install_terraform_cli`

#### Linux Permissions Considerations 

In order to make our bash scripts executable we need to change linux permission for the fix to be executable at the user mode. 

```sh
chmod u+x ./bin/install_terraform_cli
```
```sh
chmod 744 ./bin/install_terraform_cli
```

https://en.wikipedia.org/wiki/Chmod


### Github Lifecycle (Before, Init, Command)

We need to be careful when using the Init because it will not rerun if we restart an existing workspace.

https://www.gitpod.io/docs/configure/workspaces/tasks
