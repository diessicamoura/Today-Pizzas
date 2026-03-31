<div class="carrinho">
    <h3>🛒 Teu Carrinho</h3>
    <ul id="lista" style="list-style: none; padding: 0; max-height: 200px; overflow-y: auto;">
        </ul>
    <hr>
    <strong>Total: R$ <span id="total">0.00</span></strong>

    <select id="pagamento">
        <option value="pix">PIX</option>
        <option value="cartao">Cartão na entrega</option>
    </select>

    <button class="finalizar" onclick="finalizarPedido()">Finalizar Pedido</button>
    <button onclick="limparCarrinho()" style="background: #ccc; color: #333; margin-top: 5px;">Esvaziar Carrinho</button>
</div>

<script>
    // Variáveis globais para armazenar os dados
    let carrinho = [];

    // FUNÇÃO 1: Adicionar item ao array do carrinho
    function addCarrinho(nome, preco) {
        carrinho.push({ nome, preco });
        renderizarCarrinho();
    }

    // FUNÇÃO 2: Remover um item específico pelo index
    function removerDoCarrinho(index) {
        carrinho.splice(index, 1); // Remove 1 item na posição do index
        renderizarCarrinho();
    }

    // FUNÇÃO 3: Limpar todo o carrinho
    function limparCarrinho() {
        if(confirm("Desejas mesmo esvaziar o carrinho?")) {
            carrinho = [];
            renderizarCarrinho();
        }
    }

    // FUNÇÃO 4: Atualizar a visualização do HTML (O "Coração" do sistema)
    function renderizarCarrinho() {
        const listaElemento = document.getElementById("lista");
        const totalElemento = document.getElementById("total");
        
        // Limpa a lista visual antes de reconstruir
        listaElemento.innerHTML = "";
        let somaTotal = 0;

        // Cria cada item da lista com um botão de remover
        carrinho.forEach((item, index) => {
            const li = document.createElement("li");
            li.style.marginBottom = "8px";
            li.style.display = "flex";
            li.style.justifyContent = "space-between";
            
            li.innerHTML = `
                <span>${item.nome} - R$ ${item.preco.toFixed(2)}</span>
                <button onclick="removerDoCarrinho(${index})" style="width: auto; padding: 2px 8px; background: #e74c3c;">X</button>
            `;
            
            listaElemento.appendChild(li);
            somaTotal += item.preco;
        });

        // Atualiza o valor total na tela
        totalElemento.innerText = somaTotal.toFixed(2);
    }

    // FUNÇÃO 5: Finalizar e enviar para o WhatsApp
    function finalizarPedido() {
        if (carrinho.length === 0) {
            alert("O teu carrinho está vazio!");
            return;
        }

        let pagamento = document.getElementById("pagamento").value;
        let totalFinal = document.getElementById("total").innerText;

        let mensagem = "🍕 *PEDIDO - TODAY PIZZA* 🍕\n\n";
        carrinho.forEach(item => {
            mensagem += `• ${item.nome} - R$ ${item.preco.toFixed(2)}\n`;
        });

        mensagem += `\n💰 *Total: R$ ${totalFinal}*`;
        mensagem += `\n📲 *Pagamento:* ${pagamento.toUpperCase()}`;
        mensagem += "\n📍 Entrega em Marechal Cândido Rondon - PR";

        let numero = "5544998905286"; // Altera para o teu número real
        let url = "https://wa.me/" + numero + "?text=" + encodeURIComponent(mensagem);

        window.open(url, "_blank");
    }
</script>
