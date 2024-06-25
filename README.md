# Zen Linux &nbsp; [![build-ublue](https://github.com/blue-build/template/actions/workflows/build.yml/badge.svg)](https://github.com/blue-build/template/actions/workflows/build.yml)

See the [BlueBuild docs](https://blue-build.org/how-to/setup/). 

## Installation

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  sudo rpm-ostree rebase ostree-unverified-registry:ghcr.io/mecattaf/zen:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/mecattaf/zen:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```
### Manual Steps

- Copy over git credentials
- Authenticate to google chrome
- Authenticate to tailscale with `tailscale login`

### Google Chrome

1) In `chrome://settings`:

| System                                                | Value  |
|-------------------------------------------------------|--------|
| Continue running background apps when Google Chrome is closed | ❌ |
| Use hardware acceleration when available              | ✅      |

| Appearance                                            | Value  |
|-------------------------------------------------------|--------|
| Theme                                                 | All Black - Full Dark Theme/Black Theme |
| Mode                                                  | Dark   |
| Show home button                                      | ❌      |
| Show bookmarks bar                                    | ❌      |
| Show images on tab hover preview cards                | ✅      |
| Use system title bars and borders                     | ✅      |

| System                                                | Value  |
|-------------------------------------------------------|--------|
| Continue running background apps when Google Chrome is closed    | ❌ |
| Use graphics acceleration when available                         | ✅ |

2) In`chrome://flags`:

| Flag                                                  | Status |
|-------------------------------------------------------|--------|
| Preferred Ozone Platform                              | Wayland |
| Chrome Refresh 2023                                   | ✅      |
| Realbox Chrome Refresh 2023                           | ✅      |
| Chrome WebUI Refresh 2023                             | ✅      |
| Chrome Refresh 2023 New Tab Button                    | ✅      |
| Enable Display Compositor to use a new gpu thread     | ✅      |
| WebRTC PipeWire support                               | ✅      |
| Native Client                                         | ✅      |
| WebGL Developer Extensions                            | ✅      |
| WebGL Draft Extensions                                | ✅      |
| Toggle hardware accelerated H.264 video encoding for Cast Streaming | ✅ |
| Toggle hardware accelerated VP8 video encoding for Cast Streaming  | ✅ |


### Troubleshooting flatpaks

If a flatpak is broken, revert versions using:
```
flatpak list
flatpak remote-info --log flathub com.google.Chrome
flatpak update --commit=<commit-of-working-version> com.google.Chrome
```

### Rolling back to previous versions

View the list of available builds by entering:
```
skopeo list-tags docker://ghcr.io/ublue-os/bazzite | grep -- "-stable-" | sort -rV
```

Rebasing to a specific build requires users to open a host terminal and enter:
```
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/IMAGE-NAME:VERSION-YEARMONTHDAY
```

Example:
```
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-deck:39-20240113
```
For the Jan. 13th 2024 bazzite-deck (Fedora 39) build.

### To revert back to Silverblue

```shell
sudo rpm-ostree rebase fedora:fedora/40/x86_64/silverblue
```


## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso). 
