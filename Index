<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Painel RSI – WebApp Oficial</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      padding: 20px;
    }
    input, button, select {
      padding: 10px;
      font-size: 16px;
    }
    input[type="email"], input[type="text"] {
      width: 320px;
    }
    button {
      background-color: #00b894;
      color: white;
      border: none;
      margin-left: 5px;
      cursor: pointer;
    }
    #mensagem, #status {
      margin-top: 10px;
      font-weight: bold;
    }
    #painel {
      display: none;
      margin-top: 20px;
    }
    table {
      border-collapse: collapse;
      width: 100%;
      background: white;
      margin-top: 10px;
    }
    th, td {
      border: 1px solid #999;
      padding: 6px;
      text-align: center;
    }
    th {
      background-color: #ddd;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h2>Painel RSI – WebApp Oficial</h2>

  <p>Digite seu e-mail autorizado:</p>
  <input type="email" id="email" placeholder="seu@email.com" value="valdiram.lima.2013@gmail.com" />
  <button onclick="verificar()">Entrar</button>
  <p id="mensagem"></p>

  <div id="painel">
    <label>Selecionar aba:</label>
    <select id="seletorAba">
      <option value="OndaDeAlta_5">OndaDeAlta_5</option>
      <option value="OndaDeAlta_7_5">OndaDeAlta_7_5</option>
      <option value="OndaDeAlta_10" selected>OndaDeAlta_10</option>
    </select>
    <button onclick="carregarTabela()">Testar Aba Manualmente</button>

    <p id="status"></p>
    <table id="tabela"></table>
  </div>

  <script>
    const SCRIPT_URL = "https://script.google.com/macros/s/SEU_URL_DO_SCRIPT/exec";

    let dadosAtuais = [];

    async function verificar() {
      const email = document.getElementById("email").value.trim();
      document.getElementById("mensagem").innerText = "🔍 Verificando...";

      try {
        const resposta = await fetch(`${SCRIPT_URL}?email=${encodeURIComponent(email)}`);
        const texto = await resposta.text();

        document.getElementById("mensagem").innerText = texto;

        if (texto.includes("✅")) {
          document.getElementById("painel").style.display = "block";
          carregarTabela();
        }
      } catch (erro) {
        document.getElementById("mensagem").innerText = "❌ Erro de conexão.";
      }
    }

    async function carregarTabela() {
      const aba = document.getElementById("seletorAba").value;
      document.getElementById("status").innerText = `🔄 Carregando aba ${aba}...`;

      try {
        const resposta = await fetch(`${SCRIPT_URL}?aba=${encodeURIComponent(aba)}`);
        const dados = await resposta.json();

        if (!Array.isArray(dados) || dados.length === 0) {
          document.getElementById("status").innerText = "❌ Nenhum dado encontrado.";
          return;
        }

        dadosAtuais = dados;
        montarTabela(dados);
        document.getElementById("status").innerText = `✅ ${dados.length} linhas carregadas da aba ${aba}.`;
      } catch (erro) {
        document.getElementById("status").innerText = "❌ Erro ao carregar dados.";
      }
    }

    function montarTabela(dados) {
      const tabela = document.getElementById("tabela");
      const headers = dados[0];
      let html = "<tr>";

      headers.forEach(h => html += `<th>${h}</th>`);
      html += "</tr>";

      for (let i = 1; i < dados.length; i++) {
        html += "<tr>" + dados[i].map((valor, j) => {
          if (j === 2 && typeof valor === "string" && valor.includes("http")) {
            return `<td><a href="${valor}" target="_blank">🔗</a></td>`;
          }
          return `<td>${valor}</td>`;
        }).join("") + "</tr>";
      }

      tabela.innerHTML = html;
    }
  </script>
</body>
</html>
