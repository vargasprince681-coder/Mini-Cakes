# Mini Cakes
# This is my first project on github
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sweet Delights Cake Shop</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

<header>
  <h1>Sweet Delights Cake Shop</h1>
  <p>Order your favorite cakes online!</p>
</header>

<nav>
  <a href="#">Home</a>
  <a href="#products">Products</a>
  <a href="#contact">Contact</a>
</nav>

<div class="container" id="products">
  <h2>Available Cakes</h2>
  <div class="products" id="product-list"></div>
</div>

<div class="cart">
  <h3>Your Cart</h3>
  <ul id="cart-items"></ul>
  <p><strong>Total: $<span id="total">0</span></strong></p>
  <button onclick="checkout()">Checkout</button>
</div>

<footer>
  <p>© 2026 Sweet Delights</p>
</footer>

<script src="script.js"></script>
</body>
</html>


/* styles.css */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  background: #fff5f7;
}
header {
  background: #ff6f91;
  color: white;
  padding: 15px;
  text-align: center;
}
nav {
  display: flex;
  justify-content: center;
  gap: 20px;
  background: #ff8fab;
  padding: 10px;
}
nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}
.container {
  padding: 20px;
}
.products {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}
.card {
  background: white;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  text-align: center;
}
.card img {
  width: 100%;
  border-radius: 10px;
}
button {
  margin-top: 10px;
  padding: 10px;
  border: none;
  background: #ff6f91;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}
.cart {
  position: fixed;
  right: 0;
  top: 0;
  width: 300px;
  height: 100%;
  background: #fff;
  border-left: 2px solid #ff6f91;
  padding: 15px;
  overflow-y: auto;
}
footer {
  text-align: center;
  padding: 15px;
  background: #ff6f91;
  color: white;
}


// script.js
const products = [
  {name: "Chocolate Cake", price: 20, img: "https://via.placeholder.com/200"},
  {name: "Strawberry Cake", price: 18, img: "https://via.placeholder.com/200"},
  {name: "Vanilla Cake", price: 15, img: "https://via.placeholder.com/200"},
  {name: "Red Velvet Cake", price: 22, img: "https://via.placeholder.com/200"}
];

let cart = [];

function displayProducts() {
  const list = document.getElementById("product-list");
  list.innerHTML = "";
  products.forEach((p, index) => {
    list.innerHTML += `
      <div class="card">
        <img src="${p.img}" alt="${p.name}">
        <h3>${p.name}</h3>
        <p>$${p.price}</p>
        <button onclick="addToCart(${index})">Add to Cart</button>
      </div>
    `;
  });
}

function addToCart(index) {
  cart.push(products[index]);
  updateCart();
}

function updateCart() {
  const cartList = document.getElementById("cart-items");
  const total = document.getElementById("total");
  cartList.innerHTML = "";
  let sum = 0;

  cart.forEach(item => {
    cartList.innerHTML += `<li>${item.name} - $${item.price}</li>`;
    sum += item.price;
  });

  total.innerText = sum;
}

function checkout() {
  if(cart.length === 0) {
    alert("Your cart is empty!");
  } else {
    alert("Order placed successfully!");
    cart = [];
    updateCart();
  }
}

window.onload = displayProducts;
