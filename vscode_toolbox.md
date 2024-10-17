# VSCode + toolbox

## Install using official repo

``` bash
# Import microsoft gpg key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add vscode repo to yum.repos
echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null

# Refresh packages & Install code
sudo dnf check-update
sudo dnf install code
```

## Make host's podman accessible from inside toolbox

``` bash
toolbox enter vscode
echo -e '#!/bin/sh\nexec /usr/bin/flatpak-spawn --host podman "$@"' | sudo tee /usr/local/bin/podman 1>/dev/null && sudo chmod +x /usr/local/bin/podman
```

## Enable podman socket for devcontainer extension

``` bash
systemctl enable --now --user podman.socket
```

## Podman config for docker compatibility

Instructs builder to interprete some Containerfile instructions as docker would.

``` bash
cat <<EOF ~/.config/containers/containers.conf
[containers]
env = [
  "BUILDAH_FORMAT=docker"
]
label = false
userns = "keep-id"
EOF
```
<!-- TODO: Add enabling toolboxed vscode to access hosts podman -->
<!-- TODO: Add changing devcontainers docker executable to toolbox podman shim -->