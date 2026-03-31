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

/* HERO CLARO */
.hero {
    background: url("https://images.unsplash.com/photo-1593560708920-61dd98c46a4e") center/cover no-repeat;
    height: 260px;
    position: relative;
}

.overlay {
    background: rgba(255,255,255,0.75);
    height: 100%;
    display: flex;
    align-items: center;
    padding: 20px;
}

/* LOGO */
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

/* TEXTO */
.hero-text {
    margin-left: 15px;
}

.hero-text h1 {
    margin: 0;
    color: #000;
}

.hero-text p {
    margin-top: 5px;
    color: #555;
}

/* ALERTA */
.alerta {
    background: #fff;
    text-align: center;
    padding: 12px;
    font-weight: bold;
    border-bottom: 1px solid #ddd;
}

/* CARDÁPIO */
.container {
    padding: 20px;
}

.pizza {
    background: #fff;
    border-radius: 12px;
    margin-bottom: 15px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

.pizza img {
    width: 100%;
    height: 170px;
    object-fit: cover;
}

.pizza-info {
    padding: 15px;
}

.pizza-info h3 {
    margin: 0;
}

.pizza-info p {
    color: #666;
    font-size: 14px;
}

/* BOTÃO */
button {
    background: #f7931e;
    color: #fff;
    border: none;
    padding: 10px;
    width: 100%;
    margin-top: 10px;
    border-radius: 8px;
    cursor: pointer;
}

/* CARRINHO */
.carrinho {
    background: #fff;
    color: #333;
    padding: 15px;
    position: fixed;
    right: 0;
    top: 0;
    width: 280px;
    height: 100%;
    overflow-y: auto;
    border-left: 1px solid #ddd;
}

.finalizar {
    background: #f7931e;
    color: #fff;
    width: 100%;
    margin-top: 10px;
    font-weight: bold;
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

<!-- CARDÁPIO -->
<div class="container">

<div class="pizza">
    <img src="https://images.unsplash.com/photo-1604382355076-af4b0eb60143">
    <div class="pizza-info">
        <h3>Calabresa</h3>
        <p>Molho, muçarela, calabresa e cebola</p>
        <strong>R$ 35,00</strong>
        <button onclick="addCarrinho('Calabresa',35)">Adicionar</button>
    </div>
</div>

<div class="pizza">
    <img src="https://images.unsplash.com/photo-1593560708920-61dd98c46a4e">
    <div class="pizza-info">
        <h3>Frango com Catupiry</h3>
        <p>Molho, muçarela, frango e catupiry</p>
        <strong>R$ 38,00</strong>
        <button onclick="addCarrinho('Frango',38)">Adicionar</button>
    </div>
</div>

<div class="pizza">
    <img src="https://images.unsplash.com/photo-1594007654729-407eedc4fe24">
    <div class="pizza-info">
        <h3>Moda da Casa</h3>
        <p>Frango, milho, bacon e catupiry</p>
        <strong>R$ 45,00</strong>
        <button onclick="addCarrinho('Moda',45)">Adicionar</button>
    </div>
</div>

</div>

<!-- CARRINHO -->
<div class="carrinho">
    <h2>Carrinho</h2>
    <ul id="lista"></ul>
    <h3>Total: R$ <span id="total">0</span></h3>

    <h3>Pagamento</h3>
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
    let pagamento = document.getElementById("pagamento").value;

    if(total === 0){
        alert("Carrinho vazio!");
        return;
    }

    if(pagamento === "pix"){
        alert("Pedido feito! Enviaremos o PIX.");
    } else {
        alert("Pedido feito! Pague na entrega.");
    }
}
</script>

</body>
</html>
