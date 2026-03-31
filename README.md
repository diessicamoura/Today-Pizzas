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
    background: #f5f5f5;
    color: #333;
}

/* HERO */
.hero {
    background: url("https://images.unsplash.com/photo-1593560708920-61dd98c46a4e") center/cover no-repeat;
    height: 220px;
}

.overlay {
    background: rgba(255,255,255,0.75);
    height: 100%;
    display: flex;
    align-items: center;
    padding: 20px;
}

.logo {
    width: 70px;
    height: 70px;
    background: #f7931e;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.logo img {
    width: 55px;
}

.hero-text {
    margin-left: 15px;
}

.hero-text h1 {
    margin: 0;
}

.hero-text p {
    margin: 5px 0 0;
    color: #555;
}

/* ALERTA */
.alerta {
    background: #fff;
    text-align: center;
    padding: 10px;
    font-weight: bold;
    border-bottom: 1px solid #ddd;
}

/* GRID */
.grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    padding: 20px;
}

/* RESPONSIVO */
@media (max-width: 900px) {
    .grid {
        grid-template-columns: 1fr;
    }
}

/* COLUNAS */
.coluna h2 {
    text-align: center;
}

/* CARD */
.pizza {
    background: #fff;
    border-radius: 12px;
    margin-bottom: 15px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

.pizza img {
    width: 100%;
    height: 140px;
    object-fit: cover;
}

.pizza-info {
    padding: 10px;
}

button {
    background: #f7931e;
    color: #fff;
    border: none;
    padding: 10px;
    width: 100%;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
}

/* CARRINHO DESKTOP */
.carrinho {
    background: #fff;
    padding: 15px;
    position: fixed;
    right: 0;
    top: 0;
    width: 280px;
    height: 100%;
    border-left: 1px solid #ddd;
}

/* CARRINHO MOBILE */
@media (max-width: 900px) {
    .carrinho {
        position: fixed;
        bottom: 0;
        top: auto;
        width: 100%;
        height: auto;
        border-top: 1px solid #ddd;
    }
}

.finalizar {
    background: #f7931e;
    color: #fff;
    width: 100%;
    margin-top: 10px;
}

select {
    width: 100%;
    padding: 8px;
    margin-top: 10px;
}

</style>
</head>

<body>

<!-- TOPO -->
<div class="hero">
    <div class="overlay">
        <div class="logo">
            <img src="logo.png" alt="Today Pizza">
        </div>
        <div class="hero-text">
            <h1>Today Pizza</h1>
            <p>Delivery em Marechal Cândido Rondon - PR 🍕</p>
        </div>
    </div>
</div>

<div class="alerta">
🚚 Apenas entregas • Marechal Cândido Rondon - PR
</div>

<!-- CARDÁPIO -->
<div class="grid">

<!-- SALGADAS -->
<div class="coluna">
<h2>🍕 Salgadas</h2>

<div class="pizza">
<img src="https://images.unsplash.com/photo-1604382355076-af4b0eb60143">
<div class="pizza-info">
<h3>Calabresa</h3>
<strong>R$ 35</strong>
<button onclick="addCarrinho('Calabresa',35)">Adicionar</button>
</div>
</div>

<div class="pizza">
<img src="https://images.unsplash.com/photo-1593560708920-61dd98c46a4e">
<div class="pizza-info">
<h3>Frango com Catupiry</h3>
<strong>R$ 38</strong>
<button onclick="addCarrinho('Frango com Catupiry',38)">Adicionar</button>
</div>
</div>

</div>

<!-- DOCES -->
<div class="coluna">
<h2>🍫 Doces</h2>

<div class="pizza">
<img src="https://images.unsplash.com/photo-1601924582975-7e6c94b2a8f8">
<div class="pizza-info">
<h3>Chocolate</h3>
<strong>R$ 30</strong>
<button onclick="addCarrinho('Chocolate',30)">Adicionar</button>
</div>
</div>

<div class="pizza">
<img src="https://images.unsplash.com/photo-1594007654729-407eedc4fe24">
<div class="pizza-info">
<h3>Morango com Chocolate</h3>
<strong>R$ 35</strong>
<button onclick="addCarrinho('Morango com Chocolate',35)">Adicionar</button>
</div>
</div>

</div>

<!-- BEBIDAS -->
<div class="coluna">
<h2>🥤 Bebidas</h2>

<div class="pizza">
<img src="https://images.unsplash.com/photo-1581006852262-e4307cf6283a">
<div class="pizza-info">
<h3>Coca-Cola 2L</h3>
<strong>R$ 12</strong>
<button onclick="addCarrinho('Coca-Cola 2L',12)">Adicionar</button>
</div>
</div>

<div class="pizza">
<img src="https://images.unsplash.com/photo-1577801598627-ff2a44d88b41">
<div class="pizza-info">
<h3>Guaraná 2L</h3>
<strong>R$ 10</strong>
<button onclick="addCarrinho('Guaraná 2L',10)">Adicionar</button>
</div>
</div>

</div>

</div>

<!-- CARRINHO -->
<div class="carrinho">
<h3>Carrinho</h3>
<ul id="lista"></ul>
<strong>Total: R$ <span id="total">0</span></strong>

<select id="pagamento">
<option value="pix">PIX</option>
<option value="cartao">Cartão na entrega</option>
</select>

<button class="finalizar" onclick="finalizarPedido()">Finalizar Pedido</button>
</div>

<script>
let total = 0;

function addCarrinho(nome, preco){
    let lista = document.getElementById("lista");

    let item = document.createElement("li");
    item.innerText = nome + " - R$ " + preco.toFixed(2);

    lista.appendChild(item);

    total += preco;
    document.getElementById("total").innerText = total.toFixed(2);
}

function finalizarPedido(){
    if(total === 0){
        alert("Carrinho vazio!");
        return;
    }

    let pagamento = document.getElementById("pagamento").value;

    if(pagamento === "pix"){
        alert("Pedido realizado! Enviaremos o PIX.");
    } else {
        alert("Pedido realizado! Pague na entrega.");
    }
}

function finalizarPedido(){
    let endereco = document.getElementById("endereco").value;

    if(carrinho.length === 0 || endereco === ""){
        alert("Preencha o carrinho e o endereço!");
        return;
    }

    let pagamento = document.getElementById("pagamento").value;

    let msg = "🍕 *TODAY PIZZA* 🍕\n\n";

    carrinho.forEach(i=>{
        msg += "• " + i.nome + " - R$ " + i.preco.toFixed(2) + "\n";
    });

    msg += "\n💰 Total: R$ " + total.toFixed(2);
    msg += "\n📍 Endereço: " + endereco;
    msg += "\n💳 Pagamento: " + pagamento;
    msg += "\n🚚 Marechal Cândido Rondon - PR";

    let numero = "5544998905286"; // SEU NÚMERO

    let url = "https://wa.me/" + numero + "?text=" + encodeURIComponent(msg);

    window.open(url, "_blank");
}

trocar('salgada');
</script>

</body>
</html>
