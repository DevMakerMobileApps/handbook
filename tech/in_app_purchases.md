# In App Purchases:

**InAppPurchases** possibilita um aplicativo cobrar um usuário por alguma compra sem precisar que o aplicativo faça a gestão de cartões de crédito nem integração com gateways de pagamentos.
As próprias lojas Apple e Google se encarregam de todo processo de cobrança do usuário mas, cobram uma taxa de **30%** do valor vendido.

Um aplicativo **é obrigado** a implementar InAppPurchases para venda de bens digitais (acesso a conteúdo no app, áreas exclusivas de assinantes, ect). Por outro lado, **não é possível** usar InAppPurchases para compras de bens/serviços físicos (comprar produtos reais, pagar profissionas por algum serviço, ect).

As lojas dividem "bens digitais" em 4 tipos:

- **Consumíveis:** são items que acabam depois de consumídos e podem ser comprados diversas vezes. Muito comum em jogos.
- **Não-consumíveis:** são compras únicas sem data de expiração. Ex: pagamento único por acesso vitalício a parte privada da app.
- **Assinaturas auto-renovável:** Usuário assina uma vez e é cobrado periódicamente até cancelar. Ele ganha acesso enquanto a assinatura estiver ativa. Este é o mais comum em acessos à conteúdos. Ex: Acesso a parte privada da app por R$ 9,90/mês.
- **Assinaturas não-renovável:** Compra única, não renovável automaticamente que garante acesso por um determinado tempo. Ex: R$ 29.90 por 3 meses de acesso a parte privada da app.

O fluxo da compra em si, de cobrar do cartão do cliente (periodicamente ou não), é gerenciado pelas lojas **mas**, o aplicativo ainda precisa fazer a gestão dessa compra para liberar o conteúdo ao usuário do aplicativo. Normalmente aplicativos que vendem algo possuem um sistema de Login e o back-end precisa reconhecer e validar a compra e então liberar o acesso ao "bem digital" para o usuário.

#### Pré-Requisitos:
Para se iniciar o desenvolvimento do InAppPurchases é necessário:

