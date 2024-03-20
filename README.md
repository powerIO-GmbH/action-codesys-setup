# Github action setup CODESYS

> This github action is used to install CODESYS for CI/CD jobs.

## About

This action is designed to install CODESYS for further CI/CD jobs, such as signing libraries, signing packages, etc. 
It can also be used to process test cases or other CI/CD jobs in your workflow.

## Usage

>:white_flag: See the [inputs](#inputs) section for detailed descriptions.

```yml
- name: Setup CODESYS
  uses: powerIO-GmbH/action-codesys-setup@v<version>
  with:
    installer-version: 2.2.2
    auto-update-installer: false
    generation: 3.5.19.0
    architecture: 64
    patch: 6
    hotfix: 0
    build: 0 
```

## Usage examples

- Install CODESYS Version `3.5.17.2`:
```yml
- name: Setup CODESYS
  uses: powerIO-GmbH/action-codesys-setup@v<version>
  with:
    generation: 3.5.17.0
    architecture: 64
    patch: 2
```

## Inputs

The action supports the following inputs:

- `installer-version`

  The version of the installer to use to install the CODESYS installation.

  **required:** *false*  
  **default:**: *`2.2.2`* 

- `generation`

  This is the base generation you want to install. For example `3.5.19.0`.
  Even if you want to install the version `3.5.19.6` you have to define the generation as `3.5.19.0`.  
  The patch version is defined by the `patch` input.  

  **required:** *false*  
  **default:**: *`3.5.19.0`* 

- `architecture`

  The installation architecture of CODESYS. Allowed inputs: `32` and `64`.

  **required:** *false*  
  **default:**: *`64`* 

- `patch`

  The patch of the CODESYS version to install.

  **required:** *false*  
  **default:**: *`0`* 

- `hotfix`

  The hotfix of the CODESYS version to install.

  **required:** *false*  
  **default:**: *`0`* 

- `build`

  The build of the CODESYS version to install.

  **required:** *false*  
  **default:**: *`0`* 

- `installation-directory`

  This can be used to define a custom installation directory.  
  If this input is empty, the installation path is set based on the architecture and installation version.  

  For example - bit `64`, generation `3.5.19.0` and patch `6`:  
  `C:\Program Files\CODESYS 3.5.19.6`

  For example - bit `32`, generation `3.5.17.0` and patch `2`:  
  `C:\Program Files (x86)\CODESYS 3.5.17.2`

  **required:** *false*  
  **default:**: *`''`* 

- `auto-update-installer`

  If set to `true`, the installer will be updated before the installation.

  **required:** *false*  
  **default:**: *`true`* 