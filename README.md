# 📦 ThingsBoard OTA Uploader

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Install-blue?logo=github&style=flat-square)](https://github.com/marketplace/actions/publish-ota-to-thingsboard)
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg?style=flat-square)](LICENSE)

A GitHub Action to create and upload OTA (Over-the-Air) firmware packages to [ThingsBoard](https://thingsboard.io/) via its REST API.

## ✨ Features

- Authenticates with ThingsBoard using username and password
- Creates a new OTA package for a specified Device Profile
- Uploads the provided binary file to the created OTA package

## 📥 Inputs

| Name                | Description                                | Required |
| ------------------- | ------------------------------------------ | -------- |
| `title`             | Title of the OTA package                   | ✅ Yes   |
| `version`           | Firmware version to assign                 | ✅ Yes   |
| `file`              | Path to the firmware binary file           | ✅ Yes   |
| `tb_url`            | Base URL of your ThingsBoard instance      | ✅ Yes   |
| `device_profile_id` | ID of the Device Profile to attach the OTA | ✅ Yes   |
| `tb_username`       | ThingsBoard username for authentication    | ✅ Yes   |
| `tb_password`       | ThingsBoard password for authentication    | ✅ Yes   |

## 🔐 Secrets

It’s <b>HIGHLY</b> recommended to store `tb_username`, `tb_url` and `tb_password` as encrypted secrets in your GitHub repository.
To learn how, read this [doc page](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions).

## 🚀 Usage Example

```yaml
name: Upload OTA Firmware

on:
  workflow_dispatch:

jobs:
  upload-ota:
    runs-on: ubuntu-latest
    steps:
      - name: Publish OTA to ThingsBoard
        uses: LarsFL/upload-thingsboard-ota-firmware@v1
        with:
          title: "${{ github.ref_name }}"
          version: "${{ github.ref_name }}"
          file: build/esp_bridge.bin
          tb_url: ${{ secrets.TB_URL }}
          device_profile_id: ${{ secrets.TB_DEVICE_PROFILE_ID }}
          tb_username: ${{ secrets.TB_USERNAME }}
          tb_password: ${{ secrets.TB_PASSWORD }}
```
