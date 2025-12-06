---
title: "Install"
menu:
  main:
    weight: 20
---

Mise is currently in early development but its core functionality is available. Version 0.1.4 is currently available for Windows, macOS, and Linux. Installation instructions for each OS is enumerated below.

{{< tabs "uniqueid" >}}
{{< tab "macOS" >}}

Download the `.dmg` file from the [Releases](https://github.com/TimothyElder/mise/releases) page on GitHub. Open the downloaded volume and drag `Mise.app` to your applications directory.

When you first run Mise you will be prompted with a warning "The app has not been reviewed" and only given the option to delete the app. To use Mise you will have to navigate to System Settings > Privacy and Security > scroll down to the Security section and there will be an "Open Anyway".

See [this page](https://support.apple.com/guide/mac-help/open-a-mac-app-from-an-unknown-developer-mh40616/mac) from Apple for more information.


{{< /tab >}}

{{< tab "Windows" >}}

Download the `.exe` file from the [Releases](https://github.com/TimothyElder/mise/releases) page on GitHub. Double-click on the downloaded `.exe` file and the installer will run.

{{< /tab >}}

{{< tab "Linux (Debian/Ubuntu)" >}}

Download the `.deb` file from the [Releases](https://github.com/TimothyElder/mise/releases) page on GitHub. In the directory where you downloaded the file run:

```sh
sudo dpkg -i mise_0.1.4_amd64.deb
```

{{< /tab >}}

{{< tab "Source" >}}

Mise can be installed from source on macOS and Linux via the command line:

```sh
git clone https://github.com/TimothyElder/mise.git
cd mise
# make build-macos OR make build-deb
```
The `Mise.app` will appear in the `dist` directory in the source code repo and can be run from that location.

{{< /tab >}}

{{< /tabs >}}