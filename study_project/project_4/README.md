# Desafio DIO + WEX - SQL Server e Banco de Dados

Projeto proposto no Bootcamp **.NET Developer - WEX - End to End Engineering**, da plataforma **Digital Innovation One (DIO)**, com foco em modelagem e manipulação de dados utilizando **SQL Server**.

---

### 📊 Objetivo

Executar consultas SQL em um banco de dados relacional com estrutura de filmes, gêneros e atores. As queries demonstram conceitos como:

- Filtragem de dados
- Ordenação
- Agregação (COUNT, MAX)
- Relacionamentos via **JOINs**
- Uso de **chaves primárias e estrangeiras**

---

### 📃 Script de Criação do Banco

O script `films.sql` contido neste repositório realiza:

- Criação do banco `Filmes`
- Tabelas:
  - `Atores`
  - `Filmes`
  - `ElencoFilme`
  - `Generos`
  - `FilmesGenero`
- Relacionamentos entre tabelas com **chaves estrangeiras**
- Popularização das tabelas com dados reais (inserções via `INSERT`)

---

## 🔍 Consultas (Queries)

Todas as consultas estão no arquivo `challenge.sql`.

#### 1. Selecionar título e ano de lançamento

```sql

SELECT Nome, Ano FROM Filmes;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie1.jpg" alt="Querie 1" style="width: 600px;">

---

#### 2. Buscar o nome e ano dos filmes, ordenados por ordem crescente pelo ano

```sql

SELECT Nome, Ano FROM Filmes ORDER BY Ano ASC;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie2.jpg" alt="Querie 2" style="width: 600px;">

---

#### 3. Buscar pelo filme de volta para o futuro, trazendo o nome, ano e a duração

```sql

SELECT Nome, Ano, Duracao FROM Filmes WHERE Nome = 'De Volta para o Futuro';

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie3.jpg" alt="Querie 3" style="width: 600px;">

---

#### 4. Buscar os filmes lançados em 1997

```sql

SELECT Nome, Ano, Duracao FROM Filmes WHERE Ano = 1997;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie4.jpg" alt="Querie 4" style="width: 600px;">

---

#### 5. Buscar filmes lançados após 2000

```sql

SELECT Nome, Ano, Duracao FROM Filmes WHERE Ano > 2000;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie5.jpg" alt="Querie 5" style="width: 600px;">

---

#### 6. Buscar os filmes com a duracao maior que 100 e menor que 150, ordenando pela duracao em ordem crescente

```sql

SELECT Nome, Ano, Duracao FROM Filmes WHERE Duracao > 100 AND Duracao < 150 ORDER BY Duracao ASC;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie6.jpg" alt="Querie 6" style="width: 600px;">

---

#### 7. Contagem de filmes por ano, ordenando por maior duração

```sql

SELECT Ano, COUNT(*) AS ContagemDeFilmes, MAX(Duracao) AS MaiorDuracao FROM Filmes GROUP BY Ano ORDER BY MaiorDuracao DESC;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie7.jpg" alt="Querie 7" style="width: 600px;">

---

####  8. Buscar os Atores do gênero masculino, retornando o PrimeiroNome, UltimoNome

```sql

SELECT PrimeiroNome, UltimoNome, Genero FROM Atores WHERE Genero = 'M';

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie8.jpg" alt="Querie 8" style="width: 600px;">

---

#### 9. Buscar os Atores do gênero feminino, retornando o PrimeiroNome, UltimoNome, e ordenando pelo PrimeiroNome

```sql

SELECT PrimeiroNome, UltimoNome, Genero FROM Atores WHERE Genero = 'F' ORDER BY PrimeiroNome ASC;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie9.jpg" alt="Querie 9" style="width: 600px;">

---

#### 10. Filme + Gênero

```sql

SELECT Filmes.Nome, Generos.Genero FROM Filmes 
JOIN FilmesGenero ON Filmes.Id = FilmesGenero.IdFilme 
JOIN Generos ON FilmesGenero.IdGenero = Generos.Id;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie10.jpg" alt="Querie 10" style="width: 600px;">

---

#### 11. Buscar o nome do filme e o gênero do tipo "Mistério"

```sql

SELECT Filmes.Nome, Generos.Genero FROM Filmes
INNER JOIN FilmesGenero ON Filmes.Id = FilmesGenero.IdFilme
INNER JOIN Generos ON FilmesGenero.IdGenero = Generos.Id
WHERE Genero = 'Mistério';

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie11.jpg" alt="Querie 11" style="width: 600px;">

---

#### 12. Filme + Atores + Papel

```sql

SELECT Filmes.Nome, Atores.PrimeiroNome, Atores.UltimoNome, ElencoFilme.Papel FROM Filmes
JOIN ElencoFilme ON Filmes.Id = ElencoFilme.IdFilme
JOIN Atores ON ElencoFilme.IdAtor = Atores.Id;

```

<img src="https://github.com/fzanneti/wex_e2e_csharp/blob/main/study_project/project_4/assets/images/querie12.jpg" alt="Querie 12" style="width: 600px;">

---

### 🔗 Relacionamento das Tabelas

* **Filmes** (Id)   
  └─ 1\:N com **FilmesGenero** (IdFilme)   
  └─ 1\:N com **ElencoFilme** (IdFilme)   

* **Generos** (Id)   
  └─ 1\:N com **FilmesGenero** (IdGenero)   

* **Atores** (Id)   
  └─ 1\:N com **ElencoFilme** (IdAtor)   

---

### 📖 Aprendizados

* Prática de consultas SQL fundamentais para backend com .NET
* Compreensão de **JOINs** e manipulação de dados entre tabelas
* Modelagem de banco de dados relacional
* Conceitos de chaves primárias e estrangeiras

---

### 📁 Como usar este repositório

1. Clone o repositório ou baixe os arquivos `.sql`
2. Execute o script `films.sql` no **SQL Server Management Studio**
3. Utilize o arquivo `challenge.sql` para testar as queries

---

### 🚀 Sobre

Este desafio faz parte da trilha .NET + Banco de Dados oferecida pela [Digital Innovation One](https://dio.me) em parceria com a [WEX Brasil](https://www.wexinc.com/pt-br/).

---

#### 📄 Licença

Este projeto é de uso livre para fins educacionais. Compartilhe, estude e contribua! 🚀

---

##### ✍️ **Seção criada por:** *Fabio Zanneti* 🎯 Projeto: **WEX - End to End Engineering**