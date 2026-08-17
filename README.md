<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>NovaStore | Quality Products</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial,sans-serif;
}

body{
    background:#f5f6f8;
    color:#222;
}

header{
    background:#111827;
    color:white;
    padding:15px 5%;
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:15px;
    position:sticky;
    top:0;
    z-index:100;
}

.logo{
    font-size:24px;
    font-weight:bold;
}

.logo span{
    color:#22c55e;
}

.search{
    flex:1;
    max-width:500px;
}

.search input{
    width:100%;
    padding:12px 15px;
    border:none;
    border-radius:8px;
    outline:none;
}

.header-buttons{
    display:flex;
    gap:8px;
}

button{
    cursor:pointer;
    border:none;
}

.header-buttons button{
    padding:10px 13px;
    border-radius:7px;
    background:#22c55e;
    color:white;
}

.hero{
    padding:60px 5%;
    background:linear-gradient(135deg,#111827,#1f2937);
    color:white;
    text-align:center;
}

.hero h1{
    font-size:42px;
    margin-bottom:15px;
}

.hero p{
    font-size:18px;
    margin-bottom:25px;
}

.hero button{
    background:#22c55e;
    color:white;
    padding:14px 25px;
    border-radius:8px;
    font-size:16px;
}

.categories{
    padding:30px 5%;
    text-align:center;
}

.categories h2{
    margin-bottom:20px;
}

.category-buttons{
    display:flex;
    justify-content:center;
    flex-wrap:wrap;
    gap:10px;
}

.category-buttons button{
    padding:10px 18px;
    background:white;
    border:1px solid #ddd;
    border-radius:20px;
}

.category-buttons button:hover{
    background:#22c55e;
    color:white;
}

.products{
    padding:20px 5% 50px;
}

.products h2{
    margin-bottom:25px;
    text-align:center;
}

.product-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(210px,1fr));
    gap:20px;
}

.product{
    background:white;
    border-radius:12px;
    overflow:hidden;
    box-shadow:0 3px 12px rgba(0,0,0,.08);
    transition:.2s;
}

.product:hover{
    transform:translateY(-5px);
}

.product-image{
    height:190px;
    background:#e5e7eb;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:70px;
}

.product-info{
    padding:15px;
}

.product-info h3{
    margin-bottom:8px;
}

.price{
    color:#16a34a;
    font-size:20px;
    font-weight:bold;
    margin:10px 0;
}

.product-info button{
    width:100%;
    padding:11px;
    background:#111827;
    color:white;
    border-radius:7px;
}

.product-info button:hover{
    background:#22c55e;
}

footer{
    background:#111827;
    color:white;
    padding:40px 5%;
    text-align:center;
}

footer p{
    margin:8px;
    color:#bbb;
}

/* MODALS */

.modal{
    display:none;
    position:fixed;
    inset:0;
    background:rgba(0,0,0,.65);
    z-index:200;
    align-items:center;
    justify-content:center;
    padding:20px;
}

.modal-box{
    background:white;
    width:100%;
    max-width:420px;
    border-radius:12px;
    padding:25px;
    position:relative;
}

.close{
    position:absolute;
    right:18px;
    top:15px;
    font-size:24px;
    cursor:pointer;
}

.modal-box h2{
    margin-bottom:20px;
}

.modal-box input{
    width:100%;
    padding:12px;
    margin:8px 0;
    border:1px solid #ddd;
    border-radius:7px;
}

.modal-box .submit{
    width:100%;
    padding:12px;
    margin-top:10px;
    background:#22c55e;
    color:white;
    border-radius:7px;
}

.switch{
    text-align:center;
    margin-top:15px;
    color:#555;
}

.switch span{
    color:#16a34a;
    cursor:pointer;
    font-weight:bold;
}

/* CART */

.cart-items{
    max-height:300px;
    overflow:auto;
}

.cart-item{
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding:12px 0;
    border-bottom:1px solid #ddd;
}

.cart-item button{
    background:#ef4444;
    color:white;
    padding:5px 8px;
    border-radius:5px;
}

.cart-total{
    font-size:20px;
    font-weight:bold;
    margin-top:20px;
}

.checkout{
    width:100%;
    padding:13px;
    background:#22c55e;
    color:white;
    margin-top:15px;
    border-radius:7px;
}

/* MOBILE */

@media(max-width:700px){

    header{
        flex-wrap:wrap;
    }

    .logo{
        width:100%;
        text-align:center;
    }

    .search{
        order:3;
        max-width:none;
        width:100%;
    }

    .header-buttons{
        margin:auto;
    }

    .hero h1{
        font-size:32px;
    }

    .hero{
        padding:45px 20px;
    }
}
</style>
</head>

