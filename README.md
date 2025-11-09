# ⚕️ Ágata — Gerenciador de Teleconsultas

[![Status do Projeto](https://img.shields.io/badge/Status-Concluído-brightgreen.svg)](https://github.com/seu-repositorio)
[![Licença](https://img.shields.io/badge/Licença-Proprietária-blue.svg)](https://github.com/seu-repositorio)
[![Plataforma Principal](https://img.shields.io/badge/Plataforma-Java%2022%20%7C%20Quarkus-red.svg)]()

> Uma solução **NEXUMTECH** focada em simplificar a telemedicina para pacientes com dificuldades motoras, cognitivas ou tecnológicas — garantindo acesso rápido, acessível e intuitivo às consultas.

---

## 👨‍💻 Informações do Projeto & Equipe

| Categoria | Detalhe |
| :--- | :--- |
| **Instituição / Marca** | NEXUMTECH |
| **Turmas** | 1TDSPY |
| **Local e Ano** | São Paulo, 2025 |

### 👥 Equipe de Desenvolvimento
| Nome | Matrícula |
| :--- | :--- |
| Felipe Ribeiro Salles de Camargo | 565224 |
| Pamella Christiny Chaves Brito | 565206 |

---

## 🎯 Objetivo e Escopo

### 🎯 Objetivo Principal
Reduzir as **barreiras tecnológicas no acesso à saúde**, oferecendo uma plataforma robusta e simplificada que utiliza notificações direcionadas e interações diretas (botão **ENTRAR**) para garantir que o paciente acesse a teleconsulta com segurança, rapidez e sem frustração.

### 📋 Escopo Funcional
O sistema abrange a **gestão completa de agendamentos** e o **controle de interações** com o paciente:

- ✅ **Gestão CRUD** (Create, Read, Update, Delete) de pacientes, médicos e consultas.  
- ⚙️ **Regra de Conflito:** validação de horário para agendamento de consultas.  
- 🔔 **Três Modos de Notificação/Interação:**
  1. **Fixa/Pontual:** acesso direto à sala virtual.  
  2. **Pré-consulta:** direcionamento para sala de espera virtual.  
  3. **Consulta Atrasada:** acesso imediato à sala virtual.

---

## 🛠️ Pilha Tecnológica (Tech Stack)

O projeto foi desenvolvido com **arquitetura em camadas**, utilizando tecnologias modernas e de alto desempenho.

| Categoria | Tecnologia | Versão / Detalhe |
| :--- | :--- | :--- |
| **Linguagem** | Java | JDK 22 |
| **Framework** | Quarkus | 3.x |
| **Banco de Dados** | Oracle | Base Relacional |
| **Conexão** | JDBC | `ojdbc` |
| **Interface (Simulação)** | Java Swing | Teleconsulta Interativa |
| **Datas e Horários** | `java.time` | API nativa Java |

---

## 🌐 Endpoints RESTful (API)

A API está hospedada em:  
`https://teleconsultajava.onrender.com`

### 📡 Recursos e Operações

| Recurso | Método | URI | Descrição | Resposta (Sucesso) | Resposta (Erro / Regra) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Consulta** | `POST` | `/consultas` | Agenda nova consulta | `201 Created` | `409 Conflict`, `500` |
| **Consulta** | `GET` | `/consultas` | Lista todas as consultas | `200 OK` | `404 Not Found` |
| **Consulta** | `DELETE` | `/consultas/{id}` | Exclui consulta por ID | `204 No Content` | `404 Not Found` |
| **Paciente** | `POST` | `/pacientes` | Cadastra novo paciente (CPF único) | `201 Created` | `409 Conflict` |
| **Paciente** | `GET` | `/pacientes/{id}` | Busca paciente por ID | `200 OK` | `404 Not Found` |
| **Paciente** | `PUT` | `/pacientes/{id}` | Atualiza dados do paciente | `200 OK` | `404 Not Found` |
| **Médico** | `POST` | `/medicos` | Adiciona novo médico (CRM único) | `201 Created` | `409 Conflict` |
| **Médico** | `GET` | `/medicos/{crm}` | Busca médico por CRM | `200 OK` | `404 Not Found` |
| **Médico** | `PUT` | `/medicos/{crm}` | Atualiza dados do médico | `200 OK` | `404 Not Found` |

---

## 🚀 Guia de Inicialização

### 🧩 Pré-requisitos

1. **JDK 22** instalado e configurado (`JAVA_HOME` e `PATH`);  
2. Ambiente **Oracle Database** funcional;  
3. **Driver JDBC** (`ojdbc*.jar`) adicionado às dependências;  
4. Schema e scripts SQL executados.

---

### ⚙️ 1. Configuração do Banco de Dados

Edite o arquivo `banco/ConnectionFactory.java` com suas credenciais:

```java
String urlDeConexao = "jdbc:oracle:thin:@<host>:<porta>:<SID>";
String login = "<seu_usuario>";
String senha = "<sua_senha>";
````

---

### ▶️ 2. Importação e Execução

1. Abra o projeto na sua IDE (IntelliJ, Eclipse, VS Code, etc.);
2. Confirme a adição do driver JDBC nas bibliotecas;
3. Execute a classe principal:

   ```bash
   app.Main.java
   ```
4. A interação inicial ocorre via **console (CLI)**, com opções de menu para CRUD.

---

## 🐘 Scripts SQL — Criação do Schema

Execute os comandos abaixo no seu schema Oracle:

```sql
-- SEQUÊNCIAS
CREATE SEQUENCE SEQ_PACIENTE START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;
CREATE SEQUENCE SEQ_CONSULTA START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;

-- TABELA PACIENTE
CREATE TABLE PACIENTE (
    ID NUMBER PRIMARY KEY,
    NOME VARCHAR2(100) NOT NULL,
    CPF VARCHAR2(14) UNIQUE NOT NULL
);

-- TABELA MEDICO
CREATE TABLE MEDICO (
    CRM VARCHAR2(20) PRIMARY KEY,
    NOME_MEDICO VARCHAR2(100) NOT NULL,
    ESPECIALIDADE_MEDICO VARCHAR2(50) NOT NULL
);

-- TABELA CONSULTA
CREATE TABLE CONSULTA (
    ID NUMBER PRIMARY KEY,
    ID_PACIENTE NUMBER NOT NULL,
    CRM_MEDICO VARCHAR2(20) NOT NULL,
    DATA_HORA_CONSULTA TIMESTAMP NOT NULL,
    STATUS VARCHAR2(20) NOT NULL,
    DURACAO NUMBER NOT NULL,
    CONSTRAINT FK_CONSULTA_PACIENTE FOREIGN KEY (ID_PACIENTE) REFERENCES PACIENTE(ID),
    CONSTRAINT FK_CONSULTA_MEDICO FOREIGN KEY (CRM_MEDICO) REFERENCES MEDICO(CRM)
);
```

---

## 🧠 Considerações Finais

O **Ágata – Gerenciador de Teleconsultas** é uma solução desenvolvida para aprimorar a experiência de pacientes e profissionais da saúde em ambientes digitais, reduzindo a complexidade técnica e aumentando a acessibilidade.

> Projeto desenvolvido com 💙 por **NEXUMTECH** — Turma 1TDSPY, FIAP (2025).

``
```
