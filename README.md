# 🎵 Análise de Vendas e Desempenho do E-Commerce de Música (Chinook Database)

Este projeto analisa o desempenho financeiro, comercial e de catálogo da loja digital de música **Chinook**, utilizando **SQL (SQLite)** via DBeaver. 

O objetivo principal é transformar dados operacionais em **insights estratégicos de negócios**, identificando os mercados mais lucrativos, os clientes de maior valor (LTV) e os artistas que mais geram receita.

---

## 🛠️ Tecnologias e Conceitos Utilizados
* **Banco de Dados:** SQLite (Chinook Sample Database)
* **IDE:** DBeaver
* **Linguagem:** SQL
* **Comandos e Funções:** `INNER JOIN` (junção de até 4 tabelas relacionais), `GROUP BY`, `ORDER BY`, `SUM()`, `COUNT()`, `ROUND()`, `LIMIT` e Aliases (`AS`).

---

## 📌 Perguntas de Negócio e Resultados

### 1. Faturamento por País (Visão Geográfica)
Quais são os 10 principais mercados consumidores da loja em volume de receita?

```sql
SELECT 
    BillingCountry AS Pais,
    COUNT(InvoiceId) AS Total_Vendas,
    ROUND(SUM(Total), 2) AS Faturamento_Total
FROM Invoice
GROUP BY BillingCountry
ORDER BY Faturamento_Total DESC
LIMIT 10;

### 1. Faturamento por País (Visão Geográfica)
Quais são os 10 principais mercados consumidores da loja em volume de receita?

```sql
SELECT 
    BillingCountry AS Pais,
    COUNT(InvoiceId) AS Total_Vendas,
    ROUND(SUM(Total), 2) AS Faturamento_Total
FROM Invoice
GROUP BY BillingCountry
ORDER BY Faturamento_Total DESC
LIMIT 10;
```

#### 📊 Resultado da Consulta:
| Pais | Total_Vendas | Faturamento_Total |
| :--- | :---: | :---: |
| USA  | 91 | $523.06 |
| Canada | 56 | $303.96 |
| France | 35 | $195.10 |
| Brazil | 35 | $190.10 |
| Germany | 35 | $156.48 |
| United Kingdom | 28 | $112.86 |
| Czech Republic | 14 | $90.24 |
| Portugal | 14 | $77.24 |
| India | 21 | $75.26 |
| Chile | 14 | $46.62 |

### 2. Top 10 Artistas por Receita Gerada (Visão de Produto)
Mapeamento do faturamento real gerado pelas faixas vendidas de cada artista (junção de 4 tabelas: Artist -> Album -> Track -> InvoiceLine).

SELECT 
    ar.Name AS Artista,
    COUNT(il.InvoiceLineId) AS Total_Vendas_Faixas,
    ROUND(SUM(il.UnitPrice * il.Quantity), 2) AS Faturamento_Total
FROM Artist ar
JOIN Album al ON ar.ArtistId = al.ArtistId
JOIN Track t ON al.AlbumId = t.AlbumId
JOIN InvoiceLine il ON t.TrackId = il.TrackId
GROUP BY ar.ArtistId, ar.Name
ORDER BY Faturamento_Total DESC
LIMIT 10;

#### 📊 Resultado da Consulta:
| Artista | Total_Vendas_Faixas | Faturamento_Total |
| :--- | :---: | :---: |
| Iron Maiden | 140 | $138.60 |
| U2 | 107 | $105.93 |
| Metallica | 91 | $90.09 |
| Led Zeppelin | 87 | $86.13 |
| Lost | 42 | $83.58 |
| The Office | 31 | $61.69 |
| AC/DC | 35 | $34.65 |
| Foo Fighters | 35 | $34.65 |
| The Cult | 35 | $34.65 |
| Pearl Jam | 32 | $31.68 |


3. Top 10 Clientes VIP / LTV (Visão de Cliente)
Identificação dos clientes que mais investiram na plataforma ao longo do tempo.

SELECT 
    c.CustomerId,
    c.FirstName || ' ' || c.LastName AS Nome_Cliente,
    c.Country AS Pais,
    ROUND(SUM(i.Total), 2) AS Total_Gasto
FROM Customer c
JOIN Invoice i ON c.CustomerId = i.CustomerId
GROUP BY c.CustomerId, Nome_Cliente, c.Country
ORDER BY Total_Gasto DESC
LIMIT 10;

#### 📊 Resultado da Consulta:
| CustomerId | Nome_Cliente | Pais | Total_Gasto |
| :---: | :--- | :--- | :---: |
| 6 | Helena Holý | Czech Republic | $49.62 |
| 26 | Richard Cunningham | USA | $47.62 |
| 57 | Luis Rojas | Chile | $46.62 |
| 45 | Ladislav Kovács | Hungary | $45.62 |
| 46 | Hugh O'Reilly | Ireland | $45.62 |
| 37 | Fynn Zimmermann | Germany | $43.62 |
| 24 | Frank Ralston | USA | $43.62 |
| 28 | Julia Barnett | USA | $43.62 |
| 25 | Victor Stevens | USA | $42.62 |
| 7 | Astrid Gruber | Austria | $42.62 |


