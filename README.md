# 🎓 APSI-PROINT — Data Warehouse & Business Intelligence

Repositório unificado para o projeto desenvolvido nas disciplinas **Projeto Integrador (PROINT)** e **Análise e Projeto de Sistemas de Informação (APSI)** — Bacharelado em Sistemas de Informação, semestre **2025.1**.

---

## 📚 Índice

- [📌 Descrição do Projeto](#-descrição-do-projeto)
- [📁 Organização do Repositório](#-organização-do-repositório)
- [🛠 Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [🐳 Inicialização do Ambiente Docker](#-inicialização-do-ambiente-docker-passo-a-passo)
- [🗃️ Conexão via PgAdmin](#️-conexão-via-pgadmin)
- [⚙️ Carga de Dados — Pentaho PDI (ETL)](#️-carga-de-dados--pentaho-pdi-etl)
- [📊 Conexão no Power BI](#-conexão-no-power-bi)
- [📐 Arquitetura do Projeto](#-arquitetura-do-projeto)
- [👥 Colaboradores](#-colaboradores)

---

## 📌 Descrição do Projeto

O objetivo deste projeto é desenvolver uma solução completa de **Data Warehouse (DW)** e **Business Intelligence (BI)** para integrar, armazenar e analisar **dados criminais e demográficos do estado de Alagoas**.

A solução envolve:

- Modelagem dimensional  
- Ingestão e tratamento de dados (ETL com Pentaho PDI)  
- Infraestrutura containerizada  
- Dashboards interativos com Power BI  

---

## 📁 Organização do Repositório

- 🗂️ **Trello:** https://trello.com/b/Dp9VDaAQ/proint-apsi  
- 📄 **Google Drive:** https://drive.google.com/drive/u/0/folders/1lu4PswSunfSxKgVsDYo36EFelErIbT4t  

---

## 🛠 Tecnologias Utilizadas

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Pentaho](https://img.shields.io/badge/Pentaho_PDI-0A5?logo=pentaho&logoColor=white)
![PowerBI](https://img.shields.io/badge/Power_BI-F2C811?logo=powerbi&logoColor=black)
![GitHub](https://img.shields.io/badge/GitHub-000?logo=github&logoColor=white)

---

## 🐳 Inicialização do Ambiente Docker (Passo a Passo)

### Pré-requisitos
- Docker e Docker Compose instalados  
- Estar no diretório do arquivo `docker-compose.yml`  
- Ter o arquivo DDL `dw_ssp.sql` disponível localmente  

---

### Passo 1 — Iniciar os containers
```bash
docker-compose up -d
```

---

### Passo 2 — Aplicar a estrutura do banco (DDL)

#### Windows (PowerShell/CMD)
```bash
docker exec -i dw_cvli_postgres psql -U user_dw -d dw_cvli_docker < C:\apsi-proint-main\dw_ssp.sql
```

#### Git Bash (MINGW64)
```bash
docker exec -i dw_cvli_postgres psql -U user_dw -d dw_cvli_docker < /c/apsi-proint-main/dw_ssp.sql
```

---

### Passo 3 — Validar tabelas
```bash
docker exec -it dw_cvli_postgres psql -U user_dw -d dw_cvli_docker -c "\dt"
```

---

### Passo 4 — Teste simples
```sql
SELECT count(*) FROM public.dim_local;
```

---

### 🔧 Comandos úteis

Entrar no container:
```bash
docker exec -it dw_cvli_postgres bash
```

Acessar o psql:
```bash
docker exec -it dw_cvli_postgres psql -U user_dw -d dw_cvli_docker
```

Derrubar containers:
```bash
docker-compose down
```

Derrubar + remover volumes:
```bash
docker-compose down -v
```

---

## 🗃️ Conexão via PgAdmin

1. **Create → Server**  
2. Aba *Connection*:  
   - Host: `localhost`  
   - Port: `5432`  
   - Database: `dw_cvli_docker`  
3. Aba *Authentication*:  
   - Username: `user_dw`  
   - Password: `mestre`  

Validação:
```sql
SELECT count(*) FROM public.dim_local;
```

---

## ⚙️ Carga de Dados — Pentaho PDI (ETL)

### 1) Configurar Conexão `ssp`
- Tipo: PostgreSQL  
- Host: `localhost`  
- Porta: `5432`  
- Banco: `dw_cvli_docker`  
- Usuário: `user_dw`  
- Senha: `mestre`  

---

### 2) Ajustar caminhos das fontes (Planilhas Excel)

Em **todas as transformações (.ktr)**, configure:

```
C:/apsi-proint-main/Bases de Dados/
```

---

### 3) Executar o Job Principal

- Abrir: `job_dw_ssp.kjb`  
- Clicar: **Run**  

---

### ✔ 4) Validar carga
```sql
SELECT count(*) FROM fato_cvli;
```

---

## 📊 Conexão no Power BI

1. Obter Dados → **PostgreSQL**  
2. Servidor: `localhost:5432`  
3. Banco: `dw_cvli_docker`  
4. Usuário: `user_dw` / Senha: `mestre`  
5. Selecionar tabelas  
6. Carregar  

---

## Arquitetura do Projeto

<img width="1920" height="1080" alt="Arquitetura Atualizada" src="https://github.com/user-attachments/assets/85f1bfd2-e29b-42f3-814d-37217f8110e5" />

---

## 👥 Colaboradores

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/LaianeBarreto">
        <img src="https://github.com/LaianeBarreto.png" width="100px;"><br>
        <sub><b>Laiane Barreto</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/amandargusmao">
        <img src="https://github.com/amandargusmao.png" width="100px;"><br>
        <sub><b>Amanda Gusmão</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/robertoferreira7">
        <img src="https://github.com/robertoferreira7.png" width="100px;"><br>
        <sub><b>Roberto Ferreira</b></sub>
      </a>
    </td>
  </tr>
</table>
