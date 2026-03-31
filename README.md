<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Today Pizza</title>

<style>
body {
    margin: 0;
    font-family: Arial;
    background: #f5f5f5;
}

/* TOPO */
.hero {
    background: #fff;
    display: flex;
    align-items: center;
    padding: 15px;
    border-bottom: 1px solid #ddd;
}

.logo img {
    width: 60px;
}

.hero-text {
    margin-left: 10px;
}

/* ALERTA */
.alerta {
    text-align: center;
    padding: 10px;
    font-weight: bold;
    background: #fff;
}

/* ABAS */
.tabs {
    display: flex;
    justify-content: space-around;
    background: #fff;
    border-bottom: 1px solid #ddd;
}

.tab {
    padding: 12px;
    cursor: pointer;
    font-weight: bold;
}

.tab.active {
    color: #f7931e;
    border-bottom: 3px solid #f7931e;
}

/* PRODUTOS */
.produtos {
    padding: 15px;
}

.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px,1fr));
    gap: 15px;
}

.card {
    background: #fff;
    border-radius: 10px;
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

button {
    background: #f7931e;
    color: #fff;
    border: none;
    padding: 8px;
    width: 100%;
    border-radius: 6px;
}

/* CARRINHO */
.carrinho {
    position: fixed;
    right: 0;
    top: 0;
    width: 250px;
    height: 100%;
    background: #fff;
    border-left: 1px solid #ddd;
    padding: 15px;
    overflow-y: auto;
}

@media(max-width: 800px){
    .carrinho {
        width: 100%;
        height: auto;
        bottom: 0;
        top: auto;
    }
}

input, select {
    width: 100%;
    padding: 8px;
    margin-top: 8px;
}

.finalizar {
    margin-top: 10px;
}
</style>
</head>

<body>

<div class="hero">
    <div class="logo">
        <img src="logo.png">
    </div>
    <div class="hero-text">
        <h2>Today Pizza</h2>
        <p>Delivery Marechal Cândido Rondon - PR</p>
    </div>
</div>

<div class="alerta">
🚚 Apenas entregas
</div>

<!-- ABAS -->
<div class="tabs">
    <div class="tab active" onclick="trocar('salgada')">🍕 Salgadas</div>
    <div class="tab" onclick="trocar('doce')">🍫 Doces</div>
    <div class="tab" onclick="trocar('bebida')">🥤 Bebidas</div>
</div>

<!-- PRODUTOS -->
<div class="produtos">
    <div id="listaProdutos" class="grid"></div>
</div>

<!-- CARRINHO -->
<div class="carrinho">
<h3>Carrinho</h3>
<ul id="lista"></ul>

<strong>Total: R$ <span id="total">0</span></strong>

<input type="text" id="endereco" placeholder="Digite seu endereço">

<select id="pagamento">
<option value="pix">PIX</option>
<option value="cartao">Cartão na entrega</option>
</select>

<button class="finalizar" onclick="finalizarPedido()">Finalizar</button>
</div>

<script>
let produtos = {
    salgada: [
        {nome:"Calabresa", preco:35, img:"https://images.unsplash.com/photo-1604382355076-af4b0eb60143"},
        {nome:"Frango com Catupiry", preco:38, img:"https://images.unsplash.com/photo-1593560708920-61dd98c46a4e"}
    ],
    doce: [
        {nome:"Chocolate", preco:30, img:"https://images.unsplash.com/photo-1601924582975-7e6c94b2a8f8"},
        {nome:"Morango com Chocolate", preco:35, img:"https://images.unsplash.com/photo-1594007654729-407eedc4fe24"}
    ],
    bebida: [
        {nome:"Coca-Cola 2L", preco:12, img:"https://images.unsplash.com/photo-1581006852262-e4307cf6283a"},
        {nome:"Guaraná 2L", preco:10, img:"https://images.unsplash.com/photo-1577801598627-ff2a44d88b41"}
    ]
};

let carrinho = [];
let total = 0;

function trocar(tipo){
    document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
    event.target.classList.add('active');

    let lista = document.getElementById("listaProdutos");
    lista.innerHTML = "";

    produtos[tipo].forEach(p => {
        lista.innerHTML += `
        <div class="card">
            <img src="${p.img}">
            <div class="info">
                <h4>${p.nome}</h4>
                <strong>R$ ${p.preco}</strong>
                <button onclick="add('${p.nome}',${p.preco})">Adicionar</button>
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

function finalizarPedido(){
    let endereco = document.getElementById("endereco").value;

    if(carrinho.length === 0 || endereco === ""){
        alert("Preencha tudo!");
        return;
    }

    let pagamento = document.getElementById("pagamento").value;

    let msg = "🍕 *TODAY PIZZA* 🍕\n\n";

    carrinho.forEach(i=>{
        msg += "• " + i.nome + "\n";
    });

    msg += "\n💰 Total: R$ " + total.toFixed(2);
    msg += "\n📍 Endereço: " + endereco;
    msg += "\n💳 Pagamento: " + pagamento;

    let numero = "5599999999999"; // SEU NUMERO

    let url = "https://wa.me/" + numero + "?text=" + encodeURIComponent(msg);

    window.open(url, "_blank");
}

/* CARREGA INICIAL */
trocar('salgada');
</script>

</body>
</html>
