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

## 📌 Perguntas de Negócio Resolvidas

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
