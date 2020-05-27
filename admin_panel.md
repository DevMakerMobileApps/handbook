# Painel Administrativo
Segue a padronização que deve ser usado no modelo de desenvolvimento do CMS para painéis administrativos usado no backend das aplicações.


![](assets/admin_panel/WB0C668T3%207.png)

**Template utilizado:** [Appwork](https://devmaker-rails-admin-template.herokuapp.com)


## Sumário

1. [Orientações Gerais](#orientações-gerais)
	1. [Página de Login](#página-de-login)
	2. [Página de Dashboard](#página-de-dashboard)
	3. [Navegação](#navegação)
	4. [Página Minha Conta](#página-minha-conta)
2. [Telas com Formulário](#telas-com-formulário)
	1. [Padronização na Apresentação dos Campos](#padronização-na-apresentação-dos-campos)
		1. [Campo Select2](#campo-select2)
		2. [Placeholder de Data](#placeholder-de-data)
		3. [Campo de Status Ativo/Inativo](#campo-de-status-ativoinativo)
	2. [Botões](botões)
		1. [Botão de Adicionar](#botão-de-adicionar)
		2. [Botões de Ação](#botões-de-ação)
		3. [Botão de Deletar](#botão-de-deletar)
		4. [Botões de Salvar e Voltar](#botões-de-salvar-e-voltar)
	3. [Alinhamento dos Campos](#alinhamento-dos-campos)
	4. [Validações](#validações)

3. [Telas com Listagem/Tabelas](#telas-com-listagem-tabelas)
	1. [Área de Filtro](#área-de-filtro)
	2. [Coluna Principal](#coluna-principal)


## Orientações Gerais [Voltar para o Sumário](#sumário)

- [ ] Colocar o asterisco em todos os campos obrigatórios 
- [ ] Traduzir todos os campos 
- [ ] Manter o mesmo estilo de fonte, tabela, e outros elementos da UI para todos os CRUDs no painel.


### Página de Login

Campos obrigatórios:
- [ ] E-mail 
- [ ] Senha
- [ ] Link de recuperação 


### Página de Dashboard

- [ ] Definir os itens a serem utilizados, senão deixar página em branco


### Navegação

- [ ] Orientar o fluxo que o usuário levou para chegar na tela atual. O caminho pode ser representado no próprio título da página `h1`.
- [ ] Quando for tela de edição ou detalhe considerar o padrão:
**[Entidade] / [Entidade] # [ID]**

**Exemplo**

Menu lateral:

![](assets/admin_panel/171E99B6-7732-4B9C-876B-1650D452ACE7%207.png)

Como deve ficar o título da página:

![](assets/admin_panel/BBA30B90-A1DD-4A58-B345-646C09011FB2%207.png)


### Página Minha Conta
Quando houver menu Minha Conta na barra superior, redirecionar para uma tela permitindo a edição dos dados do administrador.

**Exemplo**

![](assets/admin_panel/8F56C222-2589-4EF9-8283-37BA8CD1485F%207.png)


## Telas com Formulário

![](assets/admin_panel/85B3890C-5AE1-472A-A9C1-7744BABF710B%207.png)


### Padronização na apresentação dos campos

#### Campo Select2

- [ ] Quando possuir campo de seleção `Select2`, estilizar o componente para que fique com a mesma aparência do campo de texto normal, com relação a cor de borda, cor de fundo e altura do campo.

**Exemplo**

![](assets/admin_panel/Screen%20Shot%202020-05-27%20at%2011.10.15%207.png)


#### Placeholder de Data

- [ ] Quando houver campo de data, número de telefone, CPF ou CNPJ, deve-se orientar a formatação esperada no `placeholder` do campo. 

> **Placeholder de data:** “Ex: dd/ mm/ aaaa”  

**Exemplo** 

![](assets/admin_panel/Screen%20Shot%202020-05-27%20at%2011.12.33%207.png)


#### Campo de Status Ativo/Inativo

- [ ] O campo de status ativo/inativo deve ser o último a aparecer no formulário.
- [ ] Todos os campos devem possuir label, até mesmo o campo de status ativo/inativo. 

> **Label do campo:** “Status” ou “Status da [Entidade]“  

**Exemplo**

![](assets/admin_panel/E50DD69A-3300-45F3-9758-CB81600560F8%207.png)


### Botões

- [ ] Os botões devem ser na cor primária do cliente.
- [ ] Aplicar cor sólida ao botão somente quando for ação principal e importante para a tela. Os outros botões devem ser no estilo _outline_.


#### Botão de Adicionar
- [ ] O botão deve ficar logo abaixo ao título, alinhado a esquerda da tela.


#### Botões de Ação
Orientação para uso dos botões de ação nas telas de editar e detalhe.

- [ ] Os botões de ação devem ficar logo abaixo ao título, alinhados a esquerda.
- [ ] Os botões de ação devem possuir texto e ícone representando interação.

**Exemplo**

![](assets/admin_panel/0AE9DA12-1E0C-4733-BE07-BE98956104B4%206.png)


#### Botão de Deletar 
No exemplo de botões de ação (acima) está ilustrado como deve ficar o botão de deletar também. A orientação se aplica para uso dos botões de deletar nas telas de editar e detalhe.

- [ ] Caso haja necessidade da ação de deletar na tela o botão deve ficar logo abaixo do título. 
- [ ] O botão deve ser no estilo _outline_, possuir o texto “Deletar” ou “Excluir” e ser da cor vermelha. 
- [ ] O botão de deletar deve ser o último a aparecer. 


#### Botões de Salvar e Voltar

- [ ] Deixar botão de salvar alinhado ao lado esquerdo e no final do formulário.

- [ ] Não é preciso um botão de voltar dentro de um formulário que possui fluxo com uma tela só, mas caso haja necessidade o botão deve ficar ao lado direito do botão de salvar. 

**Exemplo**

![](assets/admin_panel/35FF28B8-FB3A-4C0E-A7F1-8A395E7F181A%207.png)


### Alinhamento dos Campos

- [ ] O ideal é que o formulário seja de uma coluna. Mas para que a tela não fique com barra de rolagem longa, quando houver muitos campos, deixar campos em colunas/alinhados. 

![](assets/admin_panel/DE90C7AA-C95D-46AB-8D84-E3E647B8BD44%206.png)


**Exemplo**

![](admin_panel/Screen%20Shot%202020-05-27%20at%2011.39.46%206.png)


### Validações

- [ ] Não esquecer de colocar * (asterisco) nos campos obrigatórios e deve ficar a direita da label.

![](assets/admin_panel/2CA278A8-28D5-4F16-BAF1-A8B886646C6F%206.png)

- [ ] Padronizar a validação dos campos. Escolher entre utilizar a validação que o “required” oferece ou deixa todos iguais ao do componente. 


## Telas com Listagem/Tabelas

![](assets/admin_panel/3BFC2576-5DA7-4CAD-915E-C716BDA7FD75%206.png)


- [ ] O botão de adicionar deve ficar fora da área de filtro e alinhado a esquerda da tela.
- [ ] Botões de editar e excluir, ou outras ações do projeto devem ficar na coluna “Ações”.


### Área de Filtro

- [ ] Os campos do filtro devem possuir label.
- [ ] O campo pesquisar deve possuir a seguinte estrutura:
> **Texto da label:** “Termo”  
> **Texto do placeholder:** “Pesquisar por [termos pesquisáveis]”  


### Coluna Principal 

- [ ] Os registros da coluna principal devem ser links e redirecionar para tela de detalhe, quando houver.
- [ ] O link deve ser na cor padrão azul de link.

**Exemplo**

![](assets/admin_panel/Screen%20Shot%202020-05-27%20at%2011.49.08%206.png)






