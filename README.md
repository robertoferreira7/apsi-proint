🎓 APSI-PROINT — Data Warehouse & Business Intelligence
Repositório unificado para o projeto desenvolvido nas disciplinas Projeto Integrador (PROINT) e Análise e Projeto de Sistemas de Informação (APSI) — Bacharelado em Sistemas de Informação, semestre 2025.1.
📌 Descrição do Projeto

O objetivo deste projeto é desenvolver e implementar uma solução de Data Warehouse (DW) e Business Intelligence (BI) para integrar, armazenar e analisar dados criminais e demográficos do estado de Alagoas.

A solução integra modelagem, ingestão de dados, processamento ETL e visualização analítica.

📁 Organização do Repositório

🖼️ Trello — adicionar link

📄 Documento do Trabalho — adicionar link

📊 Cronograma — adicionar link

📜 Termo de Abertura — adicionar link

🛠 Tecnologias Utilizadas
Tecnologia	Aplicação
pgModeler	Modelagem lógica e física do Data Warehouse
PostgreSQL	SGBD utilizado para hospedar o DW
Pentaho PDI (Kettle)	Processos ETL para carga e tratamento dos dados
Power BI	Dashboards, relatórios interativos e análise visual
Docker & Docker Compose	Infraestrutura containerizada para o PostgreSQL do DW
🐳 Guia Docker — Configuração do Ambiente do DW
1. Inicialização do Ambiente
Ação	Comando / Instrução	Observações
1.1. Iniciar o serviço	No terminal, dentro da pasta com docker-compose.yml:

bash\ndocker-compose up -d\n	Sobe o container e cria o volume db-data.
1.2. Aplicar estrutura (DDL)	bash\ndocker exec -i dw_cvli_postgres psql -U user_dw -d dw_cvli_docker < C:\apsi-proint-main\dw_ssp.sql\n	No Git Bash, usar: /c/apsi-proint-main/dw_ssp.sql
1.3. Validar tabelas	bash\ndocker exec -it dw_cvli_postgres psql -U user_dw -d dw_cvli_docker -c "\dt"\n	Lista as tabelas criadas.
🗃️ Conexão via PgAdmin

No PgAdmin: Create → Server

Aba Connection

Host: localhost

Port: 5432

Database: dw_cvli_docker

Aba Authentication

Username: user_dw

Password: mestre

Validar conexão:

SELECT count(*) FROM public.dim_local;

⚙️ Carga de Dados — Pentaho PDI (ETL)
3.1 Configurar conexão ssp

Tipo: PostgreSQL

Host: localhost

Porta: 5432

Banco: dw_cvli_docker

Usuário: user_dw

Senha: mestre

3.2 Ajustar caminhos das fontes

Em todas as transformações (.ktr):

Abrir step Microsoft Excel Input

Selecionar arquivo em:

C:\apsi-proint-main\Bases de Dados\


Clicar Add

3.3 Executar o Job principal

Abrir: job_dw_ssp.kjb

Clicar: Run

3.4 Validar carga
SELECT count(*) FROM fato_cvli;

📊 Conexão no Power BI

Obter Dados → PostgreSQL

Servidor: localhost:5432

Banco: dw_cvli_docker

Credenciais:

Usuário: user_dw

Senha: mestre

Selecionar tabelas (dimensões e fato)

Carregar dados

👥 Colaboradores
<table> <tr> <td align="center"> <a href="https://github.com/LaianeBarreto"> <img src="https://github.com/LaianeBarreto.png" width="100px;"><br> <b>Laiane Barreto</b> </a> </td> <td align="center"> <a href="https://github.com/amandargusmao"> <img src="https://github.com/amandargusmao.png" width="100px;"><br> <b>Amanda Gusmão</b> </a> </td> <td align="center"> <a href="https://github.com/robertoferreira7"> <img src="https://github.com/robertoferreira7.png" width="100px;"><br> <b>Roberto Ferreira</b> </a> </td> </tr> </table>
