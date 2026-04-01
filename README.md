<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Today Pizza - Marechal Cândido Rondon</title>

<style>
    :root {
        --primary: #f7931e;
        --bg-light: #fdfdfd;
        --text-dark: #333;
    }

    body {
        margin: 0;
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
        background: var(--bg-light);
        color: var(--text-dark);
    }

    /* HEADER */
    .header {
        background: var(--primary);
        height: 60px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 20px;
        position: sticky;
        top: 0;
        z-index: 1000;
    }

    .logo-header {
        background: var(--primary);
        padding: 5px;
        border-radius: 0 0 10px 10px;
        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        margin-top: 15px;
    }

    .logo-header img { width: 55px; display: block; border-radius: 5px; }

    .header-icons {
        display: flex;
        gap: 20px;
        color: #333;
        font-size: 1.4rem;
    }

    /* HERO/BANNER */
    .hero {
        background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url("https://images.unsplash.com/photo-1593560708920-61dd98c46a4e") center/cover;
        height: 350px;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        padding: 30px 20px;
        color: white;
    }

    .hero-logo-box {
        background: var(--primary);
        width: 70px;
        height: 70px;
        padding: 5px;
        border-radius: 5px;
        margin-bottom: 15px;
    }

    .hero-logo-box img { width: 100%; height: 100%; object-fit: cover; border-radius: 3px; }

    .hero h2 { margin: 0 0 15px; font-size: 1.5rem; line-height: 1.2; }

    .btn-ver-cardapio {
        background: var(--primary);
        color: #333;
        border: none;
        padding: 12px 25px;
        border-radius: 12px;
        font-weight: bold;
        cursor: pointer;
        display: flex;
        align-items: center;
        gap: 10px;
        width: fit-content;
    }

    /* SEÇÃO CARDÁPIO */
    .cardapio-info { padding: 30px 20px 10px; }
    .cardapio-info h2 { margin: 0; font-size: 1.8rem; }
    .cardapio-info p { color: #888; margin: 5px 0; }

    /* ABAS (PILLS) */
    .tabs {
        display: flex;
        gap: 10px;
        padding: 10px 20px;
        overflow-x: auto;
    }

    .tab {
        background: #eee;
        color: #666;
        padding: 10px 25px;
        border-radius: 25px;
        font-weight: 500;
        cursor: pointer;
        white-space: nowrap;
    }

    .tab.active {
        background: white;
        color: #333;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        border: 1px solid #ddd;
    }

    /* LISTA DE PRODUTOS */
    .pizza-list { padding: 15px; min-height: 200px; }

    .card-pizza {
        background: white;
        margin-bottom: 12px;
        padding: 12px;
        border-radius: 15px;
        display: flex;
        align-items: center;
        box-shadow: 0 2px 8px rgba(0,0,0,0.05);
    }

    .card-pizza img {
        width: 65px;
        height: 65px;
        border-radius: 50%;
        object-fit: cover;
        margin-right: 15px;
    }

    .card-info { flex: 1; }
    .card-info h4 { margin: 0; font-size: 1rem; }
    .card-info span { color: var(--primary); font-weight: bold; }

    .btn-add {
        border: 1px solid #ddd;
        background: white;
        padding: 6px 12px;
        border-radius: 20px;
        font-weight: bold;
        cursor: pointer;
        color: var(--primary);
    }

    /* CHECKOUT */
    .checkout-container {
        margin: 20px;
        padding: 20px;
        background: white;
        border-radius: 15px;
        box-shadow: 0 4px 20px rgba(0,0,0,0.08);
    }

    input, select {
        width: 100%;
        padding: 14px;
        margin-top: 10px;
        border: 1px solid #eee;
        border-radius: 10px;
        box-sizing: border-box;
    }

    .finalizar-btn {
        background: #16a34a;
        color: white;
        width: 100%;
        padding: 18px;
        border: none;
        border-radius: 12px;
        font-weight: bold;
        font-size: 1.1rem;
        margin-top: 20px;
        cursor: pointer;
    }

    #pixBox {
        display: none;
        background: #fff9e6;
        padding: 15px;
        border-radius: 10px;
        margin-top: 15px;
        border: 1px solid #ffeeba;
    }
</style>
</head>
<body>

