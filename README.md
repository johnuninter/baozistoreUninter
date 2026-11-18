# BaoziStore — API REST

API REST desenvolvida como Atividade Prática da disciplina de Desenvolvimento Web Back-End.

- Aluno: John Michael Faria
- RU: 4607264
- Curso: Análise e Desenvolvimento de Sistemas
- Instituição: Centro Universitário Internacional UNINTER

# Sobre o projeto

A BaoziStore representa uma pequena loja de pão chinês — baozi. O sistema foi criado para exercitar a 
construção de uma API REST com Java, Spring Boot, Spring Data JPA, banco de dados relacional e testes utilizando Postman.

# Objetivo do projeto

A API permite controlar três tipos principais de informação:

- clientes;
- produtos;
- pedidos.

Um pedido representa a compra de um único produto por um cliente, em determinada quantidade.

# Tecnologias utilizadas

- Java 17
- Spring Boot 3.2.0
- Spring Web MVC (spring-boot-starter-web)
- Spring Data JPA
- Hibernate (mapeamento objeto-relacional)
- H2 Database (banco embarcado em modo arquivo)
- Maven (com Maven Wrapper incluído)
- Postman para testes das requisições HTTP

O projeto utiliza o padrão MVC do Spring e está organizado nos seguintes pacotes:

```
src/main/java/com/example/baozistore/
├── controller/
├── model/
└── repository/
```

# Estrutura do projeto

```
baozistore/
├── data/
│   └── BD_BAOZI.mv.db
├── src/
│   ├── main/
│   │   ├── java/com/example/baozistore/
│   │   │   ├── BaozistoreApplication.java
│   │   │   ├── controller/
│   │   │   │   ├── ClienteController.java
│   │   │   │   ├── PedidoController.java
│   │   │   │   └── ProdutoController.java
│   │   │   ├── model/
│   │   │   │   ├── Cliente.java
│   │   │   │   ├── Pedido.java
│   │   │   │   └── Produto.java
│   │   │   └── repository/
│   │   │       ├── ClienteRepository.java
│   │   │       ├── PedidoRepository.java
│   │   │       └── ProdutoRepository.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/com/example/baozistore/
│           └── BaozistoreApplicationTests.java
├── pom.xml
└── mvnw
```

# Entidades

# Cliente

| Campo        | Tipo         | Descrição       				                        |
|------------- |--------------|------------------------------------------------ |
| id           | Long         | Identificador gerado automaticamente 	          |    
| nome         | String       | Nome do cliente 				                        |
| clienteDesde | LocalDate    | Data de cadastro do cliente 			              |

# Produto

| Campo 	  | Tipo 		    | Descrição 						                          |
|---------- |------------ |------------------------------------------------ |
| id 		    | Long 		    | Identificador gerado automaticamente 		        |
| nome 		  | String 	    | Nome do produto 					                      |
| preco 	  | BigDecimal 	| Preço do produto 					                      |
| estoque 	| Boolean 	  | Indica se o produto está disponível em estoque 	|

# Pedido
	
| Campo 	    | Tipo	 	    | Descrição 						                          |
|------------ |------------ |------------------------------------------------ |
| id 		      | Long 		    | Identificador gerado automaticamente 		        |
| clienteId 	| Long 		    | Identificador do cliente que realizou o pedido 	|
| produtoId 	| Long 		    | Identificador do produto comprado 			        |
| quantidade 	| Integer 	  | Quantidade comprada 				                    |

Na versão atual, Pedido armazena clienteId e produtoId como valores Long. A validação da existência do cliente 
e do produto ainda não está implementada na camada de serviço.

# Endpoints

A aplicação expõe os endpoints abaixo. As respostas e requisições utilizam JSON.

# Clientes

| Método 	| Endpoint 		    | Descrição 			          |
|---------|-----------------|--------------------------	|
| POST 		| /clientes 		  | Cadastrar cliente 		    |
| GET 		| /clientes 		  | Listar todos os clientes 	|
| GET 		| /clientes/{id} 	| Consultar cliente por ID 	|
| DELETE 	| /clientes/{id} 	| Excluir cliente 		      |

# Produtos
	
| Método 	| Endpoint 		    | Descrição 			          |
|---------|-----------------|--------------------------	|
| POST 		| /produtos 		  | Cadastrar produto 		    |
| GET 		| /produtos 		  | Listar todos os produtos 	|
| GET 		| /produtos/{id} 	| Consultar produto por ID 	|
| DELETE 	| /produtos/{id} 	| Excluir produto 		      |

# Pedidos

| Método 	| Endpoint 		    | Descrição 			          |
|---------|-----------------|--------------------------	|
| POST 		| /pedidos 		    | Registrar pedido 		      |
| GET 		| /pedidos 		    | Listar todos os pedidos 	|
| GET 		| /pedidos/{id} 	| Consultar pedido por ID 	|
| DELETE 	| /pedidos/{id} 	| Excluir pedido 		        |

# Como executar o projeto

# Pré-requisitos

