<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Today Pizza</title>

<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        background: #f7931e;
        color: #000;
    }

    header {
        text-align: center;
        padding: 20px;
        background: #000;
    }

    header img {
        width: 180px;
    }

    .alerta {
        background: #ffcc00;
        text-align: center;
        padding: 10px;
        font-weight: bold;
    }

    .container {
        padding: 20px;
    }

    .pizza {
        background: #fff;
        margin-bottom: 15px;
        padding: 15px;
        border-radius: 10px;
    }

    button {
        background: #000;
        color: #f7931e;
        border: none;
        padding: 10px;
        cursor: pointer;
        margin-top: 10px;
        border-radius: 5px;
    }

    .carrinho {
        background: #000;
        color: #fff;
        padding: 15px;
        position: fixed;
        right: 0;
        top: 0;
        width: 300px;
        height: 100%;
        overflow-y: auto;
    }

    .finalizar {
        background: #f7931e;
        color: #000;
        width: 100%;
        margin-top: 10px;
        font-weight: bold;
    }

</style>
</head>

<body>

<header>
    <img src="logo.png" alt="Today Pizza">
</header>

<div class="alerta">
    🚚 SOMENTE ENTREGAS em Marechal Cândido Rondon - PR
</div>

<div class="container">

    <div class="pizza">
        <h3>Calabresa</h3>
        <p>Molho, muçarela, calabresa e cebola</p>
        <strong>R$ 35,00</strong><br>
        <button onclick="addCarrinho('Calabresa', 35)">Adicionar</button>
    </div>

    <div class="pizza">
        <h3>Frango com Catupiry</h3>
        <p>Molho, muçarela, frango e catupiry</p>
        <strong>R$ 38,00</strong><br>
        <button onclick="addCarrinho('Frango com Catupiry', 38)">Adicionar</button>
    </div>

    <div class="pizza">
        <h3>Moda da Casa</h3>
        <p>Frango, milho, bacon, catupiry e azeitona</p>
        <strong>R$ 45,00</strong><br>
        <button onclick="addCarrinho('Moda da Casa', 45)">Adicionar</button>
    </div>

</div>

<div class="carrinho">
    <h2>Carrinho</h2>
    <ul id="lista"></ul>
    <h3>Total: R$ <span id="total">0</span></h3>

    <h3>Pagamento:</h3>
    <select id="pagamento">
        <option value="pix">PIX</option>
        <option value="cartao">Cartão na entrega</option>
    </select>

    <button class="finalizar" onclick="finalizarPedido()">Finalizar Pedido</button>
</div>

<script>
    let total = 0;

    function addCarrinho(nome, preco) {
        let lista = document.getElementById("lista");

        let item = document.createElement("li");
        item.innerText = nome + " - R$ " + preco.toFixed(2);
        lista.appendChild(item);

        total += preco;
        document.getElementById("total").innerText = total.toFixed(2);
    }

    function finalizarPedido() {
        let pagamento = document.getElementById("pagamento").value;

        if (total === 0) {
            alert("Carrinho vazio!");
            return;
        }

        if (pagamento === "pix") {
            alert("Pedido feito! Enviaremos o PIX para pagamento.");
        } else {
            alert("Pedido feito! Pague no cartão na entrega.");
        }
    }
</script>

</body>
</html>
