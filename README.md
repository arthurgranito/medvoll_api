# 🏥 API Sistema Médico - Voll Med

Uma API REST completa para gerenciamento de sistema médico, desenvolvida com Spring Boot 3, PostgreSQL, JWT Authentication e documentação Swagger.

## 📋 Índice

- [Funcionalidades](#-funcionalidades)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Pré-requisitos](#-pré-requisitos)
- [Como Executar](#-como-executar)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Endpoints da API](#-endpoints-da-api)
- [Autenticação](#-autenticação)
- [Documentação da API](#-documentação-da-api)
- [Testes](#-testes)
- [Banco de Dados](#-banco-de-dados)
- [Contribuição](#-contribuição)

## ✨ Funcionalidades

### 🔐 Autenticação e Segurança
- **JWT Authentication**: Sistema de autenticação baseado em tokens JWT
- **Spring Security**: Configuração de segurança robusta
- **Validação de dados**: Validação completa de entrada com Bean Validation

### 👨‍⚕️ Gestão de Médicos
- ✅ Cadastro de médicos com dados completos
- ✅ Listagem paginada de médicos ativos
- ✅ Atualização de informações médicas
- ✅ Exclusão lógica (soft delete)
- ✅ Busca por especialidade
- ✅ Validação de CRM único

### 👥 Gestão de Pacientes
- ✅ Cadastro de pacientes com dados pessoais
- ✅ Listagem paginada de pacientes ativos
- ✅ Atualização de informações do paciente
- ✅ Exclusão lógica (soft delete)
- ✅ Validação de CPF único

### 📅 Gestão de Consultas
- ✅ Agendamento de consultas
- ✅ Cancelamento de consultas
- ✅ Validação de horários disponíveis
- ✅ Verificação de disponibilidade do médico
- ✅ Relacionamento médico-paciente

### 🗄️ Banco de Dados
- **PostgreSQL**: Banco de dados principal
- **Flyway**: Migração de banco de dados
- **JPA/Hibernate**: ORM para persistência
- **Soft Delete**: Exclusão lógica mantendo histórico

## 🛠️ Tecnologias Utilizadas

- **Java 17**
- **Spring Boot 3.5.4**
- **Spring Security**
- **Spring Data JPA**
- **PostgreSQL**
- **Flyway Migration**
- **JWT (Auth0)**
- **Swagger/OpenAPI 3**
- **JUnit 5**
- **Lombok**
- **Maven**

## ⚙️ Pré-requisitos

- Java 17 ou superior
- Maven 3.6+
- PostgreSQL 12+
- Git

## 🚀 Como Executar

### 1. Clone o repositório
```bash
git clone https://github.com/arthurgranito/vollmed_api.git
cd vollmed_api
```

### 2. Configure o banco de dados PostgreSQL

Crie um banco de dados chamado `vollmed_api`:
```sql
CREATE DATABASE vollmed_api;
```

### 3. Configure as variáveis de ambiente

Crie um arquivo `.env` na raiz do projeto ou configure as variáveis de ambiente:

```bash
# Configurações do banco de dados
DATABASE_URL=jdbc:postgresql://localhost:5432/vollmed_api
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=sua_senha

# Chave secreta para JWT (recomendado: gerar uma chave forte)
JWT_SECRET=sua_chave_secreta_muito_segura
```

### 4. Execute o projeto

```bash
# Compilar e executar
mvn spring-boot:run

# Ou compilar primeiro e depois executar
mvn clean install
java -jar target/api-0.0.1-SNAPSHOT.jar
```

### 5. Acesse a aplicação

- **API**: http://localhost:8080
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **Health Check**: http://localhost:8080/actuator/health

## 📁 Estrutura do Projeto

```
src/
├── main/
│   ├── java/med/voll/api/
│   │   ├── controller/          # Controllers REST
│   │   ├── domain/             # Entidades e lógica de negócio
│   │   │   ├── medico/         # Domínio de médicos
│   │   │   ├── paciente/       # Domínio de pacientes
│   │   │   ├── consulta/       # Domínio de consultas
│   │   │   ├── usuario/        # Domínio de usuários
│   │   │   └── endereco/       # Domínio de endereços
│   │   └── infra/              # Configurações de infraestrutura
│   │       ├── security/       # Configurações de segurança
│   │       ├── springdoc/      # Configurações do Swagger
│   │       └── exception/      # Tratamento de exceções
│   └── resources/
│       ├── application.properties
│       └── db/migration/       # Scripts de migração Flyway
└── test/
    └── java/med/voll/api/
        ├── controller/          # Testes de controllers
        └── domain/             # Testes de domínio
```

## 🔗 Endpoints da API

### Autenticação
- `POST /login` - Autenticação e geração de token JWT

### Médicos
- `POST /medicos` - Cadastrar médico
- `GET /medicos` - Listar médicos (paginação)
- `GET /medicos/{id}` - Buscar médico por ID
- `PUT /medicos` - Atualizar médico
- `DELETE /medicos/{id}` - Excluir médico

### Pacientes
- `POST /pacientes` - Cadastrar paciente
- `GET /pacientes` - Listar pacientes (paginação)
- `GET /pacientes/{id}` - Buscar paciente por ID
- `PUT /pacientes` - Atualizar paciente
- `DELETE /pacientes/{id}` - Excluir paciente

### Consultas
- `POST /consultas` - Agendar consulta
- `DELETE /consultas` - Cancelar consulta

## 🔐 Autenticação

A API utiliza autenticação JWT. Para acessar endpoints protegidos:

1. **Faça login**:
```bash
POST /login
Content-Type: application/json

{
  "login": "seu_usuario",
  "senha": "sua_senha"
}
```

2. **Use o token retornado**:
```bash
Authorization: Bearer seu_token_jwt
```

## 📚 Documentação da API

A documentação completa da API está disponível através do Swagger UI:

- **URL**: http://localhost:8080/swagger-ui.html
- **OpenAPI JSON**: http://localhost:8080/v3/api-docs

### Funcionalidades da Documentação:
- ✅ Todos os endpoints documentados
- ✅ Schemas de request/response
- ✅ Autenticação JWT integrada
- ✅ Exemplos de uso
- ✅ Teste direto dos endpoints

## 🧪 Testes

### Executar todos os testes
```bash
mvn test
```

## 🗄️ Banco de Dados

### Estrutura das Tabelas

#### Tabela `medicos`
- `id` (BIGSERIAL, PK)
- `nome` (VARCHAR(100))
- `email` (VARCHAR(100), UNIQUE)
- `crm` (VARCHAR(6), UNIQUE)
- `especialidade` (VARCHAR(100))
- `telefone` (VARCHAR(20))
- `ativo` (BOOLEAN)
- Dados de endereço (logradouro, bairro, cep, etc.)

#### Tabela `pacientes`
- `id` (BIGSERIAL, PK)
- `nome` (VARCHAR(100))
- `email` (VARCHAR(100), UNIQUE)
- `cpf` (VARCHAR(11), UNIQUE)
- `telefone` (VARCHAR(20), UNIQUE)
- `ativo` (BOOLEAN)
- Dados de endereço

#### Tabela `consultas`
- `id` (BIGSERIAL, PK)
- `medico_id` (BIGINT, FK)
- `paciente_id` (BIGINT, FK)
- `data` (TIMESTAMP)
- `motivo_cancelamento` (VARCHAR(100))

#### Tabela `usuarios`
- `id` (BIGSERIAL, PK)
- `login` (VARCHAR(100), UNIQUE)
- `senha` (VARCHAR(255))

### Migrações Flyway

O projeto utiliza Flyway para gerenciar migrações do banco de dados:

- `V1__create-table-medicos.sql`
- `V2__alter-table-medicos-add-column-telefone.sql`
- `V3__alter-table-medicos-add-column-ativo.sql`
- `V4__create-table-usuarios.sql`
- `V5__create-table-pacientes.sql`
- `V6__alter-table-pacientes-add-column-ativo.sql`
- `V7__create-table-consulta.sql`
- `V8__alter-table-consultas-add-column-motivo-cancelamento.sql`

## 👨‍💻 Autor

**Arthur Granito**
- GitHub: [@arthurgranito](https://github.com/seu-usuario)
- LinkedIn: [Arthur Granito](https://linkedin.com/in/arthurgranito)

⭐ Se este projeto te ajudou, considere dar uma estrela no repositório! 