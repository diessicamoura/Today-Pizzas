<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Today Pizza</title>

<style>
    :root {
        --primary: #f7931e;
        --dark: #333;
        --grey-light: #f4f4f4;
        --white: #ffffff;
    }

    body {
        margin: 0;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background: #f9f9f9;
        color: var(--dark);
    }

    /* HEADER - Estilo Foto 2 */
    .header {
        background: var(--white);
        height: 70px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 20px;
        box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        position: sticky;
        top: 0;
        z-index: 100;
    }

    .logo-header {
        background: var(--primary);
        padding: 10px;
        border-radius: 0 0 15px 15px;
        margin-top: -10px;
    }

    .logo-header img { width: 50px; }

    /* HERO - Estilo Foto 2 */
    .hero {
        background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url("https://images.unsplash.com/photo-1593560708920-61dd98c46a4e") center/cover;
        height: 300px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        color: var(--white);
        text-align: center;
        padding: 20px;
    }

    .hero h2 { margin-bottom: 20px; font-size: 1.5rem; }

    .btn-ver-cardapio {
        background: var(--primary);
        color: var(--white);
        border: none;
        padding: 12px 25px;
        border-radius: 25px;
        font-weight: bold;
        cursor: pointer;
        display: flex;
        align-items: center;
        gap: 8px;
    }

    /* TABS / ABAS - Estilo Foto 2 */
    .tabs-container {
        padding: 20px;
        text-align: center;
    }

    .tabs {
        display: flex;
        gap: 10px;
        justify-content: center;
        overflow-x: auto;
        padding-bottom: 10px;
    }

    .tab {
        background: #eee;
        padding: 8px 20px;
        border-radius: 20px;
        cursor: pointer;
        font-weight: 500;
        white-space: nowrap;
    }

    .tab.active {
        background: var(--primary);
        color: var(--white);
    }

    /* LISTA DE PRODUTOS - Estilo Foto 2 (Horizontal com foto redonda) */
    .produtos-list {
        max-width: 600px;
        margin: 0 auto;
        padding: 0 15px;
    }

    .card-item {
        background: var(--white);
        margin-bottom: 12px;
        padding: 12px;
        border-radius: 15px;
        display: flex;
        align-items: center;
        box-shadow: 0 2px 8px rgba(0,0,0,0.04);
    }

    .card-item img {
        width: 65px;
        height: 65px;
        border-radius: 50%;
        object-fit: cover;
        margin-right: 15px;
    }

    .info { flex: 1; }
    .info h4 { margin: 0; font-size: 1rem; }
    .info p { margin: 3px 0; font-weight: bold; color: var(--primary); }

    .btn-add {
        background: transparent;
        border: 2px solid var(--primary);
        color: var(--primary);
        padding: 5px 15px;
        border-radius: 15px;
        font-weight: bold;
        cursor: pointer;
    }

    /* CARRINHO E FORMULÁRIO */
    .pedido-box {
        background: var(--white);
        margin: 20px;
        padding: 20px;
        border-radius: 20px;
        box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        max-width: 600px;
        margin: 20px auto;
    }

    input, select {
        width: 100%;
        padding: 12px;
        margin: 8px 0;
        border-radius: 10px;
        border: 1px solid #ddd;
        box-sizing: border-box;
    }

    .linha { display: flex; gap: 10px; }

    #pixBox {
        display: none;
        background: #fff3cd;
        padding: 15px;
        border-radius: 10px;
        margin-top: 10px;
        border-left: 5px solid var(--primary);
    }

    .finalizar {
        background: #16a34a;
        color: #fff;
        padding: 15px;
        border: none;
        width: 100%;
        border-radius: 12px;
        font-weight: bold;
        font-size: 1.1rem;
        cursor: pointer;
        margin-top: 15px;
    }
</style>
</head>
<body>

<div class="header">
    <div class="logo-header">
        <img src="TODAY-PNG.jpg" alt="Logo">
    </div>
    <div style="font-size: 1.2rem;">🛒 ☰</div>
</div>

<div class="hero">
    <h2>Delivery em Marechal Cândido Rondon - PR 🍕</h2>
    <button class="btn-ver-cardapio" onclick="document.getElementById('cardapio-titulo').scrollIntoView({behavior:'smooth'})">
        🍴 Ver Cardápio
    </button>
</div>

<div id="cardapio-titulo" style="padding: 20px 20px 0;">
    <h2 style="margin: 0;">Nosso Cardápio</h2>
    <p style="color: #666; margin: 5px 0 0;">Escolha sua pizza favorita</p>
</div>

<div class="tabs-container">
    <div class="tabs">
        <div class="tab active" onclick="trocar('salgada')">Salgadas</div>
        <div class="tab" onclick="trocar('doce')">Doces</div>
        <div class="tab" onclick="trocar('bebida')">Bebidas</div>
    </div>
</div>

<div class="produtos-list" id="produtos"></div>

<div class="pedido-box">
    <h3>🛒 Seu Pedido</h3>
    <ul id="lista" style="padding-left: 20px;"></ul>
    <p><strong>Total: R$ <span id="total">0.00</span></strong></p>

    <hr>
    <h4>📍 Endereço</h4>
    <input type="text" id="rua" placeholder="Rua">
    <div class="linha">
        <input type="text" id="numero" placeholder="Número">
        <input type="text" id="bairro" placeholder="Bairro">
    </div>

    <h4>💳 Pagamento</h4>
    <select id="pagamento" onchange="verificarPix()">
        <option value="PIX">Pix</option>
        <option value="Cartão">Cartão na entrega</option>
    </select>

    <div id="pixBox">
        <strong>💸 Chave Pix:</strong><br>
        44998905286
    </div>

    <button class="finalizar" onclick="finalizar()">Finalizar no WhatsApp</button>
