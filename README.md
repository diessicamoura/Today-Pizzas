<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Today Pizza</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #f3f3f3;
}

/* HEADER */
.header {
    background: #f7931e;
    padding: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.header img {
    width: 50px;
}

/* HERO */
.hero {
    background: url("https://images.unsplash.com/photo-1593560708920-61dd98c46a4e") center/cover no-repeat;
    height: 300px;
    position: relative;
}

.overlay {
    position: absolute;
    bottom: 20px;
    left: 20px;
    color: #fff;
}

.logo-box {
    background: #f7931e;
    padding: 10px;
    display: inline-block;
}

.logo-box img {
    width: 60px;
}

.hero h2 {
    margin: 10px 0;
}

.btn {
    background: #f7931e;
    padding: 12px 20px;
    border-radius: 10px;
    border: none;
    font-weight: bold;
    cursor: pointer;
}

/* CARDÁPIO */
.titulo {
    padding: 20px;
}

.tabs {
    display: flex;
    gap: 10px;
    padding: 0 20px;
}

.tab {
    padding: 10px 15px;
    background: #ddd;
    border-radius: 20px;
    cursor: pointer;
}

.tab.active {
    background: #f7931e;
    color: #fff;
}

/* PRODUTOS */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px,1fr));
    gap: 15px;
    padding: 20px;
}

.card {
    background: #fff;
    border-radius: 12px;
    overflow: hidden;
}

.card img {
    width: 100%;
    height: 120px;
    object-fit: cover;
}

.info {
    padding: 10px;
}

.add {
    background: #f7931e;
    color: #fff;
    border: none;
    width: 100%;
    padding: 8px;
    border-radius: 8px;
}

/* PEDIDO */
.pedido {
    background: #fff;
    margin: 20px;
    padding: 20px;
    border-radius: 15px;
    border: 2px solid #f7931e;
}

input, select {
    width: 100%;
    padding: 10px;
    margin-top: 8px;
    border-radius: 8px;
    border: 1px solid #ccc;
}

.linha {
    display: flex;
    gap: 10px;
}

.linha input {
    flex: 1;
}

.finalizar {
    background: #25D366;
    color: #fff;
    padding: 15px;
    border: none;
    width: 100%;
    border-radius: 10px;
    margin-top: 15px;
    font-weight: bold;
}
</style>
</head>

<body>

<!-- HEADER -->
<div class="header">
    <img src="logo.png">
    🛒 ☰
</div>

<!-- HERO -->
<div class="hero">
    <div class="overlay">
        <div class="logo-box">
            <img src="logo.png">
        </div>
        <h2>Delivery em Marechal Cândido Rondon - PR 🍕</h2>
        <button class="btn" onclick="scrollCardapio()">🍴 Ver Cardápio</button>
    </div>
</div>

<!-- CARDÁPIO -->
<div id="cardapio">
<div class="titulo">
    <h2>Nosso Cardápio</h2>
    <p>Escolha sua pizza favorita</p>
</div>

<div class="tabs">
    <div class="tab active" onclick="trocar('salgada')">Salgadas</div>
    <div class="tab" onclick="trocar('doce')">Doces</div>
    <div class="tab" onclick="trocar('bebida')">Bebidas</div>
</div>

<div class="grid" id="produtos"></div>
</div>

<!-- PEDIDO -->
<div class="pedido">
<h3>🛒 Seu Pedido</h3>
<ul id="lista"></ul>

<p><strong>Total: R$ <span id="total">0.00</span></strong></p>

<hr>

<h4>📍 Dados para Entrega</h4>
<input type="text" id="rua" placeholder="Rua (Obrigatório)">

<div class="linha">
    <input type="text" id="numero" placeholder="Nº">
    <input type="text" id="bairro" placeholder="Bairro">
</div>

<h4>💳 Pagamento</h4>
<select id="pagamento">
<option value="PIX">Pix</option>
<option value="Cartão">Cartão na entrega</option>
</select>

<button class="finalizar" onclick="finalizar()">Finalizar Pedido pelo WhatsApp</button>
</div>

