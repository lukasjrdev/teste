<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lista de Compras</title>
<style>
    
    body {
        font-family: Arial, sans-serif;
        background-color: aqua;
    }
    .container {
        max-width: 200px;
        margin: 20px;
        padding: 50px;
        border: 3px solid #2b0666;
        border-radius: 15px;
    }
    .item {
        margin-bottom: 30px;


    }
    button {
        background-color: #0f0e0f;
        color: rgb(239, 237, 243);
        border: none;
        padding: 5px 10px;
        border-radius: 5px;
        cursor: pointer;
        margin-bottom: 10px;
        border-radius: 15px;

    }
    button.calculate {
        
        background-color: #113d1c;
        
    }
</style>
</head>
<body>

<div class="container">
    <h2>Lista de Compras</h2>
    <div id="items">
        <!-- Itens adicionados serão exibidos aqui -->
    </div>
    <hr>


    <div>
        <label for="itemName"> Item:</label>
        <input type="text" id="itemName">
        <label for="itemPrice"> Preço:</label>
        <input type="number" id="itemPrice">
        <label for="itemQuantity"> Quantidade:</label>
        <input type="number" id="itemQuantity">
        <hr>
        <button onclick="addItem()"> Adicionar Item </button>
    </div>
    <div>
        <button onclick="calculateTotal()">Calcular Total</button>

        <p id="totalPrice"></p>
        
    </div>
</div>

<script>
    let items = [];

    function addItem() {
        const itemName = document.getElementById("itemName").value;
        const itemPrice = parseFloat(document.getElementById("itemPrice").value);
        const itemQuantity = parseInt(document.getElementById("itemQuantity").value);

        if (itemName && itemPrice && itemQuantity) {
            const newItem = {
                name: itemName,
                price: itemPrice,
                quantity: itemQuantity
            };
            items.push(newItem);
            renderItems();
        } else {
            alert("Adicione 1 item.");
        }
    }

    function removeItem(index) {
        items.splice(index, 1);
        renderItems();
    }

    function renderItems() {
        const itemsContainer = document.getElementById("items");
        itemsContainer.innerHTML = "";
        items.forEach((item, index) => {
            const itemDiv = document.createElement("div");
            itemDiv.classList.add("item");
            itemDiv.innerHTML = `
                <span>${item.name} - R$${item.price.toFixed(2)} - Quantidade: ${item.quantity}</span>
                <button onclick="removeItem(${index})">Remover</button>
            `;
            itemsContainer.appendChild(itemDiv);
        });
    }

    function calculateTotal() {
        let total = 0;
        items.forEach(item => {
            total += item.price * item.quantity;
        });
        document.getElementById("totalPrice").innerText = `Preço Total: R$${total.toFixed(2)}`;
    }
</script>

</body>
</html>
