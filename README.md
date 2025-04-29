# Projeto de Serviço de Notificações Assíncronas

## 📋 Descrição do Projeto

O projeto consiste na criação de um serviço de notificações assíncronas, desenvolvido em **Node.js** com **TypeScript**. O objetivo é implementar uma **API REST** para gerenciar notificações, representadas por "tasks", que passam por diferentes estados, como `pending` (pendente) até serem `concluídas` (processadas).  

As tasks são inicialmente criadas, armazenadas no **MongoDB**, e processadas por no mínimo **3 workers** atuando de forma assíncrona, garantindo o envio eficiente das mensagens.

---

## 🧩 Arquitetura do Sistema

![Diagrama de Arquitetura](https://github.com/user-attachments/assets/65e3ade4-df29-4238-8950-1c4d9861c09a)

---

## 📚 Tecnologias Utilizadas

- **Node.js** + **TypeScript**
- **MongoDB**: Armazenamento de tasks e seus respectivos status.
- **RabbitMQ**: Gerenciamento da fila de mensagens.
- **Docker Compose**: Orquestração dos serviços localmente.
- **GitHub Actions**: Pipeline de CI para build, lint e testes.
- **Postman**: Criação de coleção de testes end-to-end.

---

## 🌐 API REST Endpoints

| Método | Rota            | Descrição                          |
|:------:|:-----------------|:----------------------------------|
| POST   | `/tasks`         | Criação de uma nova task          |
| GET    | `/tasks`         | Listagem de todas as tasks        |
| GET    | `/tasks/:id`     | Consulta do status de uma task    |
| PATCH  | `/tasks/:id`     | Atualização do status da task     |

- Cada task é criada inicialmente com o status `pending`.
- Após ser processada por um worker (que imprime uma mensagem no console), o status é alterado para `concluída`.

---

## ⚙️ Funcionamento dos Workers

- Os workers **não acessam diretamente** o banco de dados.
- Toda comunicação ocorre via API, garantindo centralização da lógica de negócio.
- Workers consomem tasks da fila RabbitMQ de forma **assíncrona**.
- Mínimo de **3 workers** ativos processando simultaneamente.

---

## 🚀 Extra (Opcional)

- Implementação dos mesmos endpoints via **gRPC** como alternativa ao REST.

---

## 🧪 Testes Automatizados

- Coleção **Postman** disponível para todos os endpoints.
- Cada rota inclui testes básicos para verificação dos códigos de status HTTP.
- Possibilidade de execução em pipelines CI/CD.

---

## 🛠️ Boas Práticas e Padrões

- Utilização de **interfaces** para definição de contratos.
- Adoção de **Design Patterns**:
  - **Factory Pattern**: Para criação de serviços de persistência.
  - **Observer Pattern** ou **Strategy Pattern**: Para envio de diferentes tipos de notificações.
- Código versionado com **GIT** seguindo o padrão de **Conventional Commits**.  
  Referência: [Conventional Commits](https://medium.com/linkapi-solutions/conventional-commits-pattern-3778d1a1e657)

---

## 📦 Docker e Infraestrutura Local

- Arquivo `docker-compose.yml` incluso para facilitar o setup local.
- A comunicação entre a API, MongoDB e RabbitMQ é feita via variáveis de ambiente.

Com um único comando, toda a infraestrutura pode ser levantada localmente para desenvolvimento e testes.

---

