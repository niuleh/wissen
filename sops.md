# sops

## Installation

``` bash
# Download the binary
curl -LO https://github.com/getsops/sops/releases/download/v3.9.0/sops-v3.9.0.linux.amd64

# Move the binary in to your PATH
mv sops-v3.9.0.linux.amd64 /usr/local/bin/sops

# Make the binary executable
chmod +x /usr/local/bin/sops
```

### Generate gpg key

``` bash
gpg --full-gen-key --expert
```

### Configure gpg to allow passphrase entry on terminal

[source](https://stackoverflow.com/questions/51504367/gpg-agent-forwarding-inappropriate-ioctl-for-device)

``` bash
cat << EOF > ~/.gnupg/gpg.conf
use-agent 
pinentry-mode loopback

EOF

cat << EOF > ~/.gnupg/gpg-agent.conf
allow-loopback-pinentry

EOF

echo RELOADAGENT | gpg-connect-agent
```

### .sops.yaml

Minimum working example:
``` yaml
creation_rules:
  - pgp: 'DC5025D7213BDBDE888031CBADEA685EEFFEBE67'
```

### Configure VSCode as sops editor

``` bash
mkdir .bashrc.d
cat << EOF > .bashrc.d/10-sops-editor
export EDITOR="code --wait"
EOF
```

## aliases

``` bash
# ssh_pp | wl-copy
alias ssh_pp="toolbox run -c vscode sops decrypt --extract '[\"ssh_key_passphrase\"]' ~/Documents/wissen/secrets.yml"
```