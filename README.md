<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Today Pizza - Delivery</title>

<style>
    :root {
        --primary: #d97706;
        --secondary: #f5e6d3;
        --dark: #5a3e2b;
        --success: #16a34a;
    }

    body {
        margin: 0;
        font-family: 'Georgia', serif;
        background: var(--secondary);
        color: var(--dark);
    }

    /* HEADER */
    .header {
        background: var(--primary);
        padding: 15px 25px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        color: #fff;
        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    .header img { width: 45px; }

    /* HERO */
    .hero {
        background: url("https://images.unsplash.com/photo-1593560708920-61dd98c46a4e") center/cover no-repeat;
        height: 300px;
        position: relative;
        display: flex;
        align-items: flex-end;
    }

    .overlay {
        background: rgba(0,0,0,0.5);
        width: 100%;
        padding: 30px;
        color: #fff;
    }

    .logo-box {
        background: var(--primary);
        padding: 10px;
        border-radius: 12px;
        display: inline-block;
        margin-bottom: 10px;
    }

    .logo-box img { width: 50px; }

    .btn-hero {
        background: var(--primary);
        padding: 12px 25px;
        border-radius: 30px;
        border: none;
        color: #fff;
        font-weight: bold;
        cursor: pointer;
        transition: 0.3s;
    }

    /* TITULO */
    .titulo-secao {
        text-align: center;
        padding: 30px 20px 10px;
    }

    /* GRID DE 3 COLUNAS */
    .container-cardapio {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 20px;
        padding: 20px;
        max-width: 1200px;
        margin: 0 auto;
    }

    @media (max-width: 992px) {
        .container-cardapio { grid-template-columns: 1fr; }
    }

    .coluna h2 {
        background: var(--dark);
        color: #fff;
        padding: 12px;
        border-radius: 8px;
        text-align: center;
        margin-bottom: 20px;
    }

    /* CARD DE PRODUTO */
    .card {
        background: #fffaf3;
        border-radius: 12px;
        overflow: hidden;
        margin-bottom: 15px;
        box-shadow: 0 4px 10px rgba(0,0,0,0.08);
        display: flex;
        flex-direction: column;
    }

    .card img {
        width: 100%;
        height: 140px;
        object-fit: cover;
    }

    .info {
        padding: 15px;
        flex-grow: 1;
    }

    .info h4 { margin: 0 0 5px; font-size: 1.1rem; }
    .info strong { color: var(--primary); font-size: 1.2rem; }

    .add-btn {
        background: var(--primary);
        color: #fff;
        border: none;
        width: 100%;
        padding: 10px;
        border-radius: 8px;
        cursor: pointer;
        font-weight: bold;
        margin-top: 10px;
    }

    /* AREA DO PEDIDO */
    .pedido-container {
        max-width: 800px;
        margin: 40px auto;
        background: #fffaf3;
        padding: 25px;
        border-radius: 15px;
        border: 2px solid var(--primary);
    }

    input, select {
        width: 100%;
        padding: 12px;
        margin-top: 10px;
        border-radius: 8px;
        border: 1px solid #d6bfa7;
        box-sizing: border-box;
    }

    .linha-endereco {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 15px;
    }

    #pixBox {
        display: none; /* Controlado pelo JS */
        background: #fff3cd;
        padding: 15px;
        border-radius: 8px;
        border-left: 5px solid var(--primary);
        margin-top: 15px;
    }

    .btn-finalizar {
        background: var(--success);
        color: #fff;
        padding: 18px;
        border: none;
        width: 100%;
        border-radius: 10px;
        margin-top: 20px;
        font-size: 1.2rem;
        font-weight: bold;
        cursor: pointer;
    }

    #lista-resumo {
        list-style: none;
        padding: 0;
    }

    #lista-resumo li {
        padding: 8px 0;
        border-bottom: 1px solid #eee;
        display: flex;
        justify-content: space-between;
    }
</style>
</head>
<body>

<div class="header">
    <img src="TODAY-PNG.jpg" alt="Logo">
    <span>Marechal Cândido Rondon - PR</span>
    <div>🛒 Menu</div>
</div>

