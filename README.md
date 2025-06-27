# 🔐 API de Autenticação e Autorização JWT – AV2

Este projeto faz parte da AV2 da disciplina de Desenvolvimento de APIs e tem como objetivo demonstrar uma API RESTful completa com autenticação JWT, segurança com Spring Security, documentação Swagger, monitoramento com Prometheus e deploy com Docker.

---

## 🚀 Tecnologias Utilizadas

- Java 17
- Spring Boot 3.x
- Spring Security
- Spring Data JPA
- JWT (JSON Web Token)
- H2 Database (para testes)
- Swagger / OpenAPI
- Docker + Docker Compose
- Spring Actuator + Prometheus
- JUnit e Mockito

---

## 📦 Endpoints principais

| Método | Endpoint           | Descrição                      |
|--------|--------------------|-------------------------------|
| POST   | `/auth/register`   | Registro de novo usuário      |
| POST   | `/auth/login`      | Login e geração do token JWT  |
| GET    | `/produtos`        | Listagem de produtos (seguro) |
| POST   | `/produtos`        | Criação de produto (ADMIN)    |

> A maioria dos endpoints requer **token JWT** no header:  
`Authorization: Bearer <seu_token>`

---

## ⚙️ Configurações

### `application.yml`

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:h2:mem:testdb
    username: sa
    password:
    driver-class-name: org.h2.Driver
  h2:
    console.enabled: true
  jpa:
    hibernate.ddl-auto: update
    show-sql: true

jwt:
  secret: segredosecreto123456
  expiration: 3600000 # 1 hora

management:
  endpoints.web.exposure.include: '*'
🗄️ Usuário Padrão (data.sql)
sql
Copiar
Editar
INSERT INTO users (id, username, password, role)
VALUES (1, 'admin', 'admin123', 'ROLE_ADMIN');
Lembre-se: a senha precisa estar criptografada no ambiente real. Para testes com H2, pode estar em texto plano se não estiver usando BCrypt.

📑 Swagger (Documentação)
Acesse:
🔗 http://localhost:8080/swagger-ui/index.html

📈 Prometheus + Actuator
Acesse métricas em: http://localhost:8080/actuator/prometheus

Verifique saúde em: http://localhost:8080/actuator/health

🐳 Docker
Dockerfile
dockerfile
Copiar
Editar
FROM openjdk:17
COPY . /app
WORKDIR /app
CMD ["java", "-jar", "target/app.jar"]
docker-compose.yml
yaml
Copiar
Editar
version: '3'
services:
  app:
    build: .
    ports:
      - "8080:8080"
✅ Testes
Utilize JUnit 5 + Mockito para testar:

Autenticação

Serviços de domínio (produto, usuário)

👨‍💻 Como rodar localmente
bash
Copiar
Editar
# Clonar o projeto
git clone <repo>

# Rodar com Maven
./mvnw spring-boot:run
Ou via Docker:

bash
Copiar
Editar
docker-compose up --build
🧠 Autor
Desenvolvido por Thales Augusto como parte da AV2 da disciplina de APIs.