<div class="header">
    <div class="logo-header">
        <img src="TODAY-PNG.jpg" alt="Logo">
    </div>
    <div class="header-icons">
        <span>🛒</span>
        <span>☰</span>
    </div>
</div>

<div class="hero">
    <div class="hero-logo-box">
        <img src="TODAY-PNG.jpg" alt="Logo">
    </div>
    <h2>Delivery em Marechal Cândido Rondon - PR 🍕</h2>
    <button class="btn-ver-cardapio" onclick="document.getElementById('nosso-cardapio').scrollIntoView({behavior:'smooth'})">
       🍴 Ver Cardápio
    </button>
</div>

<div id="nosso-cardapio" class="cardapio-info">
    <h2>Nosso Cardápio</h2>
    <p>Escolha sua pizza favorita</p>
</div>

<div class="tabs">
    <div class="tab active" onclick="trocarCategoria('salgada', this)">Salgadas</div>
    <div class="tab" onclick="trocarCategoria('doce', this)">Doces</div>
    <div class="tab" onclick="trocarCategoria('bebida', this)">Bebidas</div>
</div>

<div class="pizza-list" id="lista-produtos"></div>

<div class="checkout-container">
    <h3>🛒 Seu Pedido</h3>
    <ul id="resumo-pedido" style="padding-left: 20px; color: #555;"></ul>
    <p><strong>Total: R$ <span id="valor-total">0.00</span></strong></p>

    <hr style="border: 0; border-top: 1px solid #eee; margin: 20px 0;">

    <h4>📍 Endereço</h4>
    <input type="text" id="rua" placeholder="Rua">
    <div style="display: flex; gap: 10px;">
        <input type="text" id="numero" placeholder="Número">
        <input type="text" id="bairro" placeholder="Bairro">
    </div>

    <h4>💳 Pagamento</h4>
    <select id="metodo-pagamento" onchange="togglePix()">
        <option value="PIX">Pix</option>
        <option value="Cartão">Cartão na entrega</option>
    </select>

    <div id="pixBox">
        <strong>💸 Chave Pix:</strong> 44998905286
    </div>

    <button class="finalizar-btn" onclick="enviarPedido()">Finalizar no WhatsApp</button>
</div>

