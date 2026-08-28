# 🔌 Minhas APIs

Repositório com as APIs REST desenvolvidas em **Java + Spring Boot**, cada uma consumindo ou expondo dados de diferentes serviços externos.

---

## 📋 Índice

- [Sobre o repositório](#-sobre-o-repositório)
- [APIs disponíveis](#-apis-disponíveis)
- [Tecnologias](#-tecnologias)
- [Pré-requisitos](#-pré-requisitos)
- [Como rodar cada projeto](#-como-rodar-cada-projeto)
- [Estrutura do repositório](#-estrutura-do-repositório)

---

## 📖 Sobre o repositório

Este repositório reúne diferentes APIs desenvolvidas como projetos de estudo, cada uma em sua própria pasta, com `pom.xml` e `README.md` próprios.

---

## 🚀 APIs disponíveis

| Projeto | Descrição | Fonte externa consumida |
|---------|-----------|--------------------------|
| [`ClimaAPI`](./ClimaAPI) | Consulta o clima atual de uma cidade pelo nome | [WeatherAPI.com](https://www.weatherapi.com/) |
| [`FipeAPI`](./FipeAPI) | Consulta marcas, modelos, anos e valores da Tabela FIPE | [FIPE API (Parallelum)](https://fipe.parallelum.com.br/) |

> ✏️ **Adicione novas linhas** aqui conforme criar mais APIs no repositório.

---

## 🛠️ Tecnologias

- Java 17+
- Spring Boot
- Spring Web (`RestTemplate` / `@RestController`)
- Maven
- Consumo de APIs REST externas

---

## ✅ Pré-requisitos

- [Java JDK 17+](https://adoptium.net/)
- [Maven](https://maven.apache.org/download.cgi)
- Para o `ClimaAPI`: uma chave de API gratuita da [WeatherAPI.com](https://www.weatherapi.com/signup.aspx) (veja o `.env` no README do próprio projeto)

---

## ▶️ Como rodar cada projeto

Cada API é independente e roda separadamente. Entre na pasta do projeto desejado e siga as instruções do `README.md` local:

```bash
cd ClimaAPI
mvn spring-boot:run
```

ou

```bash
cd FipeAPI
mvn spring-boot:run
```

> 💡 Por padrão, todos sobem na porta `8080`. Rode apenas uma API por vez, ou configure `server.port` de forma diferente em cada `application.properties` se quiser rodar mais de uma simultaneamente.

---

## 🗂️ Estrutura do repositório

```
minhas-apis/
├── ClimaAPI/
│   ├── src/
│   ├── pom.xml
│   └── README.md
├── FipeAPI/
│   ├── src/
│   ├── pom.xml
│   └── README.md
└── README.md   <- este arquivo
```

> ✏️ **Atualize esta árvore** conforme adicionar novos projetos de API ao repositório.

---

## 📄 Licença

Repositório de uso pessoal, para fins de estudo e portfólio.
