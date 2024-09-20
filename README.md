# HomeLab

## Intro

This repo holds the code for my ansible playbooks that I use to automate my homelab setup.

## Pre-Requisite

This setup requires poetry to be installed on the control node. Once poetry is installed run the following command `poetry install`

## Usage

### boot.yml

This playbook is responsible for doing the intial setup of the raspberry pi like the shell, prompt etc.

- Once the raspberry pi is booted we need to make sure it is reachable using the domain `astropi.local`
- Run the following playbook after the raspberry pi has booted up for the 1st time `poetry run ansible-playbook --verbose --inventory inventory/hosts --extra-vars '{"upgrade_prompt":false,"fetch_latest":false}' playbooks/boot.yml`
- Make sure the playbook runs without any errors
- Now login to your raspberry pi and change the login shell for the user
- Now logout of your raspberry pi and login again you will see that the `~/.zshrc` is being sourced
- Once this setup is complete run `sudo raspi-config`
- Update any required config and once done execute `sudo reboot`

### indi.yml

This playbook is responsible for installing INDI server and all the 3rd party drivers.

- Run the following playbook `poetry run ansible-playbook --verbose --inventory inventory/hosts --extra-vars '{"system_upgrade":false,"packages":["gsc","gsc-data","indi-full"]}' playbooks/indi.yml`
