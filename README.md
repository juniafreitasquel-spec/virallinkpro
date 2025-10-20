# virallinkpro
Aplicativo para divulgação de links
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>ViralLink Pro - Versão Simples</title>
  <style>
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #3A0CA3, #4361EE);
      color: white;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      min-height: 100vh;
    }

    header {
      text-align: center;
      padding: 30px 10px;
    }

    header h1 {
      font-size: 2rem;
      margin-bottom: 0.5rem;
    }

    header p {
      color: #cfcfff;
    }

    main {
      width: 90%;
      max-width: 500px;
      background-color: rgba(255, 255, 255, 0.1);
      border-radius: 16px;
      padding: 20px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
      margin-bottom: 30px;
    }

    label {
      display: block;
      margin-top: 15px;
      font-weight: 600;
    }

    input[type="text"], textarea {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: none;
      border-radius: 8px;
      outline: none;
      font-size: 1rem;
    }

    input[type="text"] {
      background-color: #f7f7ff;
      color: #333;
    }

    button {
      width: 100%;
      padding: 12px;
      margin-top: 20px;
      border: none;
      border-radius: 10px;
      background-color: #7209B7;
      color: #fff;
      font-weight: 600;
      font-size: 1rem;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    button:hover {
      background-color: #560BAD;
    }

    .results {
      margin-top: 25px;
      padding: 15px;
      background: rgba(0, 0, 0, 0.2);
      border-radius: 10px;
    }

    .result-item {
      background: rgba(255, 255, 255, 0.15);
      padding: 10px;
      margin-top: 10px;
      border-radius: 8px;
      word-wrap: break-word;
    }

    footer {
      text-align: center;
      font-size: 0.9rem;
      color: #ccc;
      padding: 20px;
    }
  </style>
</head>
<body>
  <header>
    <h1>ViralLink Pro</h1>
    <p>Crie, organize e acompanhe seus links Shopee manualmente</p>
  </header>

  <main>
    <form id="linkForm">
      <label for="productName">Nome do produto:</label>
      <input type="text" id="productName" placeholder="Ex: Fone Bluetooth XYZ" required />

      <label for="productLink">Link do produto (Shopee):</label>
      <input type="text" id="productLink" placeholder="https://shopee.com.br/..." required />

      <label for="platform">Plataforma de divulgação:</label>
      <input type="text" id="platform" placeholder="Ex: TikTok, Instagram, WhatsApp" />

      <button type="submit">Salvar Link</button>
    </form>

    <div class="results" id="results">
      <h3>📊 Links Salvos</h3>
      <div id="linkList"></div>
    </div>
  </main>

  <footer>
    ViralLink Pro © 2025 — versão gratuita para afiliados Shopee 💜
  </footer>

  <script>
    const form = document.getElementById('linkForm');
    const linkList = document.getElementById('linkList');

    function loadLinks() {
      const links = JSON.parse(localStorage.getItem('viralLinks') || '[]');
      linkList.innerHTML = '';
      links.forEach((item, index) => {
        const div = document.createElement('div');
        div.classList.add('result-item');
        div.innerHTML = `<strong>${item.name}</strong><br>
          🔗 <a href="${item.link}" target="_blank" style="color:#fff;">${item.link}</a><br>
          📱 Plataforma: ${item.platform || '—'}<br>
          <button style="margin-top:8px; padding:5px 10px; border:none; border-radius:6px; background:#F72585; color:#fff; cursor:pointer;" onclick="deleteLink(${index})">Excluir</button>`;
        linkList.appendChild(div);
      });
    }

    function saveLink(name, link, platform) {
      const links = JSON.parse(localStorage.getItem('viralLinks') || '[]');
      links.push({ name, link, platform });
      localStorage.setItem('viralLinks', JSON.stringify(links));
      loadLinks();
    }

    function deleteLink(index) {
      const links = JSON.parse(localStorage.getItem('viralLinks') || '[]');
      links.splice(index, 1);
      localStorage.setItem('viralLinks', JSON.stringify(links));
      loadLinks();
    }

    form.addEventListener('submit', e => {
      e.preventDefault();
      const name = document.getElementById('productName').value;
      const link = document.getElementById('productLink').value;
      const platform = document.getElementById('platform').value;
      saveLink(name, link, platform);
      form.reset();
    });

    loadLinks();
  </script>
</body>
</html>