<div class="hero">
    <div class="overlay">
        <div class="logo-box">
            <img src="TODAY-PNG.jpg" alt="Logo">
        </div>
        <h1>Today Pizza 🍕</h1>
        <p>A melhor massa da região direto na sua casa!</p>
        <button class="btn-hero" onclick="document.getElementById('cardapio').scrollIntoView({behavior:'smooth'})">Ver Cardápio</button>
    </div>
</div>

<div id="cardapio" class="titulo-secao">
    <h2>Nosso Cardápio</h2>
</div>

<div class="container-cardapio">
    <div class="coluna">
        <h2>🍕 Salgadas</h2>
        <div id="lista-salgadas"></div>
    </div>

    <div class="coluna">
        <h2>🍫 Doces</h2>
        <div id="lista-doces"></div>
    </div>

    <div class="coluna">
        <h2>🥤 Bebidas</h2>
        <div id="lista-bebidas"></div>
    </div>
</div>

<div class="pedido-container">
    <h3>🛒 Seu Carrinho</h3>
    <ul id="lista-resumo">
        <p id="carrinho-vazio">O carrinho está vazio...</p>
    </ul>
    <p style="font-size: 1.4rem;"><strong>Total: R$ <span id="total-html">0.00</span></strong></p>

    <hr>

    <h4>📍 Endereço de Entrega (Obrigatório)</h4>
    <input type="text" id="rua" placeholder="Rua / Logradouro">
    <div class="linha-endereco">
        <input type="text" id="numero" placeholder="Número">
        <input type="text" id="bairro" placeholder="Bairro">
    </div>

    <h4>💳 Forma de Pagamento</h4>
    <select id="pagamento-select">
        <option value="PIX">Pix (Pagamento Antecipado)</option>
        <option value="CARTÃO">Cartão na Entrega</option>
        <option value="DINHEIRO">Dinheiro</option>
    </select>

    <div id="pixBox">
        <p><strong>✨ Chave Pix da Today Pizza:</strong></p>
        <h3 style="margin: 5px 0; color: #d97706;">44998905286</h3>
        <small>Envie o comprovante após finalizar no WhatsApp.</small>
    </div>

    <button class="btn-finalizar" onclick="finalizarPedido()">✅ Finalizar no WhatsApp</button>
</div>

