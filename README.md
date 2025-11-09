Claro\! Com base nas informações fornecidas sobre o projeto **Ágata — Gerenciador de Teleconsultas**, organizei um `README.md` completo, claro e otimizado para que você possa copiar e colar.

Este formato utiliza Markdown para melhor leitura e inclui todas as seções necessárias:

````markdown
# 🏥 Ágata — Gerenciador de Teleconsultas (NEXUMTECH)

O **Ágata** é uma solução que visa simplificar o acesso à telemedicina para pacientes com limitações (motoras, cognitivas ou dificuldades tecnológicas). Em vez de depender de sistemas complexos, o Ágata oferece interações intuitivas (como o botão **ENTRAR**), notificações direcionadas e um fluxo seguro e robusto para gerenciar agendamentos e iniciar teleconsultas.

| Informação | Detalhe |
| :--- | :--- |
| **Instituição / Marca** | NEXUMTECH |
| **Local e Ano** | São Paulo, 2025 |
| **Turmas** | 1TDSPY |
| **Equipe** | Felipe Ribeiro Salles de Camargo (565224), Pamella Christiny Chaves Brito (565206) |

---

## 🎯 Objetivo e Escopo

### Objetivo
Reduzir barreiras, orientar o paciente com interações intuitivas (botões **ENTRAR**) e garantir que o fluxo de agendamento/entrada na teleconsulta seja simples, seguro e robusto.

### Escopo
* Gestão de pacientes, médicos e consultas.
* Agendamento de consultas com verificação de conflitos de horário.
* **Notificações** para três tipos de interação: fixa/pontual, pré-consulta (sala de espera) e consulta atrasada.
* Interface CLI (Linha de Comando) para administração.
* Componente de simulação de teleconsulta via **Java Swing**.

---

## 💻 Tecnologias e Dependências

| Categoria | Detalhes |
| :--- | :--- |
| **Linguagem Principal** | Java (JDK 22) |
| **Banco de Dados** | Oracle |
| **APIs / Frameworks** | JDBC (com Oracle), Java Swing, `java.time` |
| **IDE** | IntelliJ IDEA (Recomendado) |

---

## 🌐 Endpoints da API REST (Quarkus)

A API está servida em: `https://teleconsultajava.onrender.com`

| Recurso | Método | URI | Descrição | Sucesso | Erro / Regra |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Consulta** | `POST` | `/consultas` | Agenda nova consulta (verifica conflito) | `201 Created` | `409 Conflict`, `500` |
| **Consulta** | `GET` | `/consultas` | Lista de todas as consultas agendadas | `200 OK` | `404 Not Found` |
| **Consulta** | `DELETE` | `/consultas/{id}` | Cancelar/excluir consulta por ID | `204 No Content` | `404 Not Found` |
| **Paciente** | `POST` | `/pacientes` | Adicionado novo paciente (CPF único) | `201 Created` | `409 Conflict` |
| **Paciente** | `GET` | `/pacientes/{id}` | Busca paciente por ID | `200 OK` | `404 Not Found` |
| **Paciente** | `PUT` | `/pacientes/{id}` | Atualizar todos os dados do paciente | `200 OK` | `404 Not Found` |
| **Paciente** | `DELETE` | `/pacientes/{id}` | Remover paciente pelo ID | `204 No Content` | `404 Not Found` |
| **Médico** | `POST` | `/medicos` | Adicionado novo médico (CRM único) | `201 Created` | `409 Conflict` |
| **Médico** | `GET` | `/medicos` | Lista todos os médicos | `200 OK` | `404 Not Found` |
| **Médico** | `GET` | `/medicos/{crm}` | Busca médico pelo CRM | `200 OK` | `404 Not Found` |
| **Médico** | `PUT` | `/medicos/{crm}` | Atualizar dados do médico pelo CRM | `200 OK` | `404 Not Found` |
| **Médico** | `DELETE` | `/medicos/{crm}` | Remover médico pelo CRM | `204 No Content` | `404 Not Found` |

---

## ⚙️ Guia de Execução (Passo a Passo)

### 1) Pré-requisitos
1.  **JDK 22** instalado e variáveis de ambiente (`JAVA_HOME`/`PATH`) configuradas.
2.  Banco de dados **Oracle** acessível.
3.  **Driver JDBC** (`ojdbc*.jar`) obtido e adicionado ao *classpath* do projeto na IDE.
4.  Execute os scripts SQL para criar o esquema (vide seção abaixo).

### 2) Configuração do Banco de Dados (Oracle JDBC)
No arquivo `banco/ConnectionFactory.java`, configure os detalhes da sua conexão:

```java
String urlDeConexao = "jdbc:oracle:thin:@<host>:<porta>:<SID>";
String login = "<seu_usuario>";
String senha = "<sua_senha>";
````

### 3\) Importação na IDE

1.  Abra a sua IDE (IntelliJ recomendado).
2.  **Arquivo \> Abrir** e selecione a pasta raiz do projeto (`Ágata`).
3.  Verifique se a pasta `src` está marcada como **Source Root**.
4.  Adicione o JAR do driver JDBC às bibliotecas do projeto (Módulo Libraries).

### 4\) Rodar a Aplicação

1.  Abra a classe principal: `app.Main.java`.
2.  Execute a classe (`Run`).
3.  A interação principal do sistema administrativo é feita via **console (menu)**.

-----

## 🐘 Scripts SQL (Criação do Esquema)

Copie e execute estes scripts SQL no seu esquema Oracle:

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
