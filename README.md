<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Today Pizza - Novo Design</title>

<style>
    /* VARIÁVEIS DE COR E FONTES */
    :root {
        --primary: #f7931e; /* Laranja Moderno */
        --dark-bg: #1a1a1a; /* Fundo do Banner */
        --text-dark: #333;
        --text-light: #fff;
        --grey: #f4f4f4;
        --border-color: #ddd;
    }

    body {
        margin: 0;
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
        background-color: var(--grey);
        color: var(--text-dark);
    }

    /* --- HEADER (Como na Foto 2) --- */
    .header {
        background-color: #fff;
        padding: 0 20px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        height: 80px;
        box-shadow: 0 2px 5px rgba(0,0,0,0.05);
    }

    .logo-container {
        background-color: var(--primary);
        padding: 10px;
        border-radius: 0 0 10px 10px;
        position: relative;
        top: -10px;
    }

    .header img {
        width: 60px;
    }

    .header-icons {
        display: flex;
        gap: 15px;
        font-size: 1.5rem;
        cursor: pointer;
    }

    /* --- HERO/BANNER (Como na Foto 2) --- */
    .hero {
        background: url("https://images.unsplash.com/photo-1593560708920-61dd98c46a4e") center/cover no-repeat;
        height: 350px;
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
        text-align: center;
    }

    /* Filtro escuro para o texto ler bem */
    .hero::after {
        content: '';
        position: absolute;
        top: 0; left: 0; width: 100%; height: 100%;
        background: rgba(0,0,0,0.6);
    }

    .hero-content {
        position: relative;
        z-index: 1;
        color: var(--text-light);
        padding: 0 20px;
    }

    .hero-content h2 {
        font-size: 1.6rem;
        font-weight: bold;
        margin-bottom: 20px;
    }

    .btn-cardapio {
        background-color: var(--primary);
        color: var(--text-light);
        border: none;
        padding: 15px 30px;
        border-radius: 30px;
        font-weight: bold;
        font-size: 1.1rem;
        cursor: pointer;
        transition: 0.3s;
    }

    /* --- NOSSO CARDÁPIO (Título e Abas) --- */
    .section-title {
        text-align: center;
        padding: 40px 0 20px;
        color: var(--text-dark);
    }

    .tabs {
        display: flex;
        justify-content: center;
        gap: 10px;
        padding-bottom: 30px;
    }

    .tab {
        background-color: #e0e0e0;
        color: var(--text-dark);
        padding: 10px 20px;
        border-radius: 20px;
        cursor: pointer;
        font-weight: bold;
        font-size: 0.9rem;
    }

    .tab.active {
        background-color: var(--primary);
        color: var(--text-light);
    }

    /* --- LISTA DE PIZZAS (Layout da Foto 2) --- */
    .pizza-list {
        max-width: 800px;
        margin: 0 auto;
        padding: 0 20px 40px;
    }

    .pizza-item {
        background-color: #fff;
        padding: 15px;
        border-radius: 10px;
        display: flex;
        align-items: center;
        margin-bottom: 15px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.05);
    }

    .pizza-item img {
        width: 70px;
        height: 70px;
        border-radius: 50%;
        object-fit: cover;
        margin-right: 15px;
    }

    .pizza-info {
        flex-grow: 1;
    }

    .pizza-info h4 {
        margin: 0 0 5px;
        font-size: 1.1rem;
    }

    .pizza-info span {
        font-weight: bold;
        color: var(--text-dark);
    }

    .add-btn {
        background-color: var(--grey);
        color: var(--primary);
        border: 2px solid var(--primary);
        padding: 8px 15px;
        border-radius: 20px;
        cursor: pointer;
        font-weight: bold;
    }

    /* --- CHECKOUT/PEDIDO (Mais Limpo) --- */
    .checkout-section {
        background-color: #fff;
        max-width: 800px;
        margin: 0 auto 50px;
        padding: 25px;
        border-radius: 15px;
        box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }

    .checkout-section h3 {
        color: var(--text-dark);
        margin-bottom: 15px;
    }

    input, select {
        width: 100%;
        padding: 15px;
        margin-bottom: 15px;
        border: 1px solid var(--border-color);
        border-radius: 8px;
        background-color: #fff;
        font-size: 1rem;
        box-sizing: border-box;
    }

    .linha-endereco {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 15px;
    }

    #pixBox {
        display: none;
        background-color: #fef3c7;
        padding: 15px;
        border-radius: 8px;
        margin-bottom: 15px;
    }

    .btn-finalizar {
        background-color: #2ecc71;
        color: var(--text-light);
        border: none;
        width: 100%;
        padding: 18px;
        border-radius: 10px;
        font-size: 1.2rem;
        font-weight: bold;
        cursor: pointer;
    }
</style>
</head>
<body>

<div class="header">
    <div class="logo-container">
        <img src="logo.png" alt="Logo">
    </div>
    <div class="header-icons">
        <span>🛒</span> <span>☰</span>
    </div>
</div>

<div class="hero">
    <div class="hero-content">
        <h2>Delivery em Marechal Cândido Rondon - PR 🍕</h2>
        <button class="btn-cardapio" onclick="scrollCardapio()">Ver Cardápio</button>
    </div>
</div>

