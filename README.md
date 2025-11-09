Ágata —
Identificação do Projeto e Equipe
Projeto: Ágata — Gerenciador de Teleconsultas
Instituição / Marca: NEXUMTECH
Turmas: 1TDSPY
Felipe Ribeiro Salles de Camargo - 565224 Pamella Christiny Chaves Brito - 565206
Local e Ano: São Paulo, 2025
Objetivo e Escopo do Projeto
O Ágata é uma solução que facilita o acesso à telemedicina para pacientes com limitações motoras, cognitivas ou dificuldades no uso de tecnologia. Em vez de forçar o paciente a navegar por sistemas complexos, o Ágata oferece notificações e atalhos diretos para que o usuário entre rapidamente nas salas de teleconsulta ou salas de espera.

O foco principal é: reduzir barreiras, orientar o paciente com interações intuitivas (botões ENTRAR) e garantir que o fluxo de agendamento/entrada na teleconsulta seja simples, seguro e robusto.

Escopo
Gestão de pacientes, médicos e consultas.
Agendamento de consultas com verificação de conflitos.
Notificações para três tipos de interação: fixa/pontual, pré-consulta e consulta atrasada.
Interface CLI para administração e um componente de simulação de teleconsulta via Swing.
Descrição das Funções
Há três modos de notificação/interação:

Processo de notificação fixa e pontual

Notificação com botão ENTRAR que leva diretamente à sala virtual da teleconsulta.
Processo de notificação pré-consulta

Notificação com botão ENTRAR que leva para a sala de espera virtual (aguarda liberação pelo profissional).
Processo de notificação de consulta atrasada

Notificação com botão ENTRAR que leva para a sala virtual — usada quando uma consulta já começou, mas o paciente está atrasado.
Cada fluxo tem regras de negócio específicas (validações de horário, estado da consulta, duração e atualização de status).

Pontos de extremidade (API REST)
https://teleconsultajava.onrender.com

A seguir, a tabela resumida com os recursos expostos pela API e os códigos de resposta esperados.

Recurso	Método HTTP	URI	Descrição	Sucesso	Erro / Regra de to
Consulta	PUBLICAR	/consultas	Agenda nova consulta (verifica conflito)	201 Created	409 Conflict,500
Consulta	PEGAR	/consultas	Lista de todas as consultas agendadas	200 OK	404 Not Found
Consulta	EXCLUIR	/consultas/{id}	Cancelar/excluir consulta por ID	204 No Content	404 Not Found
Paciente	PUBLICAR	/pacientes	Adicionado novo paciente (CPF único)	201 Created	409 Conflict
Paciente	PEGAR	/pacientes/{id}	Busca paciente por ID	200 OK	404 Not Found
Paciente	COLOCAR	/pacientes/{id}	Atualizar todos os dados do paciente	200 OK	404 Not Found
Paciente	EXCLUIR	/pacientes/{id}	Remover paciente pelo ID	204 No Content	404 Not Found
Médico	PUBLICAR	/medicos	Adicionado novo médico (CRM único)	201 Created	409 Conflict
Médico	PEGAR	/medicos	Lista todos os médicos	200 OK	404 Not Found
Médico	PEGAR	/medicos/{crm}	Busca médico pelo CRM	200 OK	404 Not Found
Médico	COLOCAR	/medicos/{crm}	Atualizar dados do médico pelo CRM	200 OK	404 Not Found
Médico	EXCLUIR	/medicos/{crm}	Remover médico pelo CRM	204 No Content	404 Not Found
Observação: ajuste as URIs caso a aplicação esteja servida em contexto (ex.: /api/v1/consultas).

Modelo de Dados (MER) e UML
MER (Diagrama de Entidade-Relacionamento): contempla as tabelas PACIENTE, MEDICOe CONSULTAcom as chaves estrangeiras e restrições indicadas no script SQL.
UML (Diagrama de Classes): incluindo classes como Paciente, Medico, Consulta, DAOs ( PacienteDAO, MedicoDAO, ConsultaDAO), ConsultaService(regras de negócio) e ConnectionFactory.
Observação: aqui no repositório adicionei as imagens/exportações dos diagramas (por exemplo, docs/mer.pnge docs/uml.png).

Ferramentas, Linguagens e Bibliotecas
Linguagens e Plataformas

Java (principal)
Banco de dados Oracle (base relacional)
Bibliotecas / APIs

JDBC (com Oracle)
Java Swing (simulação de interface para iniciar consulta)
java.time(manipulação de dados/horas)
java.sql.Timestamp(interação com tipos SQL)
IDE / Ferramenta de Desenvolvimento

IntelliJ IDEA (recomendado), Eclipse ou VS Code com suporte Java.
Guia de Execução (Passo a Passo)
1) Pré-requisitos
JDK 22 instalado e JAVA_HOME/ PATHconfigurado.
Banco de dados Oracle.
Driver JDBC (ojdbc*.jar) adicionado ao classpath do projeto.
Crie usuário/schema no Oracle e execute os scripts SQL abaixo.
2) para h
Abra banco/ConnectionFactory.javae configure:

String urlDeConexao = "jdbc:oracle:thin:@<host>:<porta>:<SID>";
String login = "<seu_usuario>";
String senha = "<sua_senha>";
3) Importar projeto na IDE
Arquivo > Abrir > selecione a pasta raiz do projeto (Agata).
Verifique se srcestá marcado como Source Root.
Adicione o JAR do driver JDBC às bibliotecas do projeto.
4) Rodar a aplicação
Abra app.Main.javae execute uma classe principal (Run).
A interação principal é via console (acionada por menu). Siga as opções disponíveis.
Scripts SQL (Esquema)
Copie e execute os scripts abaixo no seu esquema Oracle:

-- SEQUÊNCIAS
CREATE SEQUENCE SEQ_PACIENTE START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;
CREATE SEQUENCE SEQ_CONSULTA START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;

-- TABELAS
CREATE TABLE PACIENTE (
    ID NUMBER PRIMARY KEY,
    NOME VARCHAR2(100) NOT NULL,
    CPF VARCHAR2(14) UNIQUE NOT NULL
);

CREATE TABLE MEDICO (
    CRM VARCHAR2(20) PRIMARY KEY,
    NOME_MEDICO VARCHAR2(100) NOT NULL,
    ESPECIALIDADE_MEDICO VARCHAR2(50) NOT NULL
);

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


*Arquivo gerado automaticamente — versão README atualizada para o projeto Ágata.*
Sobre
Nenhuma descrição, site ou tópico foi fornecido.
Recursos
 Leia-me
 Atividade
Estrelas
 0 estrelas
Observadores
 0 pessoas assistindo
Garfos
 0 garfos
Lançamentos
Nenhuma versão publicada
Criar uma nova versão
Pacotes
Nenhum pacote publicado.
Publique seu primeiro pacote.
Rodapé
