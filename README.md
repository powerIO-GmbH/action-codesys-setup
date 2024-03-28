# Github action setup CODESYS

> This github action is used to install CODESYS for CI/CD jobs.

## About

This action is designed to install CODESYS for further CI/CD jobs, such as signing libraries, signing packages, etc. 
It can also be used to process test cases or other CI/CD jobs in your workflow.

> [!IMPORTANT]  
> This action is only supported to run on windows OS.

## Usage

>:white_flag: See the [inputs](#inputs) section for detailed descriptions.

```yml
  - name: Setup CODESYS
    uses: powerIO-GmbH/action-codesys-setup@v1
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
    uses: powerIO-GmbH/action-codesys-setup@v1
    with:
      generation: 3.5.17.0
      architecture: 64
      patch: 2
```

- Install CODESYS Version `3.5.20.0` with following packages.
  * _CODESYS Git_ Version 1.4.0.0
  * _CODESYS Library Documentation Support_ Version 4.5.0.0
  * Custom package file, in this case _HVAC Building & Automation_ 

```yml
    - name: Setup CODESYS
      id: setup_codesys
      uses: powerIO-GmbH/action-codesys-setup@v1
      with:
        installer-version: 2.2.2
        auto-update-installer: true
        generation: 3.5.20.0
        architecture: 64
        install-add-ons: true
        add-ons-list: |
          dd6c2da4-2ed2-4076-9bf7-52394db68819,1.4.0.0
          fb6f3506-d165-4e75-a1b9-98895d542cc8,4.5.0.0
        add-ons-from-file-list: |
          example/HVAC_Building_Process_Automation_SL_3.0.0.0.package
```

## Inputs

The action supports the following inputs:

- `installer-version`

  The version of the installer to use to install the CODESYS installation.

  **required:** *false*  
  **default:** *`2.2.2`* 

- `generation`

  This is the base generation you want to install. For example `3.5.19.0`.
  Even if you want to install the version `3.5.19.6` you have to define the generation as `3.5.19.0`.  
  The patch version is defined by the `patch` input.  

  **required:** *false*  
  **default:** *`3.5.19.0`* 

- `architecture`

  The installation architecture of CODESYS. Allowed inputs: `32` and `64`.

  **required:** *false*  
  **default:** *`64`* 

- `patch`

  The patch of the CODESYS version to install.

  **required:** *false*  
  **default:** *`0`* 

- `hotfix`

  The hotfix of the CODESYS version to install.

  **required:** *false*  
  **default:** *`0`* 

- `build`

  The build of the CODESYS version to install.

  **required:** *false*  
  **default:** *`0`* 

- `installation-directory`

  This can be used to define a custom installation directory.  
  If this input is empty, the installation path is set based on the architecture and installation version.  

  For example - bit `64`, generation `3.5.19.0` and patch `6`:  
  `C:\Program Files\CODESYS 3.5.19.6`

  For example - bit `32`, generation `3.5.17.0` and patch `2`:  
  `C:\Program Files (x86)\CODESYS 3.5.17.2`

  **required:** *false*  
  **default:** *`''`* 

- `auto-update-installer`

  If set to `true`, the installer will be updated before the installation.

  **required:** *false*  
  **default:** *`true`* 

- `install-add-ons`

  If set to `true`, the installer will install the CODESYS AddOns.

  **required:** *false*  
  **default:** *`false`* 

- `add-ons-list`

  A list of addons to install.
  Given by the id and the version of the addon.
  For example - Install Git: `dd6c2da4-2ed2-4076-9bf7-52394db68819,1.4.0.0`  

  If you want to install multiple addons, create a new line for each addon.  
  For example - Install Git and Library dev package:  
  ```
  dd6c2da4-2ed2-4076-9bf7-52394db68819,1.4.0.0
  fb6f3506-d165-4e75-a1b9-98895d542cc8,4.5.0.0
  ``` 

  **required:** *false*  
  **default:** *`''`* 

- `add-ons-from-file-list`

  A list of addons to install.
  Given by the path to the `<name>.package` file

  **required:** *false*  
  **default:** *`''`* 

## Outputs

| Output                        | Description                                       |
| ----------------------------- | ------------------------------------------------- |
| `codesys-path`                | The path of the installed CODESYS version.        |
| `codesys-executable`          | The path of the CODESYS executable.               |
| `installer-path`              | The path of the installed CODESYS installer.      |
| `installer-cli-executable`    | The path of the CODESYS installer CLI executable. |
| `installation-info-file-path` | The path of the installation information file.    |