<script>
    // DADOS DO CARDÁPIO (10 de cada + bebidas)
    const cardapioData = {
        salgadas: [
            {nome: "Calabresa", preco: 35, img: "https://images.unsplash.com/photo-1604382355076-af4b0eb60143"},
            {nome: "Frango com Catupiry", preco: 38, img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e"},
            {nome: "Portuguesa", preco: 40, img: "https://images.unsplash.com/photo-1601924638867-3ec2b4d2d8b0"},
            {nome: "Margherita", preco: 34, img: "https://images.unsplash.com/photo-1604382354936-07c5d9983bd3"},
            {nome: "4 Queijos", preco: 42, img: "https://images.unsplash.com/photo-1548365328-9f547fb0953d"},
            {nome: "Pepperoni", preco: 41, img: "https://images.unsplash.com/photo-1628840042765-356cda07504e"},
            {nome: "Bacon", preco: 39, img: "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38"},
            {nome: "Moda da Casa", preco: 45, img: "https://images.unsplash.com/photo-1594007654729-407eedc4fe24"},
            {nome: "Lombo", preco: 40, img: "https://images.unsplash.com/photo-1590947132387-155cc02f3212"},
            {nome: "Vegetariana", preco: 38, img: "https://images.unsplash.com/photo-1513104890138-7c749659a591"}
        ],
        doces: [
            {nome: "Chocolate Preto", preco: 35, img: "https://images.unsplash.com/photo-1601924582975-7e6c94b2a8f8"},
            {nome: "Chocolate Branco", preco: 35, img: "https://images.unsplash.com/photo-1613145997970-db84a7975fbb"},
            {nome: "Morango c/ Chocolate", preco: 38, img: "https://images.unsplash.com/photo-1594007654729-407eedc4fe24"},
            {nome: "Banana c/ Canela", preco: 30, img: "https://images.unsplash.com/photo-1585238342024-78d387f4a707"},
            {nome: "Romeu e Julieta", preco: 32, img: "https://images.unsplash.com/photo-1600891964599-f61ba0e24092"},
            {nome: "Prestígio", preco: 34, img: "https://images.unsplash.com/photo-1599785209707-a456fc1337bb"},
            {nome: "Oreo", preco: 37, img: "https://images.unsplash.com/photo-1586985289906-406988974504"},
            {nome: "Doce de Leite", preco: 33, img: "https://images.unsplash.com/photo-1605478909807-3a6c5c2e7f92"},
            {nome: "M&Ms", preco: 36, img: "https://images.unsplash.com/photo-1613145997987-9b1c4e0c6b77"},
            {nome: "Paçoca", preco: 31, img: "https://images.unsplash.com/photo-1617196035154-1e1d7c19e781"}
        ],
        bebidas: [
            {nome: "Coca-Cola 2L", preco: 12, img: "https://images.unsplash.com/photo-1581006852262-e4307cf6283a"},
            {nome: "Guaraná 2L", preco: 10, img: "https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"},
            {nome: "Fanta Laranja 2L", preco: 10, img: "https://images.unsplash.com/photo-1582719478250-c89cae4dc85b"},
            {nome: "Água Mineral", preco: 4, img: "https://images.unsplash.com/photo-1564419320461-6870880221ad"}
        ]
    };

    let carrinho = [];
    let valorTotal = 0;

    // INICIALIZAR CARDÁPIO
    function carregarProdutos() {
        const render = (lista, id) => {
            const div = document.getElementById(id);
            lista.forEach(p => {
                div.innerHTML += `
                    <div class="card">
                        <img src="${p.img}">
                        <div class="info">
                            <h4>${p.nome}</h4>
                            <strong>R$ ${p.preco.toFixed(2)}</strong>
                            <button class="add-btn" onclick="adicionar('${p.nome}', ${p.preco})">Adicionar</button>
                        </div>
                    </div>`;
            });
        };
        render(cardapioData.salgadas, 'lista-salgadas');
        render(cardapioData.doces, 'lista-doces');
        render(cardapioData.bebidas, 'lista-bebidas');
    }

    function adicionar(nome, preco) {
        carrinho.push({nome, preco});
        valorTotal += preco;
        atualizarCarrinho();
    }

    function atualizarCarrinho() {
        const listaUI = document.getElementById("lista-resumo");
        const totalUI = document.getElementById("total-html");
        
        if(carrinho.length > 0) document.getElementById("carrinho-vazio").style.display = "none";
        
        listaUI.innerHTML = "";
        carrinho.forEach(item => {
            listaUI.innerHTML += `<li><span>${item.nome}</span> <span>R$ ${item.preco.toFixed(2)}</span></li>`;
        });
        totalUI.innerText = valorTotal.toFixed(2);
    }

    // LOGICA DO PIX AUTOMÁTICO
    const selectPgto = document.getElementById("pagamento-select");
    const pixBox = document.getElementById("pixBox");

    function verificarPix() {
        pixBox.style.display = selectPgto.value === "PIX" ? "block" : "none";
    }

    selectPgto.addEventListener("change", verificarPix);
    verificarPix(); // Chama ao carregar para garantir se o Pix for o primeiro da lista

    // FINALIZAR E ENVIAR
    function finalizarPedido() {
        const rua = document.getElementById("rua").value;
        const num = document.getElementById("numero").value;
        const bairro = document.getElementById("bairro").value;
        const pgto = selectPgto.value;

        if(carrinho.length === 0) return alert("Seu carrinho está vazio!");
        if(!rua || !num || !bairro) return alert("Por favor, preencha o endereço completo!");

        let mensagem = "🍕 *PEDIDO - TODAY PIZZA* 🍕\n\n";
        carrinho.forEach(i => mensagem += `• ${i.nome}\n`);
        mensagem += `\n💰 *Total:* R$ ${valorTotal.toFixed(2)}`;
        mensagem += `\n💳 *Pagamento:* ${pgto}`;
        if(pgto === "PIX") mensagem += "\n🔑 Chave: 44998905286";
        mensagem += `\n📍 *Endereço:* ${rua}, ${num} - ${bairro}`;
        mensagem += "\n🚚 Marechal Cândido Rondon - PR";

        const whats = "5544998905286";
        const url = `https://wa.me/${whats}?text=${encodeURIComponent(mensagem)}`;

        window.open(url, "_blank");
        alert("✅ PEDIDO CONCLUÍDO COM SUCESSO!");
    }

    carregarProdutos();
</script>

</body>
</html>
