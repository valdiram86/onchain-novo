# 📊 Painel RSI – Criptomoedas em Alta

Este painel foi desenvolvido para exibir as criptomoedas com maior variação positiva diária, organizadas por faixas de RSI (Índice de Força Relativa), volume e market cap. O sistema é conectado diretamente a uma planilha Google Sheets atualizada automaticamente via Apps Script.

## 🔗 Acesso ao painel

> 🔐 Acesso restrito por e-mail autorizado

🌐 Painel online:  
[https://onchain-novo.vercel.app](https://onchain-novo.vercel.app) *(exemplo de domínio, ajuste conforme a implantação)*

---

## ✅ Funcionalidades

- Verificação de e-mail autorizando acesso
- Carregamento de dados por aba (`TopMoedas1D`, `OndaDeAlta_5`, `OndaDeAlta_7_5`, `OndaDeAlta_10`)
- Exibição dos dados com coloração por variação e RSI
- Botões:
  - **Atualizar Dados** (manual)
  - **Exportar CSV**
  - **Testar aba manualmente**
- Campo de filtro por símbolo
- Tabela responsiva com ordenação por coluna

---

## 📁 Estrutura

| Coluna             | Descrição                                  |
|--------------------|---------------------------------------------|
| `Ranking`          | Posição no ranking do CoinMarketCap         |
| `Símbolo`          | Código da criptomoeda                       |
| `Link`             | Acesso direto ao CoinMarketCap              |
| `RSI (1D)`         | RSI diário (via Twelve Data API)            |
| `Variação 1D (%)`  | Percentual de valorização em 24 horas       |
| `Volume (24h)`     | Volume negociado                            |
| `Market Cap`       | Capitalização de mercado estimada           |

---

## 🛠️ Tecnologias Utilizadas

- Google Apps Script
- Google Sheets
- HTML + CSS + JavaScript
- Vercel (hospedagem)
- CoinMarketCap API
- Twelve Data API

---

## 🧪 Como funciona

1. O script Apps Script coleta e filtra criptomoedas com base em critérios como variação, RSI e market cap.
2. Os dados são salvos em abas específicas da planilha.
3. O painel acessa essas abas via endpoint `doGet` autenticado por e-mail.
4. Os dados são renderizados dinamicamente no navegador.

---

## ⚙️ Variáveis de ambiente (se necessário)

Se for usar API ou rotas protegidas:

```env
NEXT_PUBLIC_API=https://script.google.com/macros/s/AKfycb.../exec
