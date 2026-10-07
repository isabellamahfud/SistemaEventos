#  Sistema de Gestão de Eventos

Sistema completo para **gestão de eventos, estoque, vendas e atendimento em PDV**, desenvolvido para uso em ambiente real.

O projeto possui uma aplicação para gerenciamento administrativo no **Windows** e uma solução de **PDV para Android**, integradas ao mesmo banco de dados.

---

##  Sobre o projeto

O **Sistema de Eventos** foi desenvolvido para centralizar o controle operacional de eventos, permitindo administrar produtos, estoque, mesas, vendedores/atendentes e vendas em um único sistema.

A aplicação foi pensada para substituir controles manuais e facilitar o acompanhamento das operações durante um evento.

### Principais objetivos

*  Controle de estoque
*  Registro de vendas
*  Emissão de tickets
*  Controle de mesas
*  Gerenciamento de atendentes
*  Relatórios de vendas
*  Cadastro e identificação de eventos
*  Atualização automática do estoque
*  Persistência dos dados em PostgreSQL

---

##  Funcionalidades

###  Sistema Administrativo

O sistema para Windows permite:

* Cadastro de eventos
* Cadastro, edição e exclusão de produtos
* Cadastro de mesas
* Cadastro de vendedores/atendentes
* Cadastro de fornecedores
* Controle de estoque inicial
* Registro de valor, quantidade e data de entrada dos produtos
* Ajustes de estoque
* Entrada e saída de produtos
* Consulta de estoque
* Resumo geral das vendas
* Relatórios de movimentação

---

###  PDV para Android

O aplicativo de PDV permite que o atendente:

1. Identifique o PDV utilizado
2. Selecione a mesa
3. Informe o atendente responsável
4. Adicione produtos ao pedido
5. Informe a quantidade de cada produto
6. Finalize a venda
7. Atualize automaticamente o estoque
8. Gere os tickets correspondentes aos itens vendidos

###  Sistema de tickets

Cada unidade vendida pode gerar um ticket individual.

**Exemplo:**

```text
2x Refrigerante
1x Pão de Queijo
```

Resultado:

```text
 Ticket 1 — Refrigerante
 Ticket 2 — Refrigerante
 Ticket 3 — Pão de Queijo
```

O sistema também poderá disponibilizar a impressão do resumo do pedido, conforme a configuração do evento.

---


##  Tecnologias utilizadas

### Backend

*  Java
*  Spring Boot
*  Maven
*  PostgreSQL
*  Spring Data JPA
*  REST API

### Desenvolvimento

* Visual Studio Code
* Git
* GitHub
* Postman

### Futuras integrações

*  Android
*  Impressão de tickets
*  Banco de dados/API em ambiente online

---

##  Banco de dados

O sistema utiliza **PostgreSQL** para armazenar as informações da aplicação.

Entre os principais dados estão:

```text
Eventos
Produtos
Estoque
Mesas
Atendentes
Fornecedores
Pedidos
Itens dos pedidos
Vendas
Tickets
```

### Fluxo básico

```text
                 ┌──────────────┐
                 │    EVENTO    │
                 └──────┬───────┘
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
     ┌─────────┐   ┌─────────┐   ┌──────────┐
     │ Produtos│   │  Mesas  │   │Atendentes│
     └────┬────┘   └────┬────┘   └─────┬────┘
          │             │              │
          └─────────────┼──────────────┘
                        ▼
                 ┌─────────────┐
                 │    PEDIDO   │
                 └──────┬──────┘
                        │
                        ▼
                 ┌─────────────┐
                 │    VENDA    │
                 └──────┬──────┘
                        │
              ┌─────────┴─────────┐
              ▼                   ▼
        ┌──────────┐        ┌──────────┐
        │  ESTOQUE │        │  TICKETS │
        └──────────┘        └──────────┘
```

---

##  Pré-requisitos

Antes de executar o projeto, instale:

* Java JDK 17 ou superior
* Maven
* PostgreSQL
* Git

Verifique as instalações:

```bash
java -version
mvn -version
psql --version
git --version
```

---

##  Instalação

Clone o repositório:

```bash
git clone SEU_LINK_DO_REPOSITORIO
```

Entre na pasta:

```bash
cd SistemaEventos
```

---

##  Executando o projeto

Compile o projeto:

```bash
mvn clean install
```

Execute a aplicação:

```bash
mvn spring-boot:run
```

A API ficará disponível localmente em:

```text
http://localhost:8080
```

---

##  API

A aplicação utiliza uma API REST para comunicação entre os sistemas.

Exemplo de estrutura:

```text
GET    /api/eventos
POST   /api/eventos
PUT    /api/eventos/{id}
DELETE /api/eventos/{id}
```

Produtos:

```text
GET    /api/produtos
POST   /api/produtos
PUT    /api/produtos/{id}
DELETE /api/produtos/{id}
```

Estoque:

```text
GET    /api/estoque
POST   /api/estoque/entrada
POST   /api/estoque/saida
```

Vendas:

```text
POST   /api/pedidos
GET    /api/vendas
GET    /api/vendas/resumo
```

> Os endpoints podem ser expandidos conforme novas funcionalidades forem implementadas.

---

##  Fluxo de uma venda

```text
Atendente
    │
    ▼
Identificação do PDV
    │
    ▼
Seleção da mesa
    │
    ▼
Seleção dos produtos
    │
    ▼
Definição das quantidades
    │
    ▼
Confirmação do pedido
    │
    ├──────────────► Atualização do estoque
    │
    ├──────────────► Registro da venda
    │
    └──────────────► Geração dos tickets
```

---

##  Relatórios

O sistema possui estrutura para geração de informações como:

* Total de vendas
* Quantidade de produtos vendidos
* Produtos mais vendidos
* Movimentação de estoque
* Vendas por PDV
* Vendas por atendente
* Vendas por mesa
* Resumo financeiro do evento

---

##  Segurança

O projeto deve utilizar boas práticas para proteção das informações:

* Credenciais do banco fora do código-fonte
* Variáveis de ambiente
* Validação dos dados recebidos pela API
* Controle de acesso
* Tratamento de exceções
* Proteção dos endpoints administrativos

---

##  Status do projeto

 **Em desenvolvimento**

O sistema está sendo desenvolvido de forma incremental, começando pela estrutura do backend, banco de dados e funcionalidades administrativas.

### Roadmap

* [x] Estrutura inicial do projeto Java
* [x] Configuração do Maven
* [x] Configuração do Spring Boot
* [ ] Configuração completa do PostgreSQL
* [ ] CRUD de eventos
* [ ] CRUD de produtos
* [ ] Controle de estoque
* [ ] Cadastro de mesas
* [ ] Cadastro de atendentes
* [ ] Sistema de pedidos
* [ ] Registro de vendas
* [ ] Geração de tickets
* [ ] Relatórios
* [ ] Aplicação Android para PDV
* [ ] Impressão de tickets
* [ ] Deploy da API
* [ ] Documentação completa da API

---

##  Desenvolvimento

Projeto desenvolvido como um sistema de software completo para gerenciamento de operações em eventos, utilizando tecnologias modernas de desenvolvimento backend e banco de dados relacional.

### Foco técnico

```text
Java
   ↓
Spring Boot
   ↓
REST API
   ↓
Spring Data JPA
   ↓
PostgreSQL
   ↓
Windows / Android
```

---

##  Licença

Este projeto possui finalidade de desenvolvimento e utilização conforme as necessidades definidas para o sistema de eventos.
