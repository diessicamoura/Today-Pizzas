<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Today Pizza - Cardápio</title>
    <style>
        :root {
            --primary: #f7931e;
            --dark: #1a1a1a;
            --light: #f9f9f9;
        }

        body {
            margin: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--light);
            color: var(--dark);
            padding-bottom: 100px;
        }

        /* HEADER */
        header {
            background: var(--primary);
            text-align: center;
            padding: 20px;
            color: white;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        .logo-header {
            width: 120px;
            border-radius: 50%;
            border: 4px solid white;
        }

        /* GRID DO CARDÁPIO */
        .container {
            max-width: 1200px;
            margin: 20px auto;
            padding: 0 20px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 25px;
        }

        @media (max-width: 900px) {
            .container { grid-template-columns: 1fr; }
        }

        .coluna h2 {
            background: var(--dark);
            color: white;
            padding: 10px;
            border-radius: 8px;
            text-align: center;
            font-size: 1.2rem;
        }

        /* ITENS */
        .item {
            background: white;
            padding: 15px;
            margin-bottom: 15px;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        .item-info h4 { margin: 0; }
        .item-info p { margin: 5px 0; color: #666; font-size: 0.9rem; }

        .btn-add {
            background: var(--primary);
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }

        /* CARRINHO E DADOS */
        .checkout-section {
            background: white;
            max-width: 1200px;
            margin: 20px auto;
            padding: 20px;
            border-radius: 15px;
            border: 2px solid var(--primary);
        }

        .form-group {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr;
            gap: 10px;
            margin-top: 15px;
        }

        @media (max-width: 600px) {
            .form-group { grid-template-columns: 1fr; }
        }

        input, select {
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 8px;
            outline: none;
        }

        .btn-finalizar {
            background: #27ae60;
            color: white;
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            margin-top: 20px;
        }

        #resumo-carrinho {
            list-style: none;
            padding: 0;
            border-bottom: 1px solid #eee;
        }
    </style>
</head>
<body>

<header>
    <img src="TODAY-PNG.jpg" alt="Today Pizza Logo" class="logo-header">
    <h1>Today Pizza</h1>
    <p>O melhor delivery de Marechal Cândido Rondon 🍕</p>
</header>

<div class="container">
    <div class="coluna">
        <h2>🍕 Pizzas Salgadas</h2>
        <div id="pizzas-salgadas"></div>
    </div>

    <div class="coluna">
        <h2>🍫 Pizzas Doces</h2>
        <div id="pizzas-doces"></div>
    </div>

    <div class="coluna">
        <h2>🥤 Bebidas</h2>
        <div id="bebidas"></div>
    </div>
</div>

<div class="checkout-section">
    <h3>🛒 Seu Pedido</h3>
    <ul id="resumo-carrinho">
        <p style="color: #999;">Carrinho vazio...</p>
    </ul>
    <h3>Total: R$ <span id="valor-total">0.00</span></h3>

    <hr>
    <h3>📍 Dados para Entrega</h3>
    <div class="form-group">
        <input type="text" id="rua" placeholder="Rua (Obrigatório)" required>
        <input type="text" id="numero" placeholder="Nº" required>
        <input type="text" id="bairro" placeholder="Bairro" required>
    </div>
    
    <h3 style="margin-top: 20px;">💳 Pagamento</h3>
    <select id="metodo-pagamento" style="width: 100%;">
        <option value="Pix">Pix</option>
        <option value="Cartão de Crédito">Cartão de Crédito</option>
        <option value="Cartão de Débito">Cartão de Débito</option>
        <option value="Dinheiro">Dinheiro</option>
    </select>

    <button class="btn-finalizar" onclick="enviarPedido()">Finalizar Pedido pelo WhatsApp</button>
</div>

<script>
    const salgadas = [
        "Calabresa", "Frango com Catupiry", "Portuguesa", "Marguerita", "Quatro Queijos", 
        "Moda da Casa", "Bacon", "Milho", "Palmito", "Lombo"
    ];
    const doces = [
        "Chocolate Preto", "Chocolate Branco", "Prestígio", "Romeu e Julieta", "Confete",
        "Banana com Canela", "Morango com Chocolate", "Ouro Branco", "Paçoquita", "Sensação"
    ];
    const itensBebidas = [
        {nome: "Coca-Cola 2L", preco: 14},
        {nome: "Guaraná Antártica 2L", preco: 12},
        {nome: "Fanta Laranja 2L", preco: 12}
    ];

    let carrinho = [];

    // Gerar Cardápio Automaticamente
    function carregarCardapio() {
        const gridSalgada = document.getElementById('pizzas-salgadas');
        salgadas.forEach(nome => {
            gridSalgada.innerHTML += criarTemplateItem(nome, 35.00);
        });

        const gridDoce = document.getElementById('pizzas-doces');
        doces.forEach(nome => {
            gridDoce.innerHTML += criarTemplateItem(nome, 32.00);
        });

        const gridBebida = document.getElementById('bebidas');
        itensBebidas.forEach(item => {
            gridBebida.innerHTML += criarTemplateItem(item.nome, item.preco);
        });
    }

    function criarTemplateItem(nome, preco) {
        return `
            <div class="item">
                <div class="item-info">
                    <h4>${nome}</h4>
                    <p>R$ ${preco.toFixed(2)}</p>
                </div>
                <button class="btn-add" onclick="addAoCarrinho('${nome}', ${preco})">+</button>
            </div>
        `;
    }

    function addAoCarrinho(nome, preco) {
        carrinho.push({nome, preco});
        atualizarVisualCarrinho();
    }

    function atualizarVisualCarrinho() {
        const lista = document.getElementById('resumo-carrinho');
        const totalTxt = document.getElementById('valor-total');
        lista.innerHTML = "";
        let total = 0;

        carrinho.forEach((item, index) => {
            lista.innerHTML += `<li>${item.nome} - R$ ${item.preco.toFixed(2)}</li>`;
            total += item.preco;
        });

        totalTxt.innerText = total.toFixed(2);
    }

    function enviarPedido() {
        const rua = document.getElementById('rua').value;
        const num = document.getElementById('numero').value;
        const bairro = document.getElementById('bairro').value;
        const pgto = document.getElementById('metodo-pagamento').value;

        if (carrinho.length === 0) return alert("Adicione itens ao carrinho!");
        if (!rua || !num || !bairro) return alert("Preencha todos os campos de endereço!");

        let msg = `🍕 *PEDIDO TODAY PIZZA*\n\n`;
        carrinho.forEach(i => msg += `• ${i.nome}\n`);
        msg += `\n💰 *Total:* R$ ${document.getElementById('valor-total').innerText}`;
        msg += `\n💳 *Pagamento:* ${pgto}`;
        msg += `\n📍 *Entrega:* ${rua}, nº ${num} - ${bairro}`;

        const fone = "5544998905286";
        const url = `https://wa.me/${fone}?text=${encodeURIComponent(msg)}`;
        
        window.open(url, '_blank');
        alert("✅ PEDIDO CONCLUÍDO COM SUCESSO!");
    }

    carregarCardapio();
</script>

</body>
</html>
