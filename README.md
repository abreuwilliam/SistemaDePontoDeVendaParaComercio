# Papelaria  - Sistema PDV

Um moderno sistema de Ponto de Venda (PDV) para gerenciamento de estoque, vendas e pedidos. Desenvolvido com **Spring Boot 3.2.5** e **Java 21**, oferecendo uma API REST robusta com segurança baseada em JWT e autenticação via OAuth2.

## 📋 Características Principais

- ✅ **Gerenciamento de Estoque**: Cadastro, consulta e atualização de produtos
- ✅ **Sistema de Pedidos**: Criar, consultar e deletar pedidos
- ✅ **Análise de Vendas**: Relatórios de itens mais/menos vendidos e não vendidos
- ✅ **Autenticação Segura**: JWT com OAuth2 (Google)
- ✅ **Notificações Push**: Integração com Web Push Notifications
- ✅ **Cache de Dados**: Otimização de performance com Spring Cache
- ✅ **Documentação API**: Swagger/OpenAPI integrado
- ✅ **Monitoramento**: Prometheus e actuators do Spring
- ✅ **Validação de Dados**: Hibernated Validator com suporte Jakarta
- ✅ **Email**: Integração com Gmail para notificações

## 🛠️ Stack Tecnológico

### Backend
- **Framework**: Spring Boot 3.2.5
- **Java**: OpenJDK 21
- **Build**: Maven 3.x
- **Segurança**: Spring Security + JWT (jjwt 0.11.5)
- **Banco de Dados**: H2 Database (em memória)
- **ORM**: JPA/Hibernate

### Dependências Principais
- `spring-boot-starter-data-jpa` - Persistência de dados
- `spring-boot-starter-security` - Autenticação e autorização
- `spring-boot-starter-web` - API web
- `spring-boot-starter-cache` - Caching
- `springdoc-openapi-starter-webmvc-ui` - Documentação Swagger
- `spring-boot-starter-actuator` - Endpoints de monitoramento
- Lombok - Redução de boilerplate

### Frontend
- HTML5
- CSS3
- JavaScript (Vanilla)
- Service Workers (PWA support)

## 📁 Estrutura do Projeto

```
projeto-completo/
├── src/
│   ├── main/
│   │   ├── java/com/pdv/papelaria/
│   │   │   ├── PdvApplication.java          # Classe principal
│   │   │   ├── aop/                         # Aspect Oriented Programming
│   │   │   ├── autenticacao/                # Módulo de autenticação
│   │   │   ├── config/                      # Configurações da aplicação
│   │   │   ├── controller/                  # Controladores REST
│   │   │   │   ├── AuthController.java
│   │   │   │   ├── ProdutoController.java
│   │   │   │   ├── PedidoController.java
│   │   │   │   ├── ItemMaisVendidoController.java
│   │   │   │   ├── ItemMenosVendidoController.java
│   │   │   │   └── ...
│   │   │   ├── dto/                         # Data Transfer Objects
│   │   │   ├── entities/                    # Entidades JPA
│   │   │   │   ├── Usuario.java
│   │   │   │   ├── Produto.java
│   │   │   │   ├── Pedidos.java
│   │   │   │   ├── Venda.java
│   │   │   │   └── ItemVenda.java
│   │   │   ├── exception/                   # Exceções customizadas
│   │   │   ├── repository/                  # Repositórios JPA
│   │   │   └── service/                     # Lógica de negócio
│   │   └── resources/
│   │       ├── application.properties
│   │       ├── application-qa.properties
│   │       ├── application-test.properties
│   │       ├── schema.sql                   # DDL do banco
│   │       ├── data.sql                     # Dados iniciais
│   │       ├── logback-spring.xml           # Configuração de logs
│   │       └── static/                      # Frontend assets
│   │           ├── index.html
│   │           ├── caixa.html
│   │           ├── cadastrarproduto.html
│   │           ├── consultaproduto.html
│   │           ├── style.css
│   │           ├── script.js
│   │           └── ...
│   └── test/
│       └── java/com/pdv/                    # Testes unitários
├── pom.xml                                  # Configuração Maven
├── prometheus.yml                           # Configuração Prometheus
├── sonar-project.properties                 # Configuração SonarQube
└── README.md
```


## 🚀 Como Executar

### Pré-requisitos
- Java 21+ instalado
- Maven 3.6+ instalado
- Git (opcional)

### Instalação e Execução

1. **Clone o repositório** (se aplicável)
```bash
git clone https://github.com/abreuwilliam/SistemaDePontoDeVendaParaComercio.git
cd projeto-completo
```

2. **Compile e execute com Maven**
```bash
# Com mvnw (Maven Wrapper)
./mvnw clean install
./mvnw spring-boot:run

# Ou com Maven instalado globalmente
mvn clean install
mvn spring-boot:run
```

