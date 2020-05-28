# Instalação de uma maquina macOS:
## Base:
1. Ter certeza que todas as atualizações do sistema estão instaladas
1. Instalar o xcode dev tools `Xcode-select —install`
1. Instalar o brew: https://docs.brew.sh/Installation

## Ruby:
1. Instalar o rbenv: https://github.com/rbenv/rbenv#installation
  1. depois de instalado rodar `rbenv init` e atualizar o bash_profile
  1. `rbenv install -l` para ver as versões disponívels
  1. `rbenv install X.X.X` para instalar uma versnao
  1. `rbenv global X.X.X` para setar esta versão instalada como padrão

## Postgres:
1. `brew install postgresql`
    ```
    To have launchd start postgresql now and restart at login:
      brew services start postgresql
    Or, if you don't want/need a background service you can just run:
      pg_ctl -D /usr/local/var/postgres start
    ```
- Sugestão: setar um alias e inicar manualmente quando quer:
  - `alias pg="pg_ctl -D /usr/local/var/postgres"` no `~/.bash_profile`
  - e quando iniciar/parar o serviço: `pg start` / `pg stop`


## NodeJS:
1. Instalar o nvm: https://github.com/nvm-sh/nvm
  1. `nvm ls-remote` para ver as versões disponívels
  1. `nvm install X.X.X` para instalar uma versão
  1. `nvm alias default X.X.X` para setar ela como a default


# Sugestões:
1. Alfred https://www.alfredapp.com
1. Spectaleapp https://www.spectacleapp.com
1. iterm2: https://www.iterm2.com
1. bash_it https://github.com/Bash-it/bash-it


