<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Today Pizza</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #111;
    color: #fff;
}

/* TOPO COM IMAGEM */
.hero {
    background: url("https://images.unsplash.com/photo-1601924582975-7e6c94b2a8f8") center/cover no-repeat;
    height: 300px;
    position: relative;
}

.overlay {
    background: rgba(0,0,0,0.6);
    height: 100%;
    display: flex;
    align-items: center;
    padding: 20px;
}

/* LOGO */
.logo {
    width: 90px;
    height: 90px;
    background: #f7931e;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.logo img {
    width: 70px;
}

/* TEXTO AO LADO DA LOGO */
.hero-text {
    margin-left: 15px;
}

.hero-text h1 {
    margin: 0;
    color: #f7931e;
}

.hero-text p {
    margin: 5px 0 0;
}

/* ALERTA */
.alerta {
    background: #f7931e;
    color: #000;
    text-align: center;
    padding: 10px;
    font-weight: bold;
}

/* CARDÁPIO */
.container {
    padding: 20px;
}

.pizza {
    background: #1c1c1c;
    border-radius: 10px;
    margin-bottom: 15px;
    overflow: hidden;
}

.pizza img {
    width: 100%;
    height: 180px;
    object-fit: cover;
}

.pizza-info {
    padding: 15px;
}

button {
    background: #f7931e;
    color: #000;
    border: none;
    padding: 10px;
    width: 100%;
    margin-top: 10px;
    cursor: pointer;
    border-radius: 5px;
    font-weight: bold;
}

/* CARRINHO */
.carrinho {
    background: #000;
    color: #fff;
    padding: 15px;
    position: fixed;
    right: 0;
    top: 0;
    width: 280px;
    height: 100%;
    overflow-y: auto;
}

.finalizar {
    background: #f7931e;
    color: #000;
    width: 100%;
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
🚚 SOMENTE ENTREGA
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
        <p>Frango, milho, bacon, catupiry</p>
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

    <button class="finalizar" onclick="finalizarPedido()">Finalizar</button>
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