<script>
let produtos = {
    salgada: [
        {nome:"🔥 Combo Família (Calabresa + Coca 2L)", preco:49, destaque:true, img:"https://altoastral.joaobidu.com.br/antigas/uploads/legacy/2016/07/AAT001-P001-89335-1-m-Divulgacao_1.jpg"},
        {nome:"⭐ Calabresa Especial", preco:35, destaque:true, img:"https://images.unsplash.com/photo-1604382355076-af4b0eb60143"},
        {nome:"⭐ Frango Cremoso com Catupiry", preco:38, destaque:true, img:"https://images.unsplash.com/photo-1593560708920-61dd98c46a4e"},
        {nome:"Pepperoni Premium", preco:41, img:"https://images.unsplash.com/photo-1628840042765-356cda07504e"},
        {nome:"Quatro Queijos Supreme", preco:42, img:"https://images.unsplash.com/photo-1548365328-9f547fb0953d"},
        {nome:"Moda da Casa Completa", preco:45, img:"https://images.unsplash.com/photo-1594007654729-407eedc4fe24"},
        {nome:"Bacon Lovers", preco:39, img:"https://images.unsplash.com/photo-1565299624946-b28f40a0ae38"},
        {nome:"Portuguesa Tradicional", preco:40, img:"https://images.unsplash.com/photo-1601924638867-3ec2b4d2d8b0"},
        {nome:"Marguerita Italiana", preco:34, img:"https://images.unsplash.com/photo-1604382354936-07c5d9983bd3"},
        {nome:"Carne Seca Especial", preco:44, img:"https://images.unsplash.com/photo-1590947132387-155cc02f3212"}
    ],

    doce: [
        {nome:"🔥 Combo Doce (Chocolate + Guaraná)", preco:39, destaque:true, img:"https://images.unsplash.com/photo-1601924582975-7e6c94b2a8f8"},
        {nome:"⭐ Chocolate com Morango", preco:35, destaque:true, img:"https://images.unsplash.com/photo-1594007654729-407eedc4fe24"},
        {nome:"⭐ Sensação Premium", preco:36, destaque:true, img:"https://images.unsplash.com/photo-1613145997987-9b1c4e0c6b77"},
        {nome:"Nutella Supreme", preco:38, img:"https://images.unsplash.com/photo-1613145997970-db84a7975fbb"},
        {nome:"Chocolate Branco Especial", preco:34, img:"https://images.unsplash.com/photo-1617196035154-1e1d7c19e781"},
        {nome:"Doce de Leite Cremoso", preco:33, img:"https://images.unsplash.com/photo-1605478909807-3a6c5c2e7f92"},
        {nome:"Prestígio", preco:32, img:"https://images.unsplash.com/photo-1599785209707-a456fc1337bb"},
        {nome:"Banana Nevada", preco:28, img:"https://images.unsplash.com/photo-1585238342024-78d387f4a707"},
        {nome:"Romeu e Julieta", preco:31, img:"https://images.unsplash.com/photo-1600891964599-f61ba0e24092"},
        {nome:"Oreo", preco:37, img:"https://images.unsplash.com/photo-1586985289906-406988974504"}
    ],

    bebida: [
        {nome:"⭐ Coca-Cola 2L (Mais pedida)", preco:12, destaque:true, img:"https://images.unsplash.com/photo-1581006852262-e4307cf6283a"},
        {nome:"Guaraná 2L", preco:10, img:"https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"},
        {nome:"Fanta Laranja", preco:10, img:"https://images.unsplash.com/photo-1582719478250-c89cae4dc85b"},
        {nome:"Sprite", preco:10, img:"https://images.unsplash.com/photo-1624517452488-04869289c4ca"},
        {nome:"Coca-Cola Lata", preco:6, img:"https://images.unsplash.com/photo-1582719478250-c89cae4dc85b"},
        {nome:"Guaraná Lata", preco:5, img:"https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"},
        {nome:"Água Mineral", preco:4, img:"https://images.unsplash.com/photo-1564419320461-6870880221ad"},
        {nome:"Suco Natural de Laranja", preco:8, img:"https://images.unsplash.com/photo-1572490122747-3968b75cc699"},
        {nome:"Suco de Uva", preco:8, img:"https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"},
        {nome:"Refrigerante 600ml", preco:7, img:"https://images.unsplash.com/photo-1581006852262-e4307cf6283a"}
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
        <div class="card">
            <img src="${p.img}">
            <div class="info">
                <h4>
${p.nome} 
${p.destaque ? '<span style="color:#f7931e;font-size:12px;">★</span>' : ''}
</h4>
                <strong>R$ ${p.preco}</strong>
                <button class="add" onclick="add('${p.nome}',${p.preco})">
➕ Adicionar
</button>
            </div>
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

    carrinho.forEach(i=>{
        msg += "• " + i.nome + "\n";
    });

    msg += "\n💰 Total: R$ " + total.toFixed(2);
    msg += "\n📍 Endereço: " + rua + ", " + numeroCasa + " - " + bairro;
    msg += "\n💳 Pagamento: " + pagamento;
    msg += "\n🚚 Marechal Cândido Rondon - PR";

    let numero = "5544998905286"; // SEU NUMERO

    let url = "https://wa.me/" + numero + "?text=" + encodeURIComponent(msg);

    window.open(url, "_blank");
}

function scrollCardapio(){
    document.getElementById("cardapio").scrollIntoView({behavior:"smooth"});
}

trocar('salgada');
</script>

</body>
</html>
