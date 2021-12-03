# Setup de desenvolvimento no OSX

A ideia desse documento é ser um guia para facilitar a configuração de um mac novo. Por enquanto ele está mais focado em comandos no processo de instação, então fique livre para melhorar esse documento.

⚠️**Se alguma comando quebrar, ajude atualizando o guia**⚠️

## Setup basico
- [1 homebrew](#1-homebrew)
- [2 cli apps](#2-cli-apps)
- [3 rvm](#3-rvm)
- [4 nvm](#4-nvm)
- [5 Xcode](#5-Xcode)
- [6 Setup git](#6-Setup-git)

## Firulas opcionais
- [Desktop apps](#desktop-apps)
- [Setup git-delta diffs](#setup-git-delta-diffs)
- [Setup iTerm2](#Setup-iTerm2)
  - [Install OhMyZsh](#install-oh-my-zsh)
  - [Install powerlevel10k](#install-powerlevel10k)
  - [Setup fzf](#setup-fzf)
  - [Setup Z](#setup-z)
  - [Add OhMyTmux](#add-oh-my-tmux)
  - [Add command to auto start tmux on iterm2](#add-command-to-auto-start-tmux-on-iterm2)

## 1 homebrew
```shell
xcode-select --install
```
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```shell
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/luciocharallo/.zprofile
```
```shell
eval "$(/opt/homebrew/bin/brew shellenv)"
```

## 2 cli apps
```shell
brew install gpg htop tmux z imagemagick redis fzf zsh zsh-syntax-highlighting postgis postgresql pinentry-mac
```

### 2.1 setup heroku
```shell
brew tap heroku/brew && brew install heroku
```
```shell
heroku autocomplete --refresh-cache
```
```shell
echo "$(heroku autocomplete:script zsh)" >> ~/.zshrc
```
```shell
source ~/.zshrc
```

### 2.2 setup postgresql
brew services start postgresql
initdb /opt/homebrew/var/postgres
echo 'alias pg="pg_ctl -D /opt/homebrew/var/postgres"' >> ~/.zshrc
```shell
source ~/.zshrc
```
```shell
pg start
```
```shell
createdb init_test
```
```shell
createuser -s postgres
```
```shell
createuser --interactive --pwprompt
```
```shell
pg stop
```

### 2.3 setup redis
```shell
brew services start redis
```
```shell
redis-server
```

## 3 rvm
```shell
gpg --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```
```shell
\curl -sSL https://get.rvm.io | bash -s stable --rails
```
```shell
source /Users/lucio/.rvm/scripts/rvm
```
```shell
source ~/.zshrc
```

### 3.1 definir gems default
```shell
echo 'bundler\nbyebug\nrails\nrspec\nrspec-rails\nrubocop\nrubocop-rspec\nsimplecov\nsolargraph' >>  ~/.default-gems
```

### 3.2 Instalar versões do ruby
```shell
rvm install 3.0.3
```
```shell
rvm list
```
```shell
rvm current
```

## 4 nvm
Tem que verificar a verão
```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```

Adicionar script abaixo no FINAL do profile file (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc)
```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

### 4.1 Define packagens default
```shell
echo 'yarn\nreact-native\nexpo-cli' >>  $NVM_DIR/default-packages
```

### 4.2 Instalar versões do nodejs
```shell
nvm install 16
```
```shell
nvm alias default 16
```

## 5 Xcode
Instalar via App Store - https://apps.apple.com/br/app/xcode/id497799835?l=en&mt=12

## 6 Setup git
```shell
git config --global user.name "<Your-Full-Name>"
```
```shell
git config --global user.email "<your-email-address>"
```

### 6.1 Git gpg keys
```shell
brew link --overwrite gnupg
```
```shell
echo "pinentry-program /opt/homebrew/bin/pinentry-mac" >> ~/.gnupg/gpg-agent.conf 
```
```shell
killall gpg-agent
```
```shell
gpg --full-generate-key
```
```shell
gpg --list-secret-keys --keyid-format=long
```
Da lista de chaves GPG, copie a forma longa do ID da chave GPG que você gostaria de usar. Neste exemplo, o ID da chave GPG é 3AA5C34371567BD2:
```shell
$ gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/FFFFFFFFFFFFFFFF 2016-03-10 [expires: 2017-03-10]
uid                          Hubot 
ssb   4096R/FFFFFFFFFFFFFFFF 2016-03-10
```
```shell
git config --global user.signingkey FFFFFFFFFFFFFFFF
```
```shell
git config --global gpg.program gpg
```
```shell
git config --global commit.gpgsign true
```
```shell
gpg --armor --export FFFFFFFFFFFFFFFF | pbcopy
```
Colar chave no [Github](https://github.com/settings/keys) e no [Gitlab](https://gitlab.com/-/profile/gpg_keys)


### 6.2 Git rsa keys
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
touch ~/.ssh/config
```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```
ssh-add -K ~/.ssh/id_ed25519
tr -d '\n' < ~/.ssh/id_ed25519.pub | pbcopy

-- access
https://github.com/settings/keys
https://gitlab.com/-/profile/keys


# Firulas

## Desktop apps
```shell
brew install --cask altair-graphql-client android-studio brave-browser dbeaver-community discord firefox google-chrome iterm2 visual-studio-code
```

## Setup git-delta diffs
```shell
brew install git-delta 
```

Adicionar em  ~/.gitconfig
```
[color]
	ui = true
[pager]
	diff = delta
	log = delta
	reflog = delta
	show = delta
[interactive]
	diffFilter = delta --color-only --features=interactive
[delta]
	features = side-by-side line-numbers decorations
	syntax-theme = Dracula
	plus-style = syntax "#003800"
	minus-style = syntax "#3f0001"

[delta "decorations"]
	commit-decoration-style = bold yellow box ul
	file-style = bold yellow ul
	file-decoration-style = none
	hunk-header-decoration-style = cyan box ul

[delta "line-numbers"]
	line-numbers-left-style = cyan
	line-numbers-right-style = cyan
	line-numbers-minus-style = 124
	line-numbers-plus-style = 28
```

## Setup iTerm2
### Install OhMyZsh
```shell
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```

### Install powerlevel10k
```shell
brew install romkatv/powerlevel10k/powerlevel10k
```
```shell
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
```

### Setup fzf
```shell
$(brew --prefix)/opt/fzf/install
```

### Setup Z
```shell
echo '. $(brew --prefix)/etc/profile.d/z.sh' >> ~/.zshrc
```

### Add OhMyTmux
```shell
cd ~/
```
```shell
git clone https://github.com/gpakosz/.tmux.git
```
```shell
ln -s -f .tmux/.tmux.conf
```
```shell
cp .tmux/.tmux.conf.local .
```

### Add command to auto start tmux on iterm2
```shell
tmux ls && read tmux_session && tmux attach -t ${tmux_session:-default} || tmux new -s ${tmux_session:-default}
```
