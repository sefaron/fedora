# Fedora setup steps

Things to do for setting up fedora

# Table of contents

- [Update Fedora](#update-fedora)
- [Install Nvidia Drivers](#install-nvidia-drivers)
- [Install ms-fonts](#install-ms-fonts)
- [Install Brave](#install-brave)
- [Install Chrome](#install-chrome)
- [Install Vscode](#install-vscode)
- [Install fonts](#install-fonts)
- [Install Additional Software](#install-additional-software)
- [Setup Github Profile](#github-profile)
- [Disable CAPSLOCK](#capslock)
- [Modifying GRUB](#modifying-grub)

## Update Fedora

```
sudo dnf update -y
```

# Install Nvidia Drivers

```
sudo dnf install kmodtool akmods mokutil openssl
```

```
sudo kmodgenca -a
```

```
sudo mokutil --import /etc/pki/akmods/certs/public_key.der
```

- set password: ( its password for mokutil that you need to re-enter during boot up)

```
sudo dnf install akmod-nvidia
```

# Install ms-fonts

```
cd ~/Downloads/
```

```
git clone https://github.com/sefaron/ms-fonts.git
```

```
mkdir /usr/local/share/fonts
```

```
mv ms-fonts /usr/local/share/fonts
```

```
fc-cache --force
```

# Install Brave

```
curl -fsS https://dl.brave.com/install.sh | sh
```

```
sudo mkdir -p /etc/brave/policies/managed/
```

```
sudo bash -c 'printf "{
  \\\"RestoreOnStartup\\\": 1,
  \\\"PasswordManagerEnabled\\\": false,
  \\\"PaymentMethodQueryEnabled\\\": false,
  \\\"AutofillCreditCardEnabled\\\": false,
  \\\"AutofillAddressEnabled\\\": false,
  \\\"ShowHomeButton\\\": true,
  \\\"BraveRewardsDisabled\\\": true,
  \\\"BraveWalletDisabled\\\": true,
  \\\"BraveVPNDisabled\\\": 1,
  \\\"BraveAIChatEnabled\\\": false,
  \\\"TorDisabled\\\": true,
  \\\"DnsOverHttpsMode\\\": \\\"automatic\\\"
}" > /etc/brave/policies/managed/GroupPolicy.json'
```

# Install Chrome

```
sudo dnf install google-chrome-stable
```

# Install Vscode

```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\nautorefresh=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null
```

```
dnf check-update
sudo dnf install code # or code-insiders
```

# Install fonts

```
sudo dnf install jetbrains-mono-fonts open-sans-fonts
```

# Install Additional Software

```
sudo dnf install gnome-tweaks nodejs libavcodec-freeworld
```

# Github Profile

```
git config --global user.name "ef"
git config --global user.email "33119700+sefaron@users.noreply.github.com"
```

# CAPSLOCK

Disable Capslock

```
gsettings set org.gnome.desktop.input-sources xkb-options "['caps:none']"
```

Enable Capslock

```
gsettings reset org.gnome.desktop.input-sources xkb-options
```

# Modifying GRUB

open config in nano :

```
sudo nano /etc/default/grub
```

apply config :

```
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

My usual grub config :

```
GRUB_TIMEOUT=8
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="rhgb quiet rd.driver.blacklist=nouveau,nova_core modprobe.blacklist=nouveau,nova_core"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```
