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