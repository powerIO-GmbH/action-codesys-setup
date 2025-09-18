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
      installer-version: 2.4.1
      auto-update-installer: false
      generation: 3.5.21.0
      architecture: 64
      patch: 2
```

## Usage examples

- Install CODESYS Version `3.5.20.4`:
```yml
  - name: Setup CODESYS
    uses: powerIO-GmbH/action-codesys-setup@v1
    with:
      generation: 3.5.20.0
      architecture: 64
      patch: 4
```

- Install CODESYS Version `3.5.20.0` with following packages.
  * _CODESYS Git_ Version 1.4.0.0
  * _CODESYS Library Documentation Support_ Version 4.5.0.0
  * Custom package file, in this case _NetBaseServices Example_ 

```yml
    - name: Setup CODESYS
      id: setup_codesys
      uses: powerIO-GmbH/action-codesys-setup@v1
      with:
        installer-version: 2.4.1
        auto-update-installer: true
        generation: 3.5.20.0
        architecture: 64
        install-add-ons: true
        add-ons-list: |
          dd6c2da4-2ed2-4076-9bf7-52394db68819,1.4.0.0
          fb6f3506-d165-4e75-a1b9-98895d542cc8,4.5.0.0
        add-ons-from-file-list: |
          example/custom_packages/NetBaseServices_Example_1.0.0.0.package
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|----------|
| `installer-version` | The version of the installer to use to install the CODESYS installation. | false | `2.4.1` |
| `generation` | This is the base generation you want to install (e.g., `3.5.21.0`). Even if you want to install version `3.5.21.2`, you have to define the generation as `3.5.21.0`. The patch version is defined by the `patch` input. | false | `3.5.21.0` |
| `architecture` | The installation architecture of CODESYS. Allowed inputs: `32` and `64`. | false | `64` |
| `patch` | The patch of the CODESYS version to install. | false | `0` |
| `hotfix` | The hotfix of the CODESYS version to install. | false | `0` |
| `build` | The build of the CODESYS version to install. | false | `0` |
| `installation-directory` | Custom installation directory. If empty, the path is set based on architecture and installation version. Examples:<br>- 64-bit, generation 3.5.19.0, patch 6: `C:\Program Files\CODESYS 3.5.19.6`<br>- 32-bit, generation 3.5.17.0, patch 2: `C:\Program Files (x86)\CODESYS 3.5.17.2` | false | `''` |
| `auto-update-installer` | If set to `true`, the installer will be updated before the installation. | false | `true` |
| `install-add-ons` | If set to `true`, the installer will install the CODESYS AddOns. | false | `false` |
| `add-ons-list` | List of addons to install, given by ID and version. Example:<br>`dd6c2da4-2ed2-4076-9bf7-52394db68819,1.4.0.0`<br>For multiple addons, create a new line for each addon. | false | `''` |
| `add-ons-from-file-list` | List of addons to install, given by the path to the `<name>.package` file. | false | `''` |


## Outputs

| Output                        | Description                                       |
| ----------------------------- | ------------------------------------------------- |
| `codesys-path`                | The path of the installed CODESYS version.        |
| `codesys-executable`          | The path of the CODESYS executable.               |
| `installer-path`              | The path of the installed CODESYS installer.      |
| `installer-cli-executable`    | The path of the CODESYS installer CLI executable. |
| `installation-info-file-path` | The path of the installation information file.    |
