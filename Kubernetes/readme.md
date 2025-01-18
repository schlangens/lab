
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

``sudo pacman -Syu k9s``

- Also install tmux and vim if not installed

- Uploaded all .dot files (.vimrc .bashrc .tmux.conf)


