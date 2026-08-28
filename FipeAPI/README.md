# 🚗 FipeAPI

API REST em **Java + Spring Boot** que consulta a Tabela FIPE (marcas, modelos, anos e valores de veículos), usando a [API pública da FIPE (Parallelum)](https://fipe.parallelum.com.br/).

---

## 📋 Índice

- [Sobre o projeto](#-sobre-o-projeto)
- [Tecnologias](#-tecnologias)
- [Pré-requisitos](#-pré-requisitos)
- [Como rodar](#-como-rodar)
- [Endpoints](#-endpoints)
- [Exemplo de uso](#-exemplo-de-uso)
- [Estrutura do projeto](#-estrutura-do-projeto)
- [Erros comuns](#-erros-comuns)

---

## 📖 Sobre o projeto

O **FipeAPI** é um serviço backend que atua como *proxy* para a API da Tabela FIPE, permitindo consultar:

- Marcas de veículos disponíveis
- Modelos de uma marca
- Anos disponíveis de um modelo
- Valor de mercado (FIPE) de um veículo específico

Ele consome a API pública `https://fipe.parallelum.com.br/api/v2` e repassa os dados para quem chamar o FipeAPI.

---

## 🛠️ Tecnologias

- Java 17+
- Spring Boot
- Spring Web (`RestTemplate`, `@RestController`)
- Maven

---

## ✅ Pré-requisitos

- [Java JDK 17+](https://adoptium.net/)
- [Maven](https://maven.apache.org/download.cgi)
- Conexão com a internet (a API FIPE é pública, não precisa de chave)

---

## ▶️ Como rodar

### 1. Clone o repositório

```bash
git clone <url-do-seu-repositorio>
cd FipeAPI
```

### 2. Rode com Maven

```bash
mvn spring-boot:run
```

A aplicação sobe por padrão em:

```
http://localhost:8080
```

### 3. Ou gere o `.jar` e rode direto

```bash
mvn clean package -DskipTests
java -jar target/FipeAPI-0.0.1-SNAPSHOT.jar
```

> 💡 Se a porta `8080` já estiver em uso: `kill -9 $(lsof -t -i :8080)` ou defina `server.port=8081` no `application.properties`.

---

## 🔗 Endpoints

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET`  | `/marcas` | Lista todas as marcas de veículos disponíveis |
| `GET`  | `/modelos/{marca}` | Lista os modelos de uma marca (`marca` = código numérico) |
| `GET`  | `/anos/{marca}/{modelo}` | Lista os anos disponíveis de um modelo |
| `GET`  | `/valor/{marca}/{modelo}/{ano}` | Retorna o valor FIPE do veículo no ano informado |

---

## 💡 Exemplo de uso

**1. Buscar marcas:**
```bash
curl http://localhost:8080/marcas
```

**2. Buscar modelos da marca (ex: código `59`):**
```bash
curl http://localhost:8080/modelos/59
```

**3. Buscar anos disponíveis de um modelo:**
```bash
curl http://localhost:8080/anos/59/5940
```

**4. Buscar o valor FIPE de um veículo:**
```bash
curl http://localhost:8080/valor/59/5940/2020-1
```

### Exemplo de resposta (valor)

```json
{
  "brand": "Fiat",
  "model": "Uno Mille EP/ EPS 1.0",
  "modelYear": 2020,
  "fuel": "Álcool",
  "codeFipe": "001004-9",
  "price": "R$ 32.500,00",
  "fuelAcronym": "A"
}
```

---

## 🗂️ Estrutura do projeto

```
FipeAPI/
├── src/
│   └── main/
│       ├── java/com/example/FipeAPI/
│       │   ├── FipeApiApplication.java
│       │   ├── controller/
│       │   │   └── Controller.java
│       │   └── service/
│       │       └── Servico.java
│       └── resources/
│           └── application.properties
├── test/java/com/example/FipeAPI/
│   └── FipeApiApplicationTests.java
├── pom.xml
└── README.md
```

---

## 🩹 Erros comuns

| Erro | Causa provável | Solução |
|------|------------------|---------|
| `Port 8080 already in use` | Outra instância da aplicação já está rodando | `kill -9 $(lsof -t -i :8080)` ou troque a porta |
| Resposta vazia ou 404 no endpoint `/anos` | Código de marca/modelo inválido | Confirme os códigos retornados por `/marcas` e `/modelos/{marca}` antes de consultar os anos |
| `Falha ao obter dados. Código de Status ...` | A API da FIPE está fora do ar ou o parâmetro enviado está incorreto | Verifique se os parâmetros de marca, modelo e ano batem com os IDs retornados pelos endpoints anteriores |

> ⚠️ **Nota:** no método `consultarAnos` do `Servico.java`, a concatenação da URL está sem as barras `/` entre `brands`, o ID da marca e `years` (ficou `"/cars/brandas"+marca+"/models/"+modelo+"years"`). Vale revisar essa linha para o endpoint `/anos` funcionar corretamente — o correto seria algo como `BASE_URL + "/cars/brands/" + marca + "/models/" + modelo + "/years"`.

---

## 📄 Licença

Este projeto é de uso livre para fins de estudo.
