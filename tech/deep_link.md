# Deep Link

## Deep Link normal:
- regista um schema único da nossa app no sistema operacional
  - ex: `http:` ou `https:` = abrir o navegador
  - ex: `mailto:` = abrir o cliente de email
  - ex: `tel:` = abrir o app de ligação
- esse schema abre sempre a app se estiver instalada!
  - ex: `dvmrapp:` = abre a app da DevMaker
- ⚠️ só abre se a app já estiver instalada. Senão o link não é reconhecido pelo sistema operacional;


## Universal Deep Link:
- é universal pq usa o schema `http` para abrir tanto uma página web quanto a app na web
- ex: `https://www.devmaker.com.br/news/2`
  - se o usuário tem a app instalada, abre a notícia 2 no app
  - se não tiver a app instalada, abre a notícia no navegador
- Apple e Goole exige que vc confirme ser o proprietário da app DevMaker e do domínio `devmaker.com.br`
- ⚠️ não direciona o usuário pra baixar a app se ela não estiver instalada

## Deferred Deep Link:
- é deferred pq o usuário pode não ter a app instalada, baixar e instalar a app e só então abrir no link específico
- ⚠️ precisa de uma grande solução no back-end e integração do back com as lojas
- ⚠️ Expo só suporte esse tipo de link usando um serviço externo: [Branch.io](https://docs.expo.io/versions/latest/sdk/branch/)


Links:
- https://docs.expo.io/workflow/linking/
- https://docs.expo.io/versions/latest/sdk/branch/
- https://github.com/react-navigation/react-navigation/issues/5409

