# profile-example

### Master:
- [![profile-example](https://github.com/osx-provisioner/profile-example/actions/workflows/push.yml/badge.svg?branch=master)](https://github.com/osx-provisioner/profile-example/actions/workflows/push.yml)

### Production:
- [![profile-example](https://github.com/osx-provisioner/profile-example/actions/workflows/push.yml/badge.svg?branch=production)](https://github.com/osx-provisioner/profile-example/actions/workflows/push.yml)

## About

An example Mac Maker profile.

Use [Mac Maker](https://github.com/osx-provisioner/mac_maker) to apply this profile to a Mac that is ready to setup.

## Profile Folder

This repository has a [profile](profile) folder that contains the following required configuration, plus additional settings:
                                                                
| -- Filename ----------------| -- Description -------------------------------------------------------------- |
|-----------------------------|-------------------------------------------------------------------------------|
| [.ansible-lint](profile/.ansible-lint)       | configuration for [ansible-lint](https://ansible-lint.readthedocs.io/en/latest/)    |
| [.yamllint](profile/.yamllint)               | configuration for [yamllint](https://yamllint.readthedocs.io/en/stable/)            |
| [install.yml](profile/install.yml)           | the main [ansible](https://ansible.com) provisioning playbook that will be run      |
| [requirements.yml](profile/requirements.yml) | configuration for [ansible-galaxy](https://galaxy.ansible.com/docs/using/installing.html#installing-multiple-roles-from-a-file) dependencies |

## Profile Precheck Folder

The profile folder contains a special [__precheck__](profile/__precheck__) folder with configuration used by the provisioner to help end users apply the profile to their machines:

| -- Filename ----------------| -- Description -------------------------------------------------------------- |
|-----------------------------|-------------------------------------------------------------------------------|
| [env.yml](profile/__precheck__/env.yml)      | required environment variables that need to be set prior to installing this profile |
| [notes.txt](profile/__precheck__/notes.txt)  | details about the installation visible to the end user                              |

## Development

[Mac Maker](https://github.com/osx-provisioner/mac_maker) can work with public Github repositories, or with `spec.json` files.

A Mac Maker profile has a specific directory structure. The spec.json file lets you mix and match where the directories and files are. It's a bit inflexible in certain ways, because it requires absolute paths, but this makes it ideal to work off a USB stick or any portable media.

```json
{
  "workspace_root_path": "The absolute path to the root folder of your cloned profile repository.",
  "profile_data_path": "This absolute path usually points to the `profile` folder inside your profile repository.",
  "galaxy_requirements_file": "This absolute path usually points to the `profile_data_path/requirements.yml` file inside your profile repository.",
  "playbook": "This absolute path usually points to the `profile_data_path/install.yml` file inside your profile repository.",
  "roles_path": [
    "This absolute path usually points to the `profile_data_path/roles` folder inside your profile repository.",
    "You can append several roles directories here, they should all be absolute paths."
  ],
  "inventory": "This absolute path usually points to the `profile_data_path/inventory` file inside your repository."
}
```

When developing your profile locally, it's handy to setup a `spec.json` that points to all the locations you need, so you can just re-run Mac Maker to test.