</div>

<script>
// DADOS ORIGINAIS (10 ITENS POR CATEGORIA)
let produtos = {
    salgada: [ 
        {nome:"🔥 Combo Família (Calabresa + Coca 2L)", preco:49, img:"https://altoastral.joaobidu.com.br/antigas/uploads/legacy/2016/07/AAT001-P001-89335-1-m-Divulgacao_1.jpg"}, 
        {nome:"⭐ Calabresa Especial", preco:35, img:"https://images.unsplash.com/photo-1604382355076-af4b0eb60143"}, 
        {nome:"⭐ Frango com Catupiry", preco:38, img:"https://images.unsplash.com/photo-1593560708920-61dd98c46a4e"}, 
        {nome:"Pepperoni Premium", preco:41, img:"https://images.unsplash.com/photo-1628840042765-356cda07504e"}, 
        {nome:"Quatro Queijos", preco:42, img:"https://images.unsplash.com/photo-1548365328-9f547fb0953d"}, 
        {nome:"Moda da Casa", preco:45, img:"https://images.unsplash.com/photo-1594007654729-407eedc4fe24"}, 
        {nome:"Bacon", preco:39, img:"https://images.unsplash.com/photo-1565299624946-b28f40a0ae38"}, 
        {nome:"Portuguesa", preco:40, img:"https://images.unsplash.com/photo-1601924638867-3ec2b4d2d8b0"}, 
        {nome:"Marguerita", preco:34, img:"https://images.unsplash.com/photo-1604382354936-07c5d9983bd3"}, 
        {nome:"Carne Seca", preco:44, img:"https://images.unsplash.com/photo-1590947132387-155cc02f3212"} 
    ], 
    doce: [ 
        {nome:"🔥 Combo Doce", preco:39, img:"https://images.unsplash.com/photo-1601924582975-7e6c94b2a8f8"}, 
        {nome:"⭐ Chocolate com Morango", preco:35, img:"https://images.unsplash.com/photo-1594007654729-407eedc4fe24"}, 
        {nome:"⭐ Sensação", preco:36, img:"https://images.unsplash.com/photo-1613145997987-9b1c4e0c6b77"}, 
        {nome:"Nutella", preco:38, img:"https://images.unsplash.com/photo-1613145997970-db84a7975fbb"}, 
        {nome:"Chocolate Branco", preco:34, img:"https://images.unsplash.com/photo-1617196035154-1e1d7c19e781"}, 
        {nome:"Doce de Leite", preco:33, img:"https://images.unsplash.com/photo-1605478909807-3a6c5c2e7f92"}, 
        {nome:"Prestígio", preco:32, img:"https://images.unsplash.com/photo-1599785209707-a456fc1337bb"}, 
        {nome:"Banana Nevada", preco:28, img:"https://images.unsplash.com/photo-1585238342024-78d387f4a707"}, 
        {nome:"Romeu e Julieta", preco:31, img:"https://images.unsplash.com/photo-1600891964599-f61ba0e24092"}, 
        {nome:"Oreo", preco:37, img:"https://images.unsplash.com/photo-1586985289906-406988974504"} 
    ], 
    bebida: [ 
        {nome:"Coca-Cola 2L", preco:12, img:"https://images.unsplash.com/photo-1581006852262-e4307cf6283a"}, 
        {nome:"Guaraná 2L", preco:10, img:"https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"}, 
        {nome:"Fanta Laranja", preco:10, img:"https://images.unsplash.com/photo-1582719478250-c89cae4dc85b"}, 
        {nome:"Sprite", preco:10, img:"https://images.unsplash.com/photo-1624517452488-04869289c4ca"}, 
        {nome:"Coca Lata", preco:6, img:"https://images.unsplash.com/photo-1582719478250-c89cae4dc85b"}, 
        {nome:"Guaraná Lata", preco:5, img:"https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"}, 
        {nome:"Água", preco:4, img:"https://images.unsplash.com/photo-1564419320461-6870880221ad"}, 
        {nome:"Suco Laranja", preco:8, img:"https://images.unsplash.com/photo-1572490122747-3968b75cc699"}, 
        {nome:"Suco Uva", preco:8, img:"https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"}, 
        {nome:"Refri 600ml", preco:7, img:"https://images.unsplash.com/photo-1581006852262-e4307cf6283a"} 
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
        lista.innerHTML += `
        <div class="card-item">
            <img src="${p.img}">
            <div class="info">
                <h4>${p.nome}</h4>
                <p>R$ ${p.preco.toFixed(2)}</p>
            </div>
            <button class="btn-add" onclick="add('${p.nome}',${p.preco})">Adicionar</button>
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

function verificarPix() {
    let pgto = document.getElementById("pagamento").value;
    document.getElementById("pixBox").style.display = pgto === "PIX" ? "block" : "none";
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
    if(pagamento === "PIX") msg += "\n💸 Chave Pix: 44998905286";
    msg += "\n🚚 Marechal Cândido Rondon - PR";

    let numeroWhats = "5544998905286";
    let url = "https://wa.me/" + numeroWhats + "?text=" + encodeURIComponent(msg);
    window.open(url, "_blank");
    alert("✅ PEDIDO CONCLUÍDO COM SUCESSO!");
}

verificarPix();
trocar('salgada');
</script>
</body>
</html>
