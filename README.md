<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
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
    height: 260px;
}

.overlay {
    background: rgba(255,255,255,0.75);
    height: 100%;
    display: flex;
    align-items: center;
    padding: 20px;
}

.logo {
    width: 80px;
    height: 80px;
    background: #f7931e;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.logo img {
    width: 60px;
}

.hero-text {
    margin-left: 15px;
}

.alerta {
    background: #fff;
    text-align: center;
    padding: 12px;
    font-weight: bold;
    border-bottom: 1px solid #ddd;
}

/* GRID 3 COLUNAS */
.grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    padding: 20px;
}

/* COLUNAS */
.coluna h2 {
    text-align: center;
    margin-bottom: 10px;
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
    padding: 8px;
    width: 100%;
    margin-top: 8px;
    border-radius: 8px;
    cursor: pointer;
}

/* CARRINHO */
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

.finalizar {
    background: #f7931e;
    color: #fff;
    width: 100%;
    margin-top: 10px;
}

</style>
</head>

<body>

<div class="hero">
    <div class="overlay">
        <div class="logo">
            <img src="logo.png">
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

<!-- GRID -->
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
<h3>Frango c/ Catupiry</h3>
<strong>R$ 38</strong>
<button onclick="addCarrinho('Frango',38)">Adicionar</button>
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
<button onclick="addCarrinho('Morango',35)">Adicionar</button>
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
<button onclick="addCarrinho('Coca 2L',12)">Adicionar</button>
</div>
</div>

<div class="pizza">
<img src="https://images.unsplash.com/photo-1577801598627-ff2a44d88b41">
<div class="pizza-info">
<h3>Guaraná 2L</h3>
<strong>R$ 10</strong>
<button onclick="addCarrinho('Guaraná',10)">Adicionar</button>
</div>
</div>

</div>

</div>

<!-- CARRINHO -->
<div class="carrinho">
<h2>Carrinho</h2>
<ul id="lista"></ul>
<h3>Total: R$ <span id="total">0</span></h3>

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
    item.innerText = nome + " - R$ " + preco;

    lista.appendChild(item);

    total += preco;
    document.getElementById("total").innerText = total;
}

function finalizarPedido(){
    if(total === 0){
        alert("Carrinho vazio!");
        return;
    }

    alert("Pedido realizado!");
}
</script>

</body>
</html>