- JDK 17 instalado (Eclipse Temurin recomendado)
- Variável de ambiente JAVA_HOME apontando para o JDK 17
- Não é necessário instalar Maven: o projeto inclui o Maven Wrapper
- Postman, caso queira repetir os testes da atividade

O `pom.xml` deste projeto está configurado com `<java.version>17</java.version>`.

# Verificar o JAVA_HOME

No Windows, no Prompt de Comando:

```
echo %JAVA_HOME%
java -version
javac -version
```

Se o comando `javac` não for reconhecido, o JAVA_HOME provavelmente aponta para um JRE em vez de um JDK.

Para definir temporariamente no terminal atual:

```
set JAVA_HOME=C:\caminho\do\jdk-17
```

# Executar com Maven Wrapper no Windows

```
.\mvnw spring-boot:run
```

Alternativa equivalente:

```
mvnw.cmd spring-boot:run
```

# Executar com Maven Wrapper no Linux ou macOS

```
chmod +x mvnw
./mvnw spring-boot:run
```

# Recompilação limpa

Caso o projeto tenha passado por mudanças no `pom.xml`:

```
.\mvnw clean
.\mvnw spring-boot:run
```

Quando a aplicação iniciar corretamente, a API ficará disponível em:

```
http://localhost:8080
```

Saída esperada no console:

```
Tomcat started on port 8080 (http)
Started BaozistoreApplication in X.XXX seconds
```

# Executar os testes

Windows:

```
.\mvnw test
```

Linux ou macOS:

```
./mvnw test
```

# Exemplos para o Postman

Configure o cabeçalho abaixo nas requisições POST:

```
Content-Type: application/json
```

# 1. Cadastrar cliente

```
POST http://localhost:8080/clientes
```

Corpo:

```
{
  "nome": "JOHN MICHAEL FARIA 4607264",
  "clienteDesde": "2026-11-16"
}
```

O nome deve ser ajustado para o nome do aluno seguido do RU, conforme a orientação da atividade.

# 2. Cadastrar produto

```
POST http://localhost:8080/produtos
```

Corpo:

```
{
  "nome": "Baozi de carne",
  "preco": 8.50,
  "estoque": true
}
```

# 3. Cadastrar pedido

Utilize os IDs retornados pelas requisições de cadastro do cliente e do produto.

```
POST http://localhost:8080/pedidos
```

Corpo:

```
{
  "clienteId": 1,
  "produtoId": 1,
  "quantidade": 2
}
```

# 4. Consultar registros

```
GET http://localhost:8080/clientes
GET http://localhost:8080/clientes/1
GET http://localhost:8080/produtos
GET http://localhost:8080/produtos/1
GET http://localhost:8080/pedidos
GET http://localhost:8080/pedidos/1
```

# 5. Excluir registros

```
DELETE http://localhost:8080/clientes/1
DELETE http://localhost:8080/produtos/1
DELETE http://localhost:8080/pedidos/1
```

Para os prints da atividade, é recomendado registrar no Postman as operações de criação, listagem, 
consulta por ID e exclusão. Os dados utilizados nos prints devem ser os mesmos apresentados na descrição 
da situação fictícia.

# Banco de dados H2

A aplicação está configurada para utilizar um banco H2 em arquivo:

```
spring.datasource.url=jdbc:h2:file:./data/BD_BAOZI
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=john
spring.datasource.password=1234
```

A criação e atualização das tabelas são controladas pela propriedade:

```
spring.jpa.hibernate.ddl-auto=update
```

O console web do H2 está configurado em:

```
http://localhost:8080/h2-console
```

Para acessar o banco pelo console H2, utilize os mesmos dados configurados em `application.properties`:

| Campo 		    | Valor 				                |
|---------------|-------------------------------|
| Driver Class 	| org.h2.Driver 			          |
| JDBC URL 		  | jdbc:h2:file:./data/BD_BAOZI 	|
| User Name 		| john 					                |
| Password 		  | 1234 					                |

O console H2 é habilitado automaticamente pela auto-configuração do Spring Boot, a partir das propriedades
`spring.h2.console.enabled=true` e `spring.h2.console.path=/h2-console`. Não é necessária nenhuma classe de 
configuração adicional.

O console H2 e as credenciais estão configurados para estudo local. Essa configuração não deve ser utilizada 
dessa forma em um ambiente de produção.

# Limitações atuais

A versão atual foi feita para o escopo básico da atividade. Ela ainda não possui:

- autenticação e autorização;
- camada de serviço;
- validação de cliente e produto ao registrar pedido;
- validação de estoque ou quantidade positiva;
- atualização com PUT ou PATCH;
- status do pedido;
- relacionamento JPA entre as entidades;
- cálculo de valor total;
- interface web própria.

# Possíveis melhorias

Como evolução do projeto, podem ser adicionados:

- uma camada service para as regras de negócio;
- validações com Bean Validation;
- relacionamentos JPA entre pedido, cliente e produto;
- controle de quantidade real do estoque;
- atualização de registros com PUT;
- tratamento padronizado de erros;
- autenticação e perfis de acesso;
- testes unitários e testes de integração;
- documentação com OpenAPI/Swagger.

# Licença

Projeto acadêmico desenvolvido para fins de estudo.