- Para pessoas jurídicas: Cliente precisa de empresa constituída, com CNPJ e conta bancária
- Conta nas lojas AppleStore &/ou GooglePlay em nome do cliente;
- Conta-Corrente bancária para depósito do valor das vendas;
- O tipo e o valor dos bens vendidos;
- **Apple:** exige assinar termos de [Paid Applications Agreement](https://help.apple.com/app-store-connect/#/devb6df5ee51) onde se cadastra a conta bancária;
  - a conta bancária **precisa** ser da mesma titularidade da conta apple.
- **Google:** exige uma comprovação da titularidade da conta bancária.
  - Depois de informar a conta bancária, ela irá depositar alguns centavos e será necessário informar o valor depositado.
  - A conta bancária **não** precisa ser do mesmo titular da conta do google;
  - ⚠️ Contas de **bancos digitais** parecem não funcionar (banco Inter não funcionou)


### Tech Stuff:
- Projetos em React Native  precisa ser ejetados do expo pois exigem configurações diretas no XCode e AndroidStudio.
- Mesmo ejetado, o código em React Native não precisa ser duplicado para ios e android. [A mesma classe](https://docs.expo.io/versions/latest/sdk/in-app-purchases/) do Expo trata as 2 lojas com uma mesma interface.
- O fluxo normal de uma compra é:
  1. O mobile faz completamente a compra no mobile;
  1. Quando a compra é confirmada no mobile, um "recibo" da compra é enviado para o back-end;
  1. O back-end confere o recibo com a respectiva loja;
  1. Se o recibo estiver ok, libera o conteúdo para o usuário;
- **Assinaturas auto-renovável:** possuem um fluxo extra:
  1. A primeria compra inicia uma assinatura
  1. A partir desse momento o servidor da loja notifica direto o back-end do aplicativo;
  1. Com essa notificação o back-end precisa entender se a assinatura ainda esta ativa ou foi cancelada.



## Apple:
- https://developer.apple.com/documentation/appstoreservernotifications
- https://developer.apple.com/documentation/storekit/in-app_purchase/testing_in-app_purchases_with_sandbox

### Testando:
- https://help.apple.com/app-store-connect/#/dev7e89e149d

**Para assinaturas auto-renováveis:**
- Usuários de teste em sandbox precisam ser cadastrados na appstoreconnect em Users and Access > Sandbox > Testrs (https://appstoreconnect.apple.com/access/testers)
- Servidor da apple simula 5 eventos de renovação automática e então cancela a assinatura automaticamente
  - **1 week:** 3 minutes
  - **1 month:** 5 minutes
  - **2 months:** 10 minutes
  - **3 months:** 15 minutes
  - **6 months:** 30 minutes
  - **1 year:** 1 hour



best guide:
https://medium.com/better-programming/react-native-in-app-purchase-subscription-bb7ad18ec5a0

--------------------------------


- [Expo Docs](https://docs.expo.io/versions/latest/sdk/in-app-purchases/)
- [Android Docs]()

### Android:
- https://developer.android.com/google/play/billing/integrate
- https://developer.android.com/google/play/billing/subs
- https://developer.android.com/google/play/billing/getting-ready#configure-rtdn

- purchase token é o que liga tudo
- se o usuário fez upgrade/dowgrande, tem o linkedPurchaseToken que é a assinatura velha e vem um novo purchase token

googles statuses:
- Active: User is in good standing and has access to the subscription.
- Cancelled: User has cancelled but still has access until expiration.
- In grace period: User experienced a payment issue, but still has access while Google is retrying the payment method.
- On hold: User experienced a payment issue, and no longer has access while Google is retrying the payment method.
- Paused: User paused their access, and does not have access until they resume.
- Expired: User has cancelled and lost access to the subscription. The user is considered churned at expiration.

## Apple:
- https://developer.apple.com/documentation/storekit/in-app_purchase
- https://developer.apple.com/documentation/storekit/in-app_purchase/subscriptions_and_offers
billing cycles
- https://developer.apple.com/documentation/appstoreservernotifications/responsebody
- https://developer.apple.com/documentation/appstoreservernotifications/notification_type
- https://developer.apple.com/documentation/storekit/in-app_purchase/validating_receipts_with_the_app_store

-----
## SEE:
- https://stackoverflow.com/questions/25828491/android-verify-iap-subscription-server-side-with-ruby
- https://medium.com/wolox/7b208f9cfa3e
- https://github.com/jnbt/candy_check
- https://github.com/nomad/venice


## Notes:
- Não funciona em emuladores! Só rodando nos dispositivos de verdade;
- As apps tanto iOS quanto Android tem que passar por uma submissão nas lojas antes de conseguir testar;
- Pra realizar uma compra de um item, primeiro é obrigatório solicitar pras lojas os detalhes desse item;



Flow:
1. Mobile connects to the store
1. Mobile list the possible purchase items
1. Requests the payment
1. get the confirmation
1. send to the back-end
1. back-end verify the purchase
    - android needs:
        - package_name: "my-package-name",
        - subscription_id: "my-subscription-id",
        - token: "my-token" (purchaseToken do expo?)

1. mobile finish the transaction
1. mobile disconnects from the store

1. Android store pings that the subscription status has changed
    1. than we neede to query the api to sync the data


suportar:
- Trial?
- providers diferentes e um fake
- como agendar um check?

=================== Structure:

Model: SubscriptionPlan:
- provider (enum: 'applestore' / 'playstore' / 'fake')
- provider_id
- value
- cycle_days

Model: Subscription
+ add o plan
- tirar o value, subscription_type, o start_at e o expiration_at
- criar uma coluna booleana: `active`


Model: SubscriptionSyncLog (save every time there was a sync)
- requested_at:timestamp
- provider_data:jsonb



Actions:
- Subscription::Start (valida com o provider e inicia)
- Subscription::Sync! (re-sincroniza com o provider e ve se o status mudou)
- Subscription::Google::AknoledgePurchase!
    - back precisa
