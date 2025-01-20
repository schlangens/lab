
## Kubernetes

Description: This is a Kubernetes Lab built with Rancher Desktop in Arch Linux

### Rancher Desktop

``yay -Syu rancher-desktop``

- Other Dependencies installed on Host

Homebrew

```
test -d ~/.linuxbrew && eval "$(~/.linuxbrew/bin/brew shellenv)"
test -d /home/linuxbrew/.linuxbrew && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bashrc
```

``brew install gcc``

### Specific to my prompt and .bashrc file
- ``sudo pacman -Syu k9s``
- ``sudo pacman -S go``
- ``go install github.com/justjanne/powerline-go@latest``


- Also install tmux and vim if not installed

- Uploaded all .dot files (.vimrc .bashrc .tmux.conf) (Repo)[https://github.com/schlangens/dotfiles]