<script>
    const itensCardapio = {
        salgada: [
            {nome: "Calabresa Especial", preco: 35, img: "https://images.unsplash.com/photo-1604382355076-af4b0eb60143"},
            {nome: "Frango com Catupiry", preco: 38, img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e"},
            {nome: "Portuguesa", preco: 40, img: "https://images.unsplash.com/photo-1601924638867-3ec2b4d2d8b0"},
            {nome: "Margherita", preco: 34, img: "https://images.unsplash.com/photo-1604382354936-07c5d9983bd3"},
            {nome: "Quatro Queijos", preco: 42, img: "https://images.unsplash.com/photo-1548365328-9f547fb0953d"},
            {nome: "Pepperoni", preco: 41, img: "https://images.unsplash.com/photo-1628840042765-356cda07504e"},
            {nome: "Bacon Lovers", preco: 39, img: "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38"},
            {nome: "Moda da Casa", preco: 45, img: "https://images.unsplash.com/photo-1594007654729-407eedc4fe24"},
            {nome: "Carne Seca", preco: 44, img: "https://images.unsplash.com/photo-1590947132387-155cc02f3212"},
            {nome: "Vegetariana", preco: 38, img: "https://images.unsplash.com/photo-1513104890138-7c749659a591"}
        ],
        doce: [
            {nome: "Chocolate com Morango", preco: 35, img: "https://images.unsplash.com/photo-1594007654729-407eedc4fe24"},
            {nome: "Sensação Premium", preco: 36, img: "https://images.unsplash.com/photo-1613145997987-9b1c4e0c6b77"},
            {nome: "Nutella Supreme", preco: 38, img: "https://images.unsplash.com/photo-1613145997970-db84a7975fbb"},
            {nome: "Banana Nevada", preco: 28, img: "https://images.unsplash.com/photo-1585238342024-78d387f4a707"},
            {nome: "Romeu e Julieta", preco: 31, img: "https://images.unsplash.com/photo-1600891964599-f61ba0e24092"},
            {nome: "Oreo", preco: 37, img: "https://images.unsplash.com/photo-1586985289906-406988974504"},
            {nome: "Chocolate Branco", preco: 34, img: "https://images.unsplash.com/photo-1617196035154-1e1d7c19e781"},
            {nome: "Doce de Leite", preco: 33, img: "https://images.unsplash.com/photo-1605478909807-3a6c5c2e7f92"},
            {nome: "Prestígio", preco: 32, img: "https://images.unsplash.com/photo-1599785209707-a456fc1337bb"},
            {nome: "Confete", preco: 34, img: "https://images.unsplash.com/photo-1613145997987-9b1c4e0c6b77"}
        ],
        bebida: [
            {nome: "Coca-Cola 2L", preco: 12, img: "https://images.unsplash.com/photo-1581006852262-e4307cf6283a"},
            {nome: "Guaraná 2L", preco: 10, img: "https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"},
            {nome: "Fanta Laranja 2L", preco: 10, img: "https://images.unsplash.com/photo-1582719478250-c89cae4dc85b"},
            {nome: "Sprite 2L", preco: 10, img: "https://images.unsplash.com/photo-1624517452488-04869289c4ca"},
            {nome: "Coca Lata", preco: 6, img: "https://images.unsplash.com/photo-1582719478250-c89cae4dc85b"},
            {nome: "Guaraná Lata", preco: 5, img: "https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"},
            {nome: "Água Mineral", preco: 4, img: "https://images.unsplash.com/photo-1564419320461-6870880221ad"},
            {nome: "Suco Laranja", preco: 8, img: "https://images.unsplash.com/photo-1572490122747-3968b75cc699"},
            {nome: "Suco Uva", preco: 8, img: "https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"},
            {nome: "Refri 600ml", preco: 7, img: "https://images.unsplash.com/photo-1581006852262-e4307cf6283a"}
        ]
    };

    let carrinho = [];
    let totalSoma = 0;

    function trocarCategoria(categoria, elemento) {
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        elemento.classList.add('active');

        const container = document.getElementById("lista-produtos");
        container.innerHTML = "";

        itensCardapio[categoria].forEach(p => {
            container.innerHTML += `
            <div class="card-pizza">
                <img src="${p.img}">
                <div class="card-info">
                    <h4>${p.nome}</h4>
                    <span>R$ ${p.preco.toFixed(2)}</span>
                </div>
                <button class="btn-add" onclick="adicionarAoCarrinho('${p.nome}', ${p.preco})">Adicionar</button>
            </div>`;
        });
    }

    function adicionarAoCarrinho(nome, preco) {
        carrinho.push({nome, preco});
        totalSoma += preco;
        
        const lista = document.getElementById("resumo-pedido");
        const li = document.createElement("li");
        li.innerText = `${nome} - R$ ${preco.toFixed(2)}`;
        lista.appendChild(li);
        
        document.getElementById("valor-total").innerText = totalSoma.toFixed(2);
    }

    function togglePix() {
        const met = document.getElementById("metodo-pagamento").value;
        document.getElementById("pixBox").style.display = met === "PIX" ? "block" : "none";
    }

    function enviarPedido() {
        const rua = document.getElementById("rua").value;
        const num = document.getElementById("numero").value;
        const bairro = document.getElementById("bairro").value;
        const pgto = document.getElementById("metodo-pagamento").value;

        if(carrinho.length === 0 || !rua) {
            alert("Selecione os produtos e preencha o endereço!");
            return;
        }

        let mensagem = "🍕 *PEDIDO TODAY PIZZA* 🍕\n\n";
        carrinho.forEach(i => mensagem += `• ${i.nome}\n`);
        mensagem += `\n💰 *Total:* R$ ${totalSoma.toFixed(2)}`;
        mensagem += `\n📍 *Endereço:* ${rua}, ${num} - ${bairro}`;
        mensagem += `\n💳 *Pagamento:* ${pgto}`;
        if(pgto === "PIX") mensagem += "\n🔑 Chave: 44998905286";
        
        const fone = "5544998905286";
        const url = `https://wa.me/${fone}?text=${encodeURIComponent(mensagem)}`;
        window.open(url, "_blank");
        alert("✅ PEDIDO CONCLUÍDO COM SUCESSO!");
    }

    // Inicialização
    window.onload = () => {
        trocarCategoria('salgada', document.querySelector('.tab'));
        togglePix();
    };
</script>

</body>
</html>
