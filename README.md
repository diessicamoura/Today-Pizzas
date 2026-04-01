<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Today Pizza - Delivery</title>

<style>
    :root {
        --primary: #f7931e;
        --bg-light: #fdfdfd;
    }

    body {
        margin: 0;
        font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
        background: var(--bg-light);
    }

    /* BARRA SUPERIOR (HEADER) */
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

    .logo-container-topo {
        background: var(--primary);
        padding: 5px;
        border-radius: 0 0 10px 10px;
        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        margin-top: 15px; /* Faz a logo "vazar" para baixo da barra */
    }

    .logo-container-topo img {
        width: 50px;
        display: block;
    }

    .header-icons {
        display: flex;
        gap: 20px;
        font-size: 1.4rem;
    }

    /* BANNER PRINCIPAL (HERO) */
    .hero {
        background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url("https://images.unsplash.com/photo-1513104890138-7c749659a591") center/cover;
        height: 350px;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        padding: 30px 20px;
        color: white;
    }

    .logo-box-banner {
        background: var(--primary);
        width: 80px;
        height: 80px;
        padding: 8px;
        border-radius: 5px;
        margin-bottom: 15px;
    }

    .logo-box-banner img {
        width: 100%;
        height: 100%;
        object-fit: contain;
    }

    .hero h2 { margin: 0 0 15px; font-size: 1.5rem; line-height: 1.2; }

    .btn-cardapio {
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
    }

    /* SEÇÃO CARDÁPIO */
    .cardapio-header { padding: 30px 20px 10px; }
    .cardapio-header h2 { margin: 0; font-size: 1.8rem; font-family: serif; }
    .cardapio-header p { color: #888; margin: 5px 0; }

    /* BOTÕES DE CATEGORIA (PILLS) */
    .tabs {
        display: flex;
        gap: 10px;
        padding: 10px 20px;
        overflow-x: auto;
    }

    .tab {
        background: #eee;
        padding: 10px 25px;
        border-radius: 25px;
        font-weight: 500;
        cursor: pointer;
        white-space: nowrap;
    }

    .tab.active {
        background: white;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        border: 1px solid #ddd;
    }

    /* LISTA DE PRODUTOS */
    .item-pizza {
        background: white;
        margin: 15px;
        padding: 12px;
        border-radius: 15px;
        display: flex;
        align-items: center;
        box-shadow: 0 2px 8px rgba(0,0,0,0.05);
    }

    .item-pizza img {
        width: 65px;
        height: 65px;
        border-radius: 50%;
        object-fit: cover;
        margin-right: 15px;
    }

    .item-info { flex: 1; }
    .item-info h4 { margin: 0; font-size: 1rem; }
    .item-info p { color: var(--primary); font-weight: bold; margin: 3px 0; }

    .btn-add {
        border: 1px solid #ddd;
        background: white;
        padding: 8px 15px;
        border-radius: 20px;
        font-weight: bold;
        cursor: pointer;
        color: var(--primary);
    }

    /* CHECKOUT */
    .checkout {
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

    .btn-finalizar {
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
</style>
</head>
<body>

<div class="header">
    <div class="logo-container-topo">
        <img src="TODAY-PNG.jpg" alt="Today Pizza">
    </div>
    <div class="header-icons">
        <span>🛒</span>
        <span>☰</span>
    </div>
</div>

<div class="hero">
    <div class="logo-box-banner">
        <img src="TODAY-PNG.jpg" alt="Logo">
    </div>
    <h2>Delivery em Marechal Cândido Rondon - PR 🍕</h2>
    <button class="btn-cardapio" onclick="document.getElementById('cardapio').scrollIntoView({behavior:'smooth'})">
       🍴 Ver Cardápio
    </button>
</div>

<div id="cardapio" class="cardapio-header">
    <h2>Nosso Cardápio</h2>
    <p>Escolha sua pizza favorita</p>
</div>

<div class="tabs">
    <div class="tab active" onclick="mostrar('salgada', this)">Todas</div>
    <div class="tab" onclick="mostrar('salgada', this)">Clássicas</div>
    <div class="tab" onclick="mostrar('doce', this)">Especiais</div>
</div>

<div id="lista-pizzas"></div>

<div class="checkout">
    <h3>🛒 Seu Pedido</h3>
    <ul id="carrinho-lista" style="padding-left: 20px;"></ul>
    <p><strong>Total: R$ <span id="total-valor">0.00</span></strong></p>
    <hr style="border: 0; border-top: 1px solid #eee;">
    <input type="text" id="rua" placeholder="Sua Rua e Número">
    <input type="text" id="bairro" placeholder="Seu Bairro">
    <select id="pagamento">
        <option value="PIX">Pix (Chave: 44998905286)</option>
        <option value="CARTÃO">Cartão na entrega</option>
    </select>
    <button class="btn-finalizar" onclick="finalizar()">Finalizar no WhatsApp</button>
</div>

<script>
    const cardapio = {
        salgada: [
            {nome: "Calabresa Especial", preco: 35, img: "https://images.unsplash.com/photo-1604382355076-af4b0eb60143"},
            {nome: "Frango com Catupiry", preco: 38, img: "https://images.unsplash.com/photo-1593560708920-61dd98c46a4e"},
            {nome: "Portuguesa Clássica", preco: 40, img: "https://images.unsplash.com/photo-1601924638867-3ec2b4d2d8b0"}
        ],
        doce: [
            {nome: "Chocolate com Morango", preco: 35, img: "https://images.unsplash.com/photo-1594007654729-407eedc4fe24"},
            {nome: "Sensação", preco: 36, img: "https://images.unsplash.com/photo-1613145997987-9b1c4e0c6b77"}
        ]
    };

    let itens = [];
    let total = 0;

    function mostrar(cat, btn) {
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        btn.classList.add('active');
        const lista = document.getElementById("lista-pizzas");
        lista.innerHTML = "";
        cardapio[cat].forEach(p => {
            lista.innerHTML += `
            <div class="item-pizza">
                <img src="${p.img}">
                <div class="item-info">
                    <h4>${p.nome}</h4>
                    <p>R$ ${p.preco.toFixed(2)}</p>
                </div>
                <button class="btn-add" onclick="add('${p.nome}', ${p.preco})">Adicionar</button>
            </div>`;
        });
    }

    function add(n, p) {
        itens.push(n);
        total += p;
        const li = document.createElement("li");
        li.innerText = `${n} - R$ ${p.toFixed(2)}`;
        document.getElementById("carrinho-lista").appendChild(li);
        document.getElementById("total-valor").innerText = total.toFixed(2);
    }

    function finalizar() {
        const rua = document.getElementById("rua").value;
        if(itens.length === 0 || !rua) return alert("Selecione itens e informe o endereço!");
        
        let msg = `🍕 *PEDIDO TODAY PIZZA*\n\n${itens.join('\n')}\n\n💰 *Total:* R$ ${total.toFixed(2)}\n📍 *Endereço:* ${rua}\n💳 *Pagamento:* ${document.getElementById("pagamento").value}`;
        window.open(`https://wa.me/5544998905286?text=${encodeURIComponent(msg)}`, "_blank");
        alert("✅ PEDIDO CONCLUÍDO COM SUCESSO!");
    }

    // Iniciar na categoria salgada
    window.onload = () => mostrar('salgada', document.querySelector('.tab'));
</script>

</body>
</html>
