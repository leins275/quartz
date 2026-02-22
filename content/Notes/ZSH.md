---
title: ZSH
date: 2026-02-22
draft: false
tags: []
aliases:
---
# Install ubuntu
## Install all software and plugins
```bash
sudo apt update -y && sudo apt install zsh -y
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```
## Update config
Open `~/.zshrc` and modify this line by adding installed plugins
```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

# Server theme
```
ZSH_THEME="lukerandall"
```
# Enable zsh

```bash
chsh -s $(which zsh)
```

---
- https://hackernoon.com/customize-oh-my-zsh-with-syntax-highlighting-and-auto-suggestions-6q1b3w8o