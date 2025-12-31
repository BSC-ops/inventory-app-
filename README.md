# inventory-app-
<!DOCTYPE html>
<html>
<head>
  <title>Inventory App</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body { font-family: Arial; padding: 15px; }
    input, button { padding: 8px; margin: 4px; width: 100%; }
    table { width: 100%; border-collapse: collapse; margin-top: 15px; }
    th, td { border: 1px solid #ccc; padding: 6px; text-align: center; }
    th { background: #eee; }
  </style>
</head>
<body>

<h2>Inventory Manager</h2>

<input id="name" placeholder="Item Name">
<input id="qty" type="number" placeholder="Starting Quantity">
<button onclick="addItem()">Add Item</button>

<table>
  <thead>
    <tr>
      <th>Item</th>
      <th>Qty</th>
      <th>+</th>
      <th>-</th>
    </tr>
  </thead>
  <tbody id="table"></tbody>
</table>

<script>
let inventory = JSON.parse(localStorage.getItem("inventory")) || [];

function save() {
  localStorage.setItem("inventory", JSON.stringify(inventory));
}

function render() {
  let t = document.getElementById("table");
  t.innerHTML = "";
  inventory.forEach((item, i) => {
    t.innerHTML += `
      <tr>
        <td>${item.name}</td>
        <td>${item.qty}</td>
        <td><button onclick="change(${i},1)">+</button></td>
        <td><button onclick="change(${i},-1)">-</button></td>
      </tr>`;
  });
}

function addItem() {
  let n = name.value.trim();
  let q = parseInt(qty.value);
  if (!n || isNaN(q)) return alert("Fill all fields");
  inventory.push({ name: n, qty: q });
  save();
  render();
}

function change(i, v) {
  inventory[i].qty += v;
  if (inventory[i].qty < 0) inventory[i].qty = 0;
  save();
  render();
}

render();
</script>

</body>
</html>

name,qty
Shampoo,120
Conditioner,85
Hair Gel,40

