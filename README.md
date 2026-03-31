# 🏥 Voll.med - API REST com Boas Práticas Spring Boot 3

## 📋 Índice
- [Sobre o Projeto](#-sobre-o-projeto)
- [Funcionalidades](#%EF%B8%8F-funcionalidades)
- [Arquitetura](#%EF%B8%8F-arquitetura)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação e Configuração](#-instalação-e-configuração)
- [Banco de Dados](#%EF%B8%8F-banco-de-dados)
- [Segurança](#-segurança)
- [Boas Práticas Implementadas](#-boas-práticas-implementadas)
- [Exemplos de Uso da API](#-exemplos-de-uso-da-api)
- [Roadmap](#%EF%B8%8F-roadmap)
- [Referências](#-referências)

---

## 📖 Sobre o Projeto

A **Voll.med** é uma API REST desenvolvida com **Spring Boot 3** para gerenciamento de clínica médica fictícia. Este projeto implementa as melhores práticas de desenvolvimento com Spring Framework, focando em código limpo, arquitetura sólida e padrões modernos de desenvolvimento.

Este projeto foi desenvolvido durante o **Curso de Spring Boot 3: documente, teste e prepare uma API para o deploy** da **DevMedia**, com ênfase em:

- 🏗️ **Arquitetura em Camadas** bem definida
- 🔒 **Segurança** com JWT (JSON Web Tokens)
- 📊 **Persistência** com JPA/Hibernate
- 🗃️ **Versionamento de Banco** com Flyway
- ✅ **Validações** robustas com Bean Validation
- 📝 **DTOs** com Records do Java 17
- 🎯 **RESTful** seguindo princípios REST

### 🎯 Objetivo

Criar uma API backend robusta para gestão de consultas médicas, permitindo:
- Cadastro e gerenciamento de médicos
- Cadastro e gerenciamento de pacientes
- Autenticação segura com JWT
- Preparação para agendamento de consultas (em desenvolvimento)

---

## ⚙️ Funcionalidades

### ✅ Implementadas

#### Médicos
- ✅ **Cadastro** de médicos com especialidade e endereço
- ✅ **Listagem paginada** de médicos ativos
- ✅ **Atualização** de dados cadastrais
- ✅ **Exclusão lógica** (inativação) de médicos
- ✅ **Detalhamento** de médico específico por ID

#### Pacientes
- ✅ **Cadastro** de pacientes com dados completos
- ✅ **Listagem paginada** de pacientes ativos
- ✅ **Atualização** de informações
- ✅ **Exclusão lógica** (inativação) de pacientes
- ✅ **Detalhamento** de paciente específico por ID

#### Autenticação
- ✅ **Login** com geração de token JWT
- ✅ **Proteção** de rotas com autenticação
- ✅ **Validação** de tokens em requisições

### 🚧 Em Desenvolvimento

- ⏳ **Agendamento de consultas** (próxima versão)
- ⏳ **Cancelamento de consultas** (próxima versão)
- ⏳ **Validações de regras de negócio** para consultas
- ⏳ **Documentação Swagger/OpenAPI**

---

## 🏗️ Arquitetura

O projeto segue uma **arquitetura em camadas** (Layered Architecture), separando claramente as responsabilidades:

```
┌─────────────────────────────────────────────────────────┐
│                   CONTROLLER LAYER                      │
│              (Recebe requisições HTTP)                  │
│  - MedicoController, PacienteController                 │
│  - AutenticacaoController                               │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                    DOMAIN LAYER                         │
│         (Lógica de negócio e entidades)                 │
│  - Entidades: Medico, Paciente, Usuario                 │
│  - Repositories: Spring Data JPA                        │
│  - DTOs: Records para transferência de dados            │
│  - Services: AutenticacaoService                        │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                INFRASTRUCTURE LAYER                     │
│          (Configurações e cross-cutting)                │
│  - Security: JWT, Filtros, Configurações                │
│  - Exception Handling: TratadorDeErros                  │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                   DATABASE LAYER                        │
│              (MySQL + Flyway Migrations)                │
└─────────────────────────────────────────────────────────┘
```

### Padrões de Design Implementados

- ✅ **Repository Pattern** - Abstração de acesso a dados
- ✅ **DTO Pattern** - Separação entre entidades e dados de transporte
- ✅ **Dependency Injection** - Injeção via Spring Framework
- ✅ **REST Pattern** - Endpoints RESTful com verbos HTTP apropriados
- ✅ **Filter Chain** - Filtro de segurança JWT
- ✅ **Soft Delete** - Exclusão lógica com flag `ativo`

---

## 🛠 Tecnologias Utilizadas

### Core Framework
- **[Java 17](https://www.oracle.com/java)** - LTS com Records, Pattern Matching e melhorias
- **[Spring Boot 3.0.0-M5](https://spring.io/projects/spring-boot)** - Framework principal (Milestone)
- **[Maven](https://maven.apache.org)** - Gerenciamento de dependências e build

### Persistência e Banco de Dados
- **[Spring Data JPA](https://spring.io/projects/spring-data-jpa)** - Abstração de persistência
- **[Hibernate](https://hibernate.org)** - Implementação JPA/ORM
- **[MySQL 8.0+](https://www.mysql.com)** - Banco de dados relacional
- **[Flyway](https://flywaydb.org)** - Controle de versão e migração de banco

### Segurança
- **[Spring Security](https://spring.io/projects/spring-security)** - Framework de segurança
- **[Auth0 Java JWT 4.2.1](https://github.com/auth0/java-jwt)** - Geração e validação de JWT

### Validação e Utilitários
- **[Bean Validation (Jakarta)](https://beanvalidation.org)** - Validação declarativa de dados
- **[Lombok](https://projectlombok.org)** - Redução de boilerplate (getters, setters, etc)

### Desenvolvimento
- **[Spring Boot DevTools](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.devtools)** - Hot reload durante desenvolvimento

### Testes
- **[Spring Boot Test](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing)** - Suporte a testes
- **[Spring Security Test](https://docs.spring.io/spring-security/reference/servlet/test/index.html)** - Testes de segurança

---

## 📁 Estrutura do Projeto

```
spring-boot-3-best-practices-main/
│
├── src/
│   ├── main/
│   │   ├── java/med/voll/api/
│   │   │   ├── ApiApplication.java              # Classe principal
│   │   │   │
│   │   │   ├── controller/                      # Camada de apresentação
│   │   │   │   ├── AutenticacaoController.java
│   │   │   │   ├── HelloController.java
│   │   │   │   ├── MedicoController.java
│   │   │   │   └── PacienteController.java
│   │   │   │
│   │   │   ├── domain/                          # Camada de domínio
│   │   │   │   │
│   │   │   │   ├── endereco/
│   │   │   │   │   ├── Endereco.java           # Entidade embeddable
│   │   │   │   │   └── DadosEndereco.java      # DTO Record
│   │   │   │   │
│   │   │   │   ├── medico/
│   │   │   │   │   ├── Medico.java             # Entidade JPA
│   │   │   │   │   ├── MedicoRepository.java   # Interface Repository
│   │   │   │   │   ├── Especialidade.java      # Enum
│   │   │   │   │   ├── DadosCadastroMedico.java
│   │   │   │   │   ├── DadosAtualizacaoMedico.java
│   │   │   │   │   ├── DadosListagemMedico.java
│   │   │   │   │   └── DadosDetalhamentoMedico.java
│   │   │   │   │
│   │   │   │   ├── paciente/
│   │   │   │   │   ├── Paciente.java           # Entidade JPA
│   │   │   │   │   ├── PacienteRepository.java # Interface Repository
│   │   │   │   │   ├── DadosCadastroPaciente.java
│   │   │   │   │   ├── DadosAtualizacaoPaciente.java
│   │   │   │   │   ├── DadosListagemPaciente.java
│   │   │   │   │   └── DadosDetalhamentoPaciente.java
│   │   │   │   │
│   │   │   │   └── usuario/
│   │   │   │       ├── Usuario.java            # Entidade JPA
│   │   │   │       ├── UsuarioRepository.java
│   │   │   │       ├── AutenticacaoService.java # Service de autenticação
│   │   │   │       └── DadosAutenticacao.java   # DTO Record
│   │   │   │
│   │   │   └── infra/                           # Camada de infraestrutura
│   │   │       │
│   │   │       ├── security/
│   │   │       │   ├── SecurityConfigurations.java  # Config Spring Security
│   │   │       │   ├── SecurityFilter.java          # Filtro JWT
│   │   │       │   ├── TokenService.java            # Serviço de tokens
│   │   │       │   └── DadosTokenJWT.java           # DTO Token
│   │   │       │
│   │   │       └── exception/
│   │   │           └── TratadorDeErros.java         # Global exception handler
│   │   │
│   │   └── resources/
│   │       ├── application.properties           # Configurações da aplicação
│   │       └── db/migration/                    # Scripts Flyway
│   │           ├── V1__create-table-medicos.sql
│   │           ├── V2__alter-table-medicos-add-column-telefone.sql
│   │           ├── V3__alter-table-medicos-add-column-ativo.sql
│   │           ├── V4__create-table-pacientes.sql
│   │           └── V5__create-table-usuarios.sql
│   │
│   └── test/
│       └── java/med/voll/api/
│           └── ApiApplicationTests.java
│
├── .mvn/                                        # Maven wrapper
├── .gitignore
├── mvnw                                         # Maven wrapper Unix
├── mvnw.cmd                                     # Maven wrapper Windows
├── pom.xml                                      # Configuração Maven
└── README.md
```

---

## 📦 Pré-requisitos

### Software Necessário

- ☕ **Java 17 ou superior** ([Download JDK 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html))
- 🔧 **Maven 3.8+** ([Download Maven](https://maven.apache.org/download.cgi))
- 🗄️ **MySQL 8.0+** ([Download MySQL](https://dev.mysql.com/downloads/mysql/))
- 💻 **IDE recomendada**: IntelliJ IDEA, Eclipse ou VS Code com Java Extensions

### Verificar Instalação

```bash
# Verificar Java
java -version
# Saída esperada: java version "17.x.x"

# Verificar Maven
mvn -version
# Saída esperada: Apache Maven 3.8.x

# Verificar MySQL
mysql --version
# Saída esperada: mysql Ver 8.0.x
```

---

## 🚀 Instalação e Configuração

### 1️⃣ Clonar o Repositório

```bash
git clone <url-do-repositorio>
cd spring-boot-3-best-practices-main
```

### 2️⃣ Configurar o Banco de Dados

Conecte ao MySQL e crie o banco de dados:

```sql
CREATE DATABASE vollmed_api;
```

### 3️⃣ Configurar Credenciais

Edite o arquivo `src/main/resources/application.properties`:

```properties
# Configuração do banco de dados
spring.datasource.url=jdbc:mysql://localhost/vollmed_api
spring.datasource.username=seu_usuario
spring.datasource.password=sua_senha

# Configuração JPA/Hibernate
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# Segurança
server.error.include-stacktrace=never

# JWT Secret (use variável de ambiente em produção)
api.security.token.secret=${JWT_SECRET:12345678}
```

### 4️⃣ Configurar Segredo JWT (Recomendado)

```bash
# Linux/Mac
export JWT_SECRET=sua-chave-secreta-muito-segura-aqui

# Windows (PowerShell)
$env:JWT_SECRET="sua-chave-secreta-muito-segura-aqui"

# Windows (CMD)
set JWT_SECRET=sua-chave-secreta-muito-segura-aqui
```

### 5️⃣ Instalar Dependências

```bash
mvn clean install
```

### 6️⃣ Executar a Aplicação

```bash
# Usando Maven
mvn spring-boot:run

# Ou usando Maven Wrapper (recomendado)
./mvnw spring-boot:run         # Linux/Mac
mvnw.cmd spring-boot:run       # Windows
```

### 7️⃣ Verificar Execução

A aplicação estará rodando em: **`http://localhost:8080`**

Teste com:
```bash
curl http://localhost:8080/hello
```

---

## 🗄️ Banco de Dados

### Gerenciamento com Flyway

O projeto utiliza **Flyway** para versionamento e migração automática do banco de dados. As migrations são executadas automaticamente na inicialização.

### Migrations Disponíveis

| Versão | Arquivo | Descrição |
|--------|---------|-----------|
| V1 | `V1__create-table-medicos.sql` | Cria tabela `medicos` |
| V2 | `V2__alter-table-medicos-add-column-telefone.sql` | Adiciona coluna `telefone` |
| V3 | `V3__alter-table-medicos-add-column-ativo.sql` | Adiciona coluna `ativo` (soft delete) |
| V4 | `V4__create-table-pacientes.sql` | Cria tabela `pacientes` |
| V5 | `V5__create-table-usuarios.sql` | Cria tabela `usuarios` |

### Modelo de Dados

#### Tabela: medicos
```sql
medicos
├── id (BIGINT, PK, AUTO_INCREMENT)
├── nome (VARCHAR(100), NOT NULL)
├── email (VARCHAR(100), UNIQUE, NOT NULL)
├── crm (VARCHAR(6), UNIQUE, NOT NULL)
├── especialidade (VARCHAR(100), NOT NULL)
├── telefone (VARCHAR(20))
├── ativo (TINYINT, NOT NULL)
└── endereco (embedded)
    ├── logradouro (VARCHAR(100), NOT NULL)
    ├── bairro (VARCHAR(100), NOT NULL)
    ├── cep (VARCHAR(9), NOT NULL)
    ├── complemento (VARCHAR(100))
    ├── numero (VARCHAR(20))
    ├── uf (CHAR(2), NOT NULL)
    └── cidade (VARCHAR(100), NOT NULL)
```

#### Tabela: pacientes
```sql
pacientes
├── id (BIGINT, PK, AUTO_INCREMENT)
├── nome (VARCHAR(100), NOT NULL)
├── email (VARCHAR(100), UNIQUE, NOT NULL)
├── cpf (VARCHAR(14), UNIQUE, NOT NULL)
├── telefone (VARCHAR(20), NOT NULL)
├── ativo (TINYINT, NOT NULL)
└── endereco (embedded)
    ├── logradouro (VARCHAR(100), NOT NULL)
    ├── bairro (VARCHAR(100), NOT NULL)
    ├── cep (VARCHAR(9), NOT NULL)
    ├── complemento (VARCHAR(100))
    ├── numero (VARCHAR(20))
    ├── uf (CHAR(2), NOT NULL)
    └── cidade (VARCHAR(100), NOT NULL)
```

#### Tabela: usuarios
```sql
usuarios
├── id (BIGINT, PK, AUTO_INCREMENT)
├── login (VARCHAR(100), UNIQUE, NOT NULL)
└── senha (VARCHAR(255), NOT NULL)  # BCrypt hash
```

### Especialidades Médicas (Enum)

```java
ORTOPEDIA
CARDIOLOGIA
GINECOLOGIA
DERMATOLOGIA
```

---

## 🔒 Segurança

### Autenticação com JWT

A API implementa autenticação **stateless** baseada em **JSON Web Tokens (JWT)**.

#### Fluxo de Autenticação

```
┌─────────┐                    ┌─────────┐                    ┌──────────┐
│ Cliente │                    │   API   │                    │  Banco   │
└────┬────┘                    └────┬────┘                    └────┬─────┘
     │                              │                              │
     │ 1. POST /login               │                              │
     │ {login, senha}               │                              │
     ├─────────────────────────────>│                              │
     │                              │ 2. Validar credenciais       │
     │                              ├─────────────────────────────>│
     │                              │                              │
     │                              │ 3. Usuário válido            │
     │                              │<─────────────────────────────┤
     │                              │                              │
     │                              │ 4. Gerar JWT Token           │
     │                              │                              │
     │ 5. Retorna token             │                              │
     │<─────────────────────────────┤                              │
     │                              │                              │
     │ 6. GET /medicos              │                              │
     │ Authorization: Bearer {JWT}  │                              │
     ├─────────────────────────────>│                              │
     │                              │ 7. Validar token             │
     │                              │                              │
     │                              │ 8. Buscar dados              │
     │                              ├─────────────────────────────>│
     │                              │                              │
     │                              │ 9. Retornar médicos          │
     │                              │<─────────────────────────────┤
     │ 10. Resposta JSON            │                              │
     │<─────────────────────────────┤                              │
     │                              │                              │
```

### Componentes de Segurança

#### SecurityConfigurations
Configura o Spring Security:
- Desabilita CSRF (API stateless)
- Configura sessões como stateless
- Define endpoints públicos e protegidos
- Registra filtro JWT customizado

#### SecurityFilter
Filtro que intercepta requisições:
- Extrai token JWT do header `Authorization`
- Valida token
- Autentica usuário no contexto do Spring Security

#### TokenService
Gerencia tokens JWT:
- Geração de tokens com expiração
- Validação de tokens
- Extração de informações (subject/login)

### Endpoints Públicos

```
POST /login                    # Autenticação
GET  /hello                    # Endpoint de teste (opcional)
```

### Endpoints Protegidos

Todos os endpoints abaixo requerem **token JWT válido** no header:

```
Authorization: Bearer {seu-token-jwt-aqui}
```

```
# Médicos
POST   /medicos               # Cadastrar médico
GET    /medicos               # Listar médicos (paginado)
GET    /medicos/{id}          # Detalhar médico
PUT    /medicos               # Atualizar médico
DELETE /medicos/{id}          # Inativar médico

# Pacientes
POST   /pacientes             # Cadastrar paciente
GET    /pacientes             # Listar pacientes (paginado)
GET    /pacientes/{id}        # Detalhar paciente
PUT    /pacientes             # Atualizar paciente
DELETE /pacientes/{id}        # Inativar paciente
```

### Configurações de Segurança

- ✅ Senhas criptografadas com **BCrypt**
- ✅ Tokens com expiração configurável
- ✅ Validação automática em todas as requisições
- ✅ Sessões stateless (sem gerenciamento de sessão)
- ✅ CORS configurado para desenvolvimento

---

## 🎯 Boas Práticas Implementadas

### 1️⃣ **Uso de Records (Java 17)**

DTOs implementados como Records, reduzindo boilerplate:

```java
public record DadosCadastroMedico(
    @NotBlank String nome,
    @NotBlank @Email String email,
    @NotBlank String telefone,
    @NotBlank @Pattern(regexp = "\\d{4,6}") String crm,
    @NotNull Especialidade especialidade,
    @NotNull @Valid DadosEndereco endereco
) {}
```

### 2️⃣ **Paginação com Spring Data**

Listagens paginadas para melhor performance:

```java
@GetMapping
public ResponseEntity<Page<DadosListagemMedico>> listar(
    @PageableDefault(size = 10, sort = {"nome"}) Pageable paginacao
) {
    var page = repository.findAllByAtivoTrue(paginacao)
        .map(DadosListagemMedico::new);
    return ResponseEntity.ok(page);
}
```

### 3️⃣ **Bean Validation**

Validações declarativas nos DTOs:

- `@NotBlank` - campo não pode ser nulo ou vazio
- `@NotNull` - campo não pode ser nulo
- `@Email` - validação de formato de e-mail
- `@Pattern` - validação com regex
- `@Valid` - validação em cascata

### 4️⃣ **ResponseEntity**

Retornos HTTP apropriados:

```java
// 201 Created com Location header
ResponseEntity.created(uri).body(dados);

// 200 OK
ResponseEntity.ok(dados);

// 204 No Content
ResponseEntity.noContent().build();
```

### 5️⃣ **Soft Delete**

Exclusão lógica ao invés de física:

```java
@DeleteMapping("/{id}")
@Transactional
public ResponseEntity excluir(@PathVariable Long id) {
    var medico = repository.getReferenceById(id);
    medico.excluir();  // Marca como inativo
    return ResponseEntity.noContent().build();
}
```

### 6️⃣ **Separação de Responsabilidades**

- **Controllers**: Apenas recebem requisições e retornam respostas
- **Repositories**: Apenas acesso a dados
- **Entities**: Lógica de domínio encapsulada
- **DTOs**: Transferência de dados

### 7️⃣ **Tratamento Global de Exceções**

Handler centralizado para exceções:

```java
@RestControllerAdvice
public class TratadorDeErros {
    
    @ExceptionHandler(EntityNotFoundException.class)
    public ResponseEntity tratarErro404() {
        return ResponseEntity.notFound().build();
    }
    
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity tratarErro400(MethodArgumentNotValidException ex) {
        var erros = ex.getFieldErrors();
        return ResponseEntity.badRequest().body(erros.stream()
            .map(DadosErroValidacao::new).toList());
    }
}
```

### 8️⃣ **Flyway Migrations**

Versionamento de banco de dados:
- Scripts SQL versionados
- Execução automática
- Histórico de alterações

---

## 📚 Exemplos de Uso da API

### 1️⃣ Autenticação

```bash
# Request
POST http://localhost:8080/login
Content-Type: application/json

{
  "login": "usuario@email.com",
  "senha": "senha123"
}

# Response
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### 2️⃣ Cadastrar Médico

```bash
# Request
POST http://localhost:8080/medicos
Authorization: Bearer {token}
Content-Type: application/json

{
  "nome": "Dr. João Silva",
  "email": "joao.silva@email.com",
  "telefone": "11987654321",
  "crm": "123456",
  "especialidade": "CARDIOLOGIA",
  "endereco": {
    "logradouro": "Rua das Flores",
    "bairro": "Centro",
    "cep": "12345-678",
    "cidade": "São Paulo",
    "uf": "SP",
    "numero": "100",
    "complemento": "Sala 10"
  }
}

# Response (201 Created)
Location: http://localhost:8080/medicos/1

{
  "id": 1,
  "nome": "Dr. João Silva",
  "email": "joao.silva@email.com",
  "crm": "123456",
  "especialidade": "CARDIOLOGIA",
  "telefone": "11987654321",
  "endereco": {
    "logradouro": "Rua das Flores",
    "bairro": "Centro",
    "cep": "12345-678",
    "cidade": "São Paulo",
    "uf": "SP",
    "numero": "100",
    "complemento": "Sala 10"
  }
}
```

### 3️⃣ Listar Médicos (Paginado)

```bash
# Request
GET http://localhost:8080/medicos?page=0&size=5&sort=nome
Authorization: Bearer {token}

# Response (200 OK)
{
  "content": [
    {
      "id": 1,
      "nome": "Dr. João Silva",
      "email": "joao.silva@email.com",
      "crm": "123456",
      "especialidade": "CARDIOLOGIA"
    }
  ],
  "pageable": {
    "pageNumber": 0,
    "pageSize": 5
  },
  "totalElements": 1,
  "totalPages": 1
}
```

### 4️⃣ Atualizar Médico

```bash
# Request
PUT http://localhost:8080/medicos
Authorization: Bearer {token}
Content-Type: application/json

{
  "id": 1,
  "nome": "Dr. João Silva Souza",
  "telefone": "11999887766",
  "endereco": {
    "logradouro": "Avenida Principal",
    "bairro": "Jardins",
    "cep": "12345-999",
    "cidade": "São Paulo",
    "uf": "SP",
    "numero": "200"
  }
}

# Response (200 OK)
{
  "id": 1,
  "nome": "Dr. João Silva Souza",
  "email": "joao.silva@email.com",
  "crm": "123456",
  "especialidade": "CARDIOLOGIA",
  "telefone": "11999887766",
  "endereco": {
    "logradouro": "Avenida Principal",
    "bairro": "Jardins",
    "cep": "12345-999",
    "cidade": "São Paulo",
    "uf": "SP",
    "numero": "200",
    "complemento": null
  }
}
```

### 5️⃣ Detalhar Médico

```bash
# Request
GET http://localhost:8080/medicos/1
Authorization: Bearer {token}

# Response (200 OK)
{
  "id": 1,
  "nome": "Dr. João Silva",
  "email": "joao.silva@email.com",
  "crm": "123456",
  "especialidade": "CARDIOLOGIA",
  "telefone": "11987654321",
  "endereco": {
    "logradouro": "Rua das Flores",
    "bairro": "Centro",
    "cep": "12345-678",
    "cidade": "São Paulo",
    "uf": "SP",
    "numero": "100",
    "complemento": "Sala 10"
  }
}
```

### 6️⃣ Inativar Médico (Soft Delete)

```bash
# Request
DELETE http://localhost:8080/medicos/1
Authorization: Bearer {token}

# Response (204 No Content)
```

### 7️⃣ Cadastrar Paciente

```bash
# Request
POST http://localhost:8080/pacientes
Authorization: Bearer {token}
Content-Type: application/json

{
  "nome": "Maria Santos",
  "email": "maria.santos@email.com",
  "cpf": "123.456.789-00",
  "telefone": "11988776655",
  "endereco": {
    "logradouro": "Rua das Palmeiras",
    "bairro": "Vila Nova",
    "cep": "98765-432",
    "cidade": "Rio de Janeiro",
    "uf": "RJ",
    "numero": "50"
  }
}

# Response (201 Created)
{
  "id": 1,
  "nome": "Maria Santos",
  "email": "maria.santos@email.com",
  "cpf": "123.456.789-00",
  "telefone": "11988776655"
}
```

---

## 🗺️ Roadmap

### Próximas Funcionalidades

#### Fase 1 - Consultas (Em Breve)
- [ ] Endpoint de agendamento de consultas
- [ ] Endpoint de cancelamento de consultas
- [ ] Validações de regras de negócio:
  - [ ] Horário de funcionamento da clínica
  - [ ] Antecedência mínima para agendamento
  - [ ] Médico disponível no horário
  - [ ] Paciente sem consulta no mesmo dia
  - [ ] Médico sem outra consulta no mesmo horário

#### Fase 2 - Documentação
- [ ] Integração com SpringDoc OpenAPI
- [ ] Documentação Swagger UI
- [ ] Exemplos de requisições
- [ ] Schemas de resposta

#### Fase 3 - Testes
- [ ] Testes unitários de controllers
- [ ] Testes de integração
- [ ] Testes de repositories
- [ ] Testes de segurança

#### Fase 4 - Deploy
- [ ] Profile de produção
- [ ] Dockerfile
- [ ] Docker Compose
- [ ] CI/CD pipeline
- [ ] Monitoramento com Actuator

---

## 🎓 Referências

### Curso Base

**Curso**: Spring Boot 3: documente, teste e prepare uma API para o deploy  
**Plataforma**: [DevMedia](https://www.devmedia.com.br)  
**Instrutor**: Rodrigo Ferreira  
**Escola**: [Alura](https://www.alura.com.br)

### Documentação Oficial

- 📘 **[Spring Boot 3 Documentation](https://docs.spring.io/spring-boot/docs/3.0.x/reference/htmlsingle/)**
- 🔒 **[Spring Security Reference](https://docs.spring.io/spring-security/reference/)**
- 💾 **[Spring Data JPA](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)**
- 🗃️ **[Flyway Documentation](https://flywaydb.org/documentation/)**
- 🔑 **[Auth0 JWT Library](https://github.com/auth0/java-jwt)**
- ☕ **[Java 17 Documentation](https://docs.oracle.com/en/java/javase/17/)**

### Links Úteis

- 🎨 **[Layout Figma](https://www.figma.com/file/N4CgpJqsg7gjbKuDmra3EV/Voll.med)** - Design mobile
- 📋 **[Trello do Projeto](https://trello.com/b/O0lGCsKb/api-voll-med)** - Funcionalidades
- 🔗 **[Spring Boot Guides](https://spring.io/guides)** - Tutoriais oficiais
- 📚 **[Baeldung Spring Tutorials](https://www.baeldung.com/spring-boot)** - Tutoriais avançados

---

## 📄 Licença

Projeto desenvolvido pela [Alura](https://www.alura.com.br) para fins educacionais.

---

## 👨‍💻 Autor

Projeto baseado no curso da **DevMedia**, implementando boas práticas de Spring Boot 3.

---

## 🤝 Contribuindo

Este é um projeto educacional baseado em curso. Contribuições são bem-vindas:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abra um Pull Request

---

## ⚠️ Avisos Importantes

### Spring Boot 3.0.0-M5

Este projeto utiliza uma versão **Milestone (M5)** do Spring Boot 3, que é uma versão de pré-lançamento. 

**Recomendação para produção**: Atualizar para versão stable (3.0.0 ou superior).

### Segurança

- ⚠️ **Não utilize** o secret JWT padrão (`12345678`) em produção
- ⚠️ **Configure** variável de ambiente `JWT_SECRET` com valor seguro
- ⚠️ **Altere** credenciais padrão do MySQL
- ⚠️ **Não commite** senhas ou secrets no repositório

---

## 📞 Suporte

Para dúvidas sobre Spring Boot:
- [Spring Community](https://spring.io/community)
- [Stack Overflow - Spring Boot](https://stackoverflow.com/questions/tagged/spring-boot)

Para dúvidas sobre o curso:
- [DevMedia](https://www.devmedia.com.br)
- [Alura](https://www.alura.com.br)

---

**Desenvolvido com ❤️ usando Spring Boot 3 e boas práticas**
