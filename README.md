# Backend API REST com FastAPI

> 🚀 **O Projeto:** Uma API RESTful completa desenvolvida em Python com o framework FastAPI. Este projeto implementa um backend robusto, um sistema que potenciaria um aplicativo de e-commerce ou um serviço de delivery., seguindo as melhores práticas do mercado.
>
## 🎯 O Desafio (Para não técnicos) 

O objetivo deste projeto é criar a "espinha dorsal" de uma aplicação moderna. Imagine um aplicativo (como um site ou um app de celular) que precisa:

* Registrar novos usuários de forma segura.
* Permitir que usuários façam login e acessem dados que são só seus.
* Salvar, ler, atualizar e apagar informações (como postagens de blog, produtos, tarefas, etc.).

Esta API faz tudo isso de forma rápida, segura e escalável.

## ✨ Principais Funcionalidades

* **Sistema de Autenticação Seguro:** Implementação completa de login com tokens JWT (OAuth2). Senhas são 100% criptografadas (hashing) e nunca armazenadas em texto puro.
* **Gerenciamento de Usuários:** CRUD (Criar, Ler, Atualizar, Deletar) completo para usuários.
* **Gerenciamento de Pedidos:** CRUD completo para Pedidos.
* **Documentação Interativa:** A API gera automaticamente uma documentação navegável (Swagger UI e ReDoc) que permite testar os endpoints diretamente do navegador.
* **Alta Performance:** Capaz de lidar com milhares de requisições por segundo.

## 🛠️ Tecnologias e Ferramentas Utilizadas

| Tecnologia | Propósito |
| :--- | :--- |
| **FastAPI** | O framework principal, escolhido por sua altíssima performance e facilidade de uso. |
| **Pydantic** | Usado para validação de dados (garante que os dados de entrada e saída estão corretos). |
| **SQLAlchemy** | O "tradutor" (ORM) que conecta o código Python ao banco de dados relacional. |
| **Alembic** | Ferramenta para "versionar" o banco de dados (migrations), permitindo atualizações seguras da estrutura. |
| **JWT (pyjwt)** | Para criação e validação dos tokens de autenticação seguros. |
| **Passlib & Bcrypt** | Para criptografia (hashing) de senhas. |
| **Uvicorn** | O servidor web (ASGI) que executa a aplicação FastAPI. |
| **Pytest** | Para a criação e execução de testes automatizados, garantindo a qualidade do código. |
| **PostgreSQL / SQLite**| O banco de dados relacional que armazena todas as informações. |
| **Git & GitHub** | Para controle de versão e hospedagem do código. |

---

## 📚 Documentação e Arquitetura (Para Técnicos)

Esta seção detalha as escolhas técnicas e como interagir com o projeto.

### 🏛️ Arquitetura e Decisões de Design

1.  **Repository Pattern (Padrão de Repositório):** A lógica de negócios (serviços) está desacoplada da lógica de acesso ao banco de dados (repositórios). Isso torna o código mais limpo, fácil de manter e muito mais fácil de testar (permitindo mocks do repositório).
2.  **Dependency Injection (Injeção de Dependência):** O FastAPI é usado extensivamente para injetar dependências, como as sessões do banco de dados e os repositórios, diretamente nos endpoints.
3.  **Segurança (OAuth2 com JWT):** Foi implementado o fluxo `OAuth2PasswordBearer`. O endpoint `/token` gera um `access_token` JWT após validar o usuário. Os endpoints protegidos exigem este token, que é validado para identificar o usuário logado.
4.  **Migrations com Alembic:** O Alembic é usado para gerenciar as alterações no esquema do banco de dados. Qualquer alteração nos modelos (Models) do SQLAlchemy pode ser refletida no banco de dados executando `alembic revision --autogenerate` e `alembic upgrade head`.

### 📖 Documentação Interativa da API

Uma das grandes vantagens do FastAPI é a documentação automática. Após executar o projeto, você pode acessar:

* **Swagger UI:** `http://127.0.0.1:8000/docs`
* **ReDoc:** `http://127.0.0.1:8000/redoc`

### 🔩 Principais Endpoints

| Método | Endpoint | Descrição | Requer Auth? |
| :--- | :--- | :--- | :--- |
| `POST` | `/token` | Autentica um usuário e retorna um Access Token JWT. | ❌ Não |
| `POST` | `/users` | Cria um novo usuário (registro). | ❌ Não |
| `GET` | `/users` | Lista todos os usuários. | ✅ Sim |
| `GET` | `/users/{id}` | Busca um usuário por ID. | ✅ Sim |
| `POST` | `/[recurso]` | Cria um novo [recurso (ex: tarefa, produto)]. | ✅ Sim |
| `GET` | `/[recurso]` | Lista todos os [recursos] do usuário logado. | ✅ Sim |
| `PUT` | `/[recurso]/{id}` | Atualiza um [recurso] específico. | ✅ Sim |
| `DELETE` | `/[recurso]/{id}` | Deleta um [recurso] específico. | ✅ Sim |