<div id="cardapio">
    <div class="section-title">
        <h2>Nosso Cardápio</h2>
    </div>

    <div class="tabs">
        <div class="tab active" onclick="trocar('salgada')">Salgadas</div>
        <div class="tab" onclick="trocar('doce')">Doces</div>
        <div class="tab" onclick="trocar('bebida')">Bebidas</div>
    </div>

    <div class="pizza-list" id="produtos"></div>
</div>

<div class="checkout-section">
    <h3>🛒 Seu Pedido</h3>
    <ul id="lista"></ul>
    <p style="font-size: 1.3rem;"><strong>Total: R$ <span id="total">0,00</span></strong></p>

    <hr>
    <h3>📍 Endereço</h3>
    <input type="text" id="rua" placeholder="Rua / Logradouro">
    <div class="linha-endereco">
        <input type="text" id="numero" placeholder="Número">
        <input type="text" id="bairro" placeholder="Bairro">
    </div>

    <h3>💳 Pagamento</h3>
    <select id="pagamento">
        <option value="PIX">Pix</option>
        <option value="CARTÃO">Cartão na entrega</option>
    </select>

    <div id="pixBox">
        <strong>✨ Chave Pix da Today Pizza:</strong><br>
        44998905286
    </div>

    <button class="btn-finalizar" onclick="finalizar()">✅ Finalizar no WhatsApp</button>
</div>

<script>
    // --- LÓGICA DO SISTEMA (MANTIDA IGUAL AO CÓDIGO 1) ---
    // (Apenas removi as fotos longas para o código caber aqui, adicionei fotos redondas)

    let produtos = {
        salgada: [
            {nome:"⭐ Calabresa Especial", preco:35, img:"https://altoastral.joaobidu.com.br/antigas/uploads/legacy/2016/07/AAT001-P001-89335-1-m-Divulgacao_1.jpg"},
            {nome:"⭐ Frango Cremoso com Catupiry", preco:38, img:"https://images.unsplash.com/photo-1593560708920-61dd98c46a4e"},
            {nome:"Moda da Casa", preco:45, img:"https://images.unsplash.com/photo-1594007654729-407eedc4fe24"}
        ],
        doce: [
            {nome:"🔥 Combo Doce (Chocolate + Guaraná)", preco:39, img:"https://images.unsplash.com/photo-1601924582975-7e6c94b2a8f8"},
            {nome:"⭐ Chocolate com Morango", preco:35, img:"https://images.unsplash.com/photo-1594007654729-407eedc4fe24"}
        ],
        bebida: [
            {nome:"⭐ Coca-Cola 2L", preco:12, img:"https://images.unsplash.com/photo-1581006852262-e4307cf6283a"},
            {nome:"Guaraná 2L", preco:10, img:"https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"}
        ]
    };

    let carrinho = [];
    let total = 0;

    function trocar(tipo){
        document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
        event.target.classList.add('active');

        let lista = document.getElementById("produtos");
        lista.innerHTML = "";

        produtos[tipo].forEach(p=>{
            // --- NOVO LAYOUT DO ITEM DA PIZZA ---
            lista.innerHTML += `
            <div class="pizza-item">
                <img src="${p.img}">
                <div class="pizza-info">
                    <h4>${p.nome}</h4>
                    <span>R$ ${p.preco}</span>
                </div>
                <button class="add-btn" onclick="add('${p.nome}',${p.preco})">Adicionar</button>
            </div>`;
        });
    }

    function add(nome, preco){
        carrinho.push({nome, preco});
        total += preco;

        let li = document.createElement("li");
        li.innerText = nome + " - R$ " + preco;

        document.getElementById("lista").appendChild(li);
        document.getElementById("total").innerText = total.toFixed(2);
    }

    function finalizar(){
        let rua = document.getElementById("rua").value;

        if(carrinho.length === 0 || rua === ""){
            alert("Preencha o pedido e endereço!");
            return;
        }

        let numeroCasa = document.getElementById("numero").value;
        let bairro = document.getElementById("bairro").value;
        let pagamento = document.getElementById("pagamento").value;

        let msg = "🍕 *TODAY PIZZA* 🍕\n\n";
        carrinho.forEach(i=>{ msg += "• " + i.nome + "\n"; });
        msg += "\n💰 Total: R$ " + total.toFixed(2);
        msg += "\n📍 Endereço: " + rua + ", " + numeroCasa + " - " + bairro;
        msg += "\n💳 Pagamento: " + pagamento;

        if(pagamento === "PIX"){ msg += "\n💸 Chave Pix: 44998905286"; }
        msg += "\n🚚 Marechal Cândido Rondon - PR";

        const whats = "5544998905286";
        const url = `https://wa.me/${whats}?text=${encodeURIComponent(msg)}`;
        window.open(url, "_blank");
    }

    function gerenciarExibicaoPix() {
        let selectPagamento = document.getElementById("pagamento");
        let pixBox = document.getElementById("pixBox");
        pixBox.style.display = selectPagamento.value === "PIX" ? "block" : "none";
    }

    document.getElementById("pagamento").addEventListener("change", gerenciarExibicaoPix);
    gerenciarExibicaoPix(); 

    function scrollCardapio(){
        document.getElementById("cardapio").scrollIntoView({behavior:"smooth"});
    }

    trocar('salgada'); // Carrega a primeira aba
</script>

</body>
</html>
</body>
</html>