<body>

<header>

    <div class="logo">
        Nova<span>Store</span>
    </div>

    <div class="search">
        <input
            type="text"
            id="searchInput"
            placeholder="Search products..."
            onkeyup="searchProducts()"
        >
    </div>

    <div class="header-buttons">
        <button onclick="openLogin()">Login</button>
        <button onclick="openCart()">🛒 Cart (<span id="cartCount">0</span>)</button>
    </div>

</header>


<section class="hero">

    <h1>Welcome to NovaStore</h1>

    <p>
        Quality products at affordable prices.
    </p>

    <button onclick="document.getElementById('products').scrollIntoView()">
        Shop Now
    </button>

</section>


<section class="categories">

    <h2>Shop By Category</h2>

    <div class="category-buttons">

        <button onclick="filterProducts('all')">
            All
        </button>

        <button onclick="filterProducts('electronics')">
            Electronics
        </button>

        <button onclick="filterProducts('fashion')">
            Fashion
        </button>

        <button onclick="filterProducts('home')">
            Home
        </button>

        <button onclick="filterProducts('beauty')">
            Beauty
        </button>

        <button onclick="filterProducts('accessories')">
            Accessories
        </button>

    </div>

</section>


<section class="products" id="products">

    <h2>Featured Products</h2>

    <div class="product-grid" id="productGrid">


        <div class="product" data-category="electronics">

            <div class="product-image">
                📱
            </div>

            <div class="product-info">

                <h3>Smartphone</h3>

                <p>Modern smartphone with powerful features.</p>

                <div class="price">
                    ₦150,000
                </div>

                <button onclick="addToCart('Smartphone',150000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="electronics">

            <div class="product-image">
                🎧
            </div>

            <div class="product-info">

                <h3>Wireless Headphones</h3>

                <p>Clear sound and comfortable design.</p>

                <div class="price">
                    ₦35,000
                </div>

                <button onclick="addToCart('Wireless Headphones',35000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="electronics">

            <div class="product-image">
                ⌚
            </div>

            <div class="product-info">

                <h3>Smart Watch</h3>

                <p>Track your activities and notifications.</p>

                <div class="price">
                    ₦45,000
                </div>

                <button onclick="addToCart('Smart Watch',45000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="fashion">

            <div class="product-image">
                👟
            </div>

            <div class="product-info">

                <h3>Running Sneakers</h3>

                <p>Comfortable shoes for everyday activities.</p>

                <div class="price">
                    ₦28,000
                </div>

                <button onclick="addToCart('Running Sneakers',28000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="fashion">

            <div class="product-image">
                👕
            </div>

            <div class="product-info">

                <h3>Premium T-Shirt</h3>

                <p>Simple and comfortable everyday wear.</p>

                <div class="price">
                    ₦15,000
                </div>

                <button onclick="addToCart('Premium T-Shirt',15000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="fashion">

            <div class="product-image">
                🧢
            </div>

            <div class="product-info">

                <h3>Classic Cap</h3>

                <p>Stylish cap for casual outfits.</p>

                <div class="price">
                    ₦8,000
                </div>

                <button onclick="addToCart('Classic Cap',8000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="home">

            <div class="product-image">
                🛋️
            </div>

            <div class="product-info">

                <h3>Modern Sofa</h3>

                <p>Comfortable furniture for your home.</p>

                <div class="price">
                    ₦250,000
                </div>

                <button onclick="addToCart('Modern Sofa',250000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="home">

            <div class="product-image">
                💡
            </div>

            <div class="product-info">

                <h3>LED Lamp</h3>

                <p>Bright and energy-efficient lighting.</p>

                <div class="price">
                    ₦12,000
                </div>

                <button onclick="addToCart('LED Lamp',12000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="beauty">

            <div class="product-image">
                🧴
            </div>

            <div class="product-info">

                <h3>Body Care Set</h3>

                <p>Daily care products for your routine.</p>

                <div class="price">
                    ₦18,000
                </div>

                <button onclick="addToCart('Body Care Set',18000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="accessories">

            <div class="product-image">
                🎒
            </div>

            <div class="product-info">

                <h3>Travel Backpack</h3>

                <p>Durable backpack for school and travel.</p>

                <div class="price">
                    ₦22,000
                </div>

                <button onclick="addToCart('Travel Backpack',22000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="accessories">

            <div class="product-image">
                🕶️
            </div>

            <div class="product-info">

                <h3>Fashion Sunglasses</h3>

                <p>Stylish sunglasses for everyday use.</p>

                <div class="price">
                    ₦10,000
                </div>

                <button onclick="addToCart('Fashion Sunglasses',10000)">
                    Add to Cart
                </button>

            </div>

        </div>


        <div class="product" data-category="electronics">

            <div class="product-image">
                💻
            </div>

            <div class="product-info">

                <h3>Laptop</h3>

                <p>Fast laptop for work, study and entertainment.</p>

                <div class="price">
                    ₦450,000
                </div>

                <button onclick="addToCart('Laptop',450000)">
                    Add to Cart
                </button>

            </div>

        </div>


    </div>

