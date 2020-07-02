# Gerar assinatura SHA256 dos fontes de um projeto

Clientes que desejam registar patente dos fontes do projeto podem solicitar um hash de assinatura dos fontes do sistema. Pra fazer isso:

1. Baixe a pasta todos os projetos relacionados (backend, ios, android, react native)
1. Faça um zip com todas as pastas
1. Faça o hash SHA256 do zip com o comando: `openssl dgst -sha256 <zip file>`