# Publicando APPs em React Native com Expo:

Siga [este guia do expo](https://docs.expo.io/distribution/app-stores/)

`expo build:ios --release-channel=production`
`expo build:android --release-channel=production`

#### Lembre-se:
- app bundleIdentifior nnao pode ter `_` nem `-` nem nenhum caracter especial
- checkar a versão do SDK do expo, preferencialmente a mais atual
- https://docs.expo.io/versions/latest/distribution/building-standalone-apps/
- **usar o release channel de production**
- privacy: "unlisted"
- aumentar ios.buildNumber e android.versionCode sempre que for fazer uma build
- para android: rode `fetch:android:keystore` e salve as chaver e o arquivo `.jks` no redmine do projeto
- [Configure o FCM ServerKey para envio de push notifications](https://docs.expo.io/guides/using-fcm/#uploading-server-credentials) 

## Para Produção?
- mudar pra url de produção!
- Lembre de usar o **release channel** `production`! -> `expo build:[ios/android] --release-channel=production`