3. **Acesse a aplicação**
- **API REST**: http://localhost:8080
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **OpenAPI JSON**: http://localhost:8080/v3/api-docs
- **Prometheus Metrics**: http://localhost:8080/actuator/prometheus
- **Health Check**: http://localhost:8080/actuator/health

### Variáveis de Ambiente (Recomendado)
```bash
# CORS Origins
export CORS_ORIGINS=http://localhost:5173,http://localhost:3000

# Você pode sobrescrever em profiless específicos
```

## 🔐 Autenticação e Segurança

### JWT (JSON Web Token)
- **Chave Secreta**: HS512 (mínimo 64 caracteres)
- **Tempo de Expiração**: 86400000ms (24 horas)
- **Header**: `Authorization: Bearer <token>`

### OAuth2 - Google
- **Client ID**: Seu ID do Google Cloud
- **Redirect URI**: `http://localhost:8080/login/oauth2/code/google`

### Roles de Usuário
- `ADMIN` - Acesso total ao sistema
- `USER` - Acesso restrito (consultas básicas)

## 📡 Endpoints Principais da API

### Autenticação
```
POST   /login              - Login com JWT
POST   /login/oauth2/code/google - OAuth2 Google
POST   /logout             - Logout
```

### Produtos
```
GET    /produto/{codigoProduto}     - Buscar produto por código
POST   /produto/caixa               - Operações de caixa
GET    /produto                     - Listar produtos
POST   /produto                     - Criar produto
PUT    /produto/{id}                - Atualizar produto
DELETE /produto/{id}                - Deletar produto
```

### Pedidos
```
POST   /pedidos                    - Criar pedido
GET    /pedidos                    - Listar pedidos
DELETE /pedidos                    - Deletar todos os pedidos
```

### Análises
```
GET    /item-mais-vendido          - Itens mais vendidos
GET    /item-menos-vendido         - Itens menos vendidos
GET    /item-nao-vendido           - Itens não vendidos
```

### Push Notifications
```
POST   /push/subscribe              - Inscrever em notificações
POST   /push/send                   - Enviar notificação push
```

## 📊 Monitoramento e Observabilidade

### Prometheus
- **Endpoint**: `/actuator/prometheus`
- **Métricas**: CPU, Memória, JVM, HTTP requests
- **Arquivo de config**: `prometheus.yml`

### Actuator Endpoints
```
GET /:8080/actuator/health    - Status da aplicação
GET /:8080/actuator/info      - Informações da aplicação
GET /:8080/actuator/prometheus - Métricas Prometheus
```

## 📧 Integração de Email

A aplicação está configurada para enviar emails via **Gmail SMTP**:
- **Host**: smtp.gmail.com
- **Porta**: 587
- **Autenticação**: Habilitada (TLS)
- **Email**: seu_email

> ⚠️ **Nota**: Use senhas de aplicação (App Passwords) do Gmail em produção, não sua senha regular.

## 🔔 Web Push Notifications

A aplicação suporta Web Push com VAPID:
- **Public Key**: Configurada em `application.properties`
- **Private Key**: Configurada em `application.properties`
- **Service Worker**: `service-worker.js` no frontend

## 🧪 Testes

A aplicação inclui testes unitários e de integração usando JUnit + Spring Test.

```bash
# Executar todos os testes
./mvnw test

# Executar com cobertura Jacoco
./mvnw clean test jacoco:report
```

### Arquivos de Teste
- `ControllerTest.java` - Testes dos controladores
- `UsuarioServiceTest.java` - Testes do serviço de usuário
- `ProjetoCompletoApplicationTests.java` - Testes de contexto

**Cobertura Jacoco**: Disponível em `target/site/jacoco/index.html`

## ⚙️ Perfis de Execução

A aplicação suporta múltiplos perfis:

- **qa** (padrão): Configuração para QA
- **test**: Configuração para testes
- Altere em `application.properties`: `spring.profiles.active=qa`

## 📝 Logs

- **Level**: DEBUG para Hibernate SQL, INFO para Spring Security
- **Formato**: Configurado em `logback-spring.xml`
- **Output**: Console + arquivo (se configurado)

## 🤝 Contribuindo

1. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
2. Submeta suas mudanças (`git commit -am 'Add some AmazingFeature'`)
3. Push para a branch (`git push origin feature/AmazingFeature`)
4. Abra um Pull Request

## 📄 Licença

Este projeto está licenciado sob a MIT License - veja o arquivo LICENSE para detalhes.

## 👤 Autor

**William Abreu**

## 📞 Suporte

Para dúvidas ou problemas, entre em contato ou abra uma issue no repositório.

---

**Última atualização**: Abril 2026
