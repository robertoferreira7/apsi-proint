# 🎓 APSI-PROINT --- Data Warehouse & Business Intelligence

### Repositório unificado para o projeto desenvolvido nas disciplinas **Projeto Integrador (PROINT)** e **Análise e Projeto de Sistemas de Informação (APSI)** --- Bacharelado em Sistemas de Informação, semestre **2025.1**.

------------------------------------------------------------------------

## 📌 Descrição do Projeto

O objetivo deste projeto é desenvolver e implementar uma solução de
**Data Warehouse (DW)** e **Business Intelligence (BI)** para integrar,
armazenar e analisar **dados criminais e demográficos do estado de
Alagoas**.

A solução integra modelagem, ingestão de dados, processamento ETL e
visualização analítica.

------------------------------------------------------------------------

## 📁 Organização do Repositório

-   🖼️ **Trello** --- *adicionar link*\
-   📄 **Documento do Trabalho** --- *adicionar link*\
-   📊 **Cronograma** --- *adicionar link*\
-   📜 **Termo de Abertura** --- *adicionar link*

------------------------------------------------------------------------

## 🛠 Tecnologias Utilizadas

  -----------------------------------------------------------------------
  Tecnologia                          Aplicação
  ----------------------------------- -----------------------------------
  **pgModeler:**                       Modelagem lógica e física do Data
                                      Warehouse

  **PostgreSQL:**                      SGBD utilizado para hospedar o DW

  **Pentaho PDI (Kettle):**            Processos ETL para carga e
                                      tratamento dos dados

  **Power BI:**                        Dashboards, relatórios interativos
                                      e análise visual

  **Docker & Docker Compose:**         Infraestrutura containerizada para
                                      o PostgreSQL do DW
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# Guia de Inicialização do Ambiente Docker do Data Warehouse

## 🐳 Inicialização do Ambiente Docker (Passo a Passo)

### Pré-requisitos
- Docker e Docker Compose instalados.
- Estar no mesmo diretório do arquivo `docker-compose.yml`.
- Ter o arquivo DDL `dw_ssp.sql` disponível localmente.

---

### Passo 1 — Iniciar os containers
```bash
docker-compose up -d
```

---

### Passo 2 — Aplicar a estrutura do banco (DDL)
No Windows (PowerShell ou CMD):
```bash
docker exec -i dw_cvli_postgres psql -U user_dw -d dw_cvli_docker < C:\apsi-proint-main\dw_ssp.sql
```

No Git Bash (MINGW64):
```bash
docker exec -i dw_cvli_postgres psql -U user_dw -d dw_cvli_docker < /c/apsi-proint-main/dw_ssp.sql
```

---

### Passo 3 — Validar as tabelas criadas
```bash
docker exec -it dw_cvli_postgres psql -U user_dw -d dw_cvli_docker -c "\dt"
```

---

### Passo 4 — Teste simples
```sql
SELECT count(*) FROM public.dim_local;
```

---

### Comandos úteis
- Entrar no container:
```bash
docker exec -it dw_cvli_postgres bash
```

- Acessar o psql:
```bash
docker exec -it dw_cvli_postgres psql -U user_dw -d dw_cvli_docker
```

- Derrubar containers:
```bash
docker-compose down
```

- Derrubar + limpar volumes:
```bash
docker-compose down -v
```


# 🗃️ Conexão via PgAdmin

1.  No PgAdmin: **Create → Server**
2.  Aba **Connection**
    -   Host: `localhost`\
    -   Port: `5432`\
    -   Database: `dw_cvli_docker`
3.  Aba **Authentication**
    -   Username: `user_dw`\
    -   Password: `mestre`
4.  Validar conexão:

``` sql
SELECT count(*) FROM public.dim_local;
```

------------------------------------------------------------------------

# ⚙️ Carga de Dados --- Pentaho PDI (ETL)

## **3.1 Configurar conexão `ssp`**

-   Tipo: PostgreSQL\
-   Host: `localhost`\
-   Porta: `5432`\
-   Banco: `dw_cvli_docker`\
-   Usuário: `user_dw`\
-   Senha: `mestre`

## **3.2 Ajustar caminhos das fontes**

Em **todas as transformações (.ktr)**:

-   Abrir step **Microsoft Excel Input**
-   Selecionar arquivo em:

```{=html}
<!-- -->
```
    C:\apsi-proint-main\Bases de Dados\

-   Clicar **Add**

## **3.3 Executar o Job principal**

-   Abrir: `job_dw_ssp.kjb`
-   Clicar: **Run**

## **3.4 Validar carga**

``` sql
SELECT count(*) FROM fato_cvli;
```

------------------------------------------------------------------------

# 📊 Conexão no Power BI

1.  **Obter Dados → PostgreSQL**
2.  Servidor: `localhost:5432`
3.  Banco: `dw_cvli_docker`
4.  Credenciais:
    -   Usuário: `user_dw`\
    -   Senha: `mestre`
5.  Selecionar tabelas (dimensões e fato)\
6.  Carregar dados

------------------------------------------------------------------------

# 👥 Colaboradores

```{=html}
<table>
```
```{=html}
<tr>
```
```{=html}
<td align="center">
```
`<a href="https://github.com/LaianeBarreto">`{=html}
`<img src="https://github.com/LaianeBarreto.png" width="100px;">`{=html}`<br>`{=html}
`<b>`{=html}Laiane Barreto`</b>`{=html} `</a>`{=html}
```{=html}
</td>
```
```{=html}
<td align="center">
```
`<a href="https://github.com/amandargusmao">`{=html}
`<img src="https://github.com/amandargusmao.png" width="100px;">`{=html}`<br>`{=html}
`<b>`{=html}Amanda Gusmão`</b>`{=html} `</a>`{=html}
```{=html}
</td>
```
```{=html}
<td align="center">
```
`<a href="https://github.com/robertoferreira7">`{=html}
`<img src="https://github.com/robertoferreira7.png" width="100px;">`{=html}`<br>`{=html}
`<b>`{=html}Roberto Ferreira`</b>`{=html} `</a>`{=html}
```{=html}
</td>
```
```{=html}
</tr>
```
```{=html}
</table>
```