</section>


<footer>

    <h2>NovaStore</h2>

    <p>Your trusted online shopping store.</p>

    <p>© 2026 NovaStore. All rights reserved.</p>

</footer>


<!-- LOGIN MODAL -->

<div class="modal" id="loginModal">

    <div class="modal-box">

        <span class="close" onclick="closeModal('loginModal')">
            ×
        </span>

        <h2>Login</h2>

        <input
            type="email"
            placeholder="Email address"
        >

        <input
            type="password"
            placeholder="Password"
        >

        <button class="submit" onclick="login()">
            Login
        </button>

        <div class="switch">
            Don't have an account?
            <span onclick="openRegister()">Register</span>
        </div>

    </div>

</div>


<!-- REGISTER MODAL -->

<div class="modal" id="registerModal">

    <div class="modal-box">

        <span class="close" onclick="closeModal('registerModal')">
            ×
        </span>

        <h2>Create Account</h2>

        <input
            type="text"
            placeholder="Full name"
        >

        <input
            type="email"
            placeholder="Email address"
        >

        <input
            type="password"
            placeholder="Create password"
        >

        <button class="submit" onclick="register()">
            Create Account
        </button>

        <div class="switch">
            Already have an account?
            <span onclick="openLogin()">Login</span>
        </div>

    </div>

</div>


<!-- CART MODAL -->

<div class="modal" id="cartModal">

    <div class="modal-box">

        <span class="close" onclick="closeModal('cartModal')">
            ×
        </span>

        <h2>Your Cart</h2>

        <div class="cart-items" id="cartItems">
            Your cart is empty.
        </div>

        <div class="cart-total">
            Total: ₦<span id="cartTotal">0</span>
        </div>

        <button class="checkout" onclick="checkout()">
            Checkout
        </button>

    </div>

</div>


<script>

let cart = [];

function addToCart(name, price){

    cart.push({
        name:name,
        price:price
    });

    updateCart();

    alert(name + " added to cart!");

}


function updateCart(){

    document.getElementById("cartCount").textContent = cart.length;

    let items = document.getElementById("cartItems");

    if(cart.length === 0){

        items.innerHTML = "Your cart is empty.";

        document.getElementById("cartTotal").textContent = "0";

        return;
    }

    let total = 0;

    items.innerHTML = "";

    cart.forEach((item,index)=>{

        total += item.price;

        items.innerHTML += `

            <div class="cart-item">

                <div>
                    <strong>${item.name}</strong><br>
                    ₦${item.price.toLocaleString()}
                </div>

                <button onclick="removeItem(${index})">
                    Remove
                </button>

            </div>

        `;

    });

    document.getElementById("cartTotal").textContent =
        total.toLocaleString();

}


function removeItem(index){

    cart.splice(index,1);

    updateCart();

}


function openCart(){

    document.getElementById("cartModal").style.display = "flex";

}


function openLogin(){

    closeModal("registerModal");

    document.getElementById("loginModal").style.display = "flex";

}


function openRegister(){

    closeModal("loginModal");

    document.getElementById("registerModal").style.display = "flex";

}


function closeModal(id){

    document.getElementById(id).style.display = "none";

}


function login(){

    alert("Login system ready. A real database will be connected later.");

}


function register(){

    alert("Registration system ready. A real database will be connected later.");

}


function checkout(){

    if(cart.length === 0){

        alert("Your cart is empty.");

        return;
    }

    alert(
        "Checkout selected. Payment gateway can be connected next."
    );

}


function filterProducts(category){

    let products =
        document.querySelectorAll(".product");

    products.forEach(product=>{

        if(
            category === "all" ||
            product.dataset.category === category
        ){

            product.style.display = "block";

        }else{

            product.style.display = "none";

        }

    });

}


function searchProducts(){

    let search =
        document
        .getElementById("searchInput")
        .value
        .toLowerCase();

    let products =
        document.querySelectorAll(".product");

    products.forEach(product=>{

        let name =
            product
            .querySelector("h3")
            .textContent
            .toLowerCase();

        if(name.includes(search)){

            product.style.display = "block";

        }else{

            product.style.display = "none";

        }

    });

}


window.onclick = function(event){

    if(event.target.classList.contains("modal")){

        event.target.style.display = "none";

    }

}


</script>

</body>
</html>
