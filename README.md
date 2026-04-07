# Resellsweden
<!DOCTYPE html>
<html lang="sv">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Golf Resell Sweden</title>
<style>
body { margin:0; font-family: Arial, sans-serif; background:#f9f9f9; }
a { text-decoration:none; color:inherit; }

.top-banner { background:#16a34a; color:white; font-weight:bold; overflow:hidden; white-space:nowrap; }
.top-banner span { display:inline-block; padding:10px 0; animation:scrollText 15s linear infinite; }
@keyframes scrollText { 0% { transform:translateX(100%);} 100% { transform:translateX(-100%);} }

header { background:white; position:sticky; top:0; z-index:100; box-shadow:0 2px 5px rgba(0,0,0,0.1);}
.nav { display:flex; justify-content:space-between; align-items:center; padding:15px 30px; }
.menu { display:flex; gap:20px; position:relative; font-weight:bold; font-size:14px; }
.menu div { cursor:pointer; position:relative; padding:6px 10px; }
.dropdown { display:none; position:absolute; top:35px; background:white; border:1px solid #eee; flex-direction:column; z-index:200; min-width:200px; }
.dropdown div { padding:10px; cursor:pointer; }
.dropdown div:hover { background:#f0f0f0; }
.show { display:flex; flex-direction:column; }

/* HERO */
.hero { height:80vh; background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), url('https://images.unsplash.com/photo-1592919505780-303950717480') center/cover no-repeat; display:flex; align-items:center; justify-content:center; text-align:center; color:white; }
.hero-box { background:rgba(0,0,0,0.5); padding:30px; border-radius:10px; max-width:700px; }
.hero h1 { font-size:36px; margin-bottom:10px; font-weight:700; }
.hero p { font-size:14px; margin:8px 0; line-height:1.6; }

/* INFO UNDER HERO */
.hero-info { margin-top:15px; font-size:14px; }

/* PRODUKTER */
.section { padding:50px 30px; }
.products { display:flex; flex-wrap:wrap; gap:15px; padding:20px 0; }
.card { width: calc(33.33% - 10px); background:white; padding:10px; text-align:center; border-radius:10px; box-shadow:0 0 5px rgba(0,0,0,0.1); cursor:pointer; transition: transform 0.2s; }
.card:hover { transform: scale(1.05); }
.card img { width:100%; height:180px; object-fit:cover; border-radius:10px; }
.card p { font-weight:bold; margin:5px 0; }
.btn { background:#16a34a; color:white; padding:8px 12px; margin-top:5px; cursor:pointer; border:none; border-radius:5px; }

/* VARUKORG KNAPP */
.cart { background:#16a34a; color:white; padding:10px 18px; border-radius:25px; font-size:16px; cursor:pointer; }

/* FULLSKÄRM PRODUKTSIDA */
.product-page-full { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:white; z-index:1000; overflow-y:auto; padding:40px; box-sizing:border-box; }
.product-page-full img { width:300px; height:300px; object-fit:cover; border-radius:10px; display:block; margin-bottom:15px; }
.product-page-full button { background:#16a34a; color:white; border:none; padding:10px 15px; border-radius:5px; cursor:pointer; margin-top:10px; font-size:16px; }
.product-page-full h2 { margin-bottom:10px; }
.product-page-full p { margin-bottom:10px; }

/* POPUP VARUKORG */
#cartContent { display:none; position:fixed; top:50%; left:50%; transform:translate(-50%,-50%); width:350px; max-height:70%; z-index:10000; box-shadow:0 10px 25px rgba(0,0,0,0.3); background:white; border-radius:15px; padding:20px; overflow-y:auto; }

/* SÖK */
.search-box { display:flex; justify-content:flex-end; gap:10px; margin-bottom:10px; }
.search-box input { padding:6px 10px; width:250px; border-radius:5px; border:1px solid #ccc; display:none; }
.search-box button { padding:6px 10px; border:none; background:#16a34a; color:white; border-radius:5px; cursor:pointer; font-size:18px; }

/* PIL FÖR VISA ALLA */
.showAllBtn { font-size:16px; cursor:pointer; color:#16a34a; font-weight:bold; padding:5px; }

</style>
</head>
<body>

<div class="top-banner"><span>Just nu 10% rabatt på utvalda produkter!</span></div>

<header>
<div class="nav">
<h2 onclick="window.scrollTo(0,0)" style="cursor:pointer;">Golf Resell Sweden</h2>
<div class="menu">
<div id="golfBtn">Golfbollar
    <div id="golfMenu" class="dropdown"></div>
</div>
<div id="tillbehorBtn">Tillbehör
    <div id="tillbehorMenu" class="dropdown"></div>
</div>
<div onclick="document.getElementById('info').scrollIntoView()">Om oss</div>
<div onclick="document.getElementById('kontakt').scrollIntoView()">Kontakt</div>
<div class="cart" onclick="toggleCart()">🛒 <span id="cartCount">0</span></div>
<div class="search-box">
<input type="text" id="searchInput" placeholder="Sök golfboll...">
<button onclick="toggleSearch()">🔍</button>
</div>
</div>
</div>
</header>

<!-- HERO -->
<section class="hero">
<div class="hero-box">
<h1>Golf Resell Sweden</h1>
<p>Vi är två 15-åriga killar som älskar golf.</p>
<p>Vi säljer begagnade premiumbollar och tillbehör med hög kvalitet.</p>
<div class="hero-info">
<p>🚚 Fri frakt över 400 kr &nbsp; ⏱ 2-5 arbetsdagar &nbsp; 🌍 Leverans i hela Sverige</p>
</div>
</div>
</section>

<!-- BÄSTSÄLJARE -->
<section class="section">
<h2>Bästsäljare 
<span class="showAllBtn" onclick="showAllBollar()">➤ Visa alla</span>
</h2>
<div class="products" id="golfProducts"></div>
</section>

<!-- FULLSKÄRM PRODUKTSIDA -->
<div class="product-page-full" id="productPageFull">
<button class="close-btn" onclick="closeProductPageFull()">× Stäng</button>
<img id="productImgFull" src="">
<h2 id="productNameFull"></h2>
<p id="productDescFull"></p>
<p id="productPriceFull"></p>
<button onclick="addToCartWithAnimation()">Lägg till i kundvagn</button>
<h3>Recensioner</h3>
<p>⭐️⭐️⭐️⭐️☆ Bra kvalitet och prisvärd!</p>
<p>⭐️⭐️⭐️⭐️⭐ Fantastiskt skick på bollarna.</p>
</div>

<!-- POPUP VARUKORG -->
<div id="cartContent"></div>

<section class="section section-alt" id="info">
<h2>Om oss</h2>
<p>Vi är två kompisar på 15 år som brinner för golf och vill göra sporten mer tillgänglig. Vi handplockar begagnade premiumbollar och erbjuder dem till fantastiska priser. Vi älskar sporten och vill hjälpa fler att upptäcka glädjen med golf.</p>
<p>Följ oss på sociala medier för tips och uppdateringar!</p>
</section>

<section class="section" id="kontakt" style="background:#16a34a; color:white; text-align:center;">
<h2>Kontakt & Sociala medier</h2>
<p>Mail: info@golfresell.se</p>
<p>Telefon: 0701234567</p>
<p>Instagram: <a href=tiktok.com/@golfresellsweden target="_blank" style="color:white;">@golfresell</a></p>
<p>TikTok: <a href=tiktok.com/@golfresellswedentarget="_blank" style="color:white;">@golfresell</a></p>
<p>Vinted: <a href="https://www.vinted.se/member/267730130-golfresellsweden" target="_blank" style="color:white;">@GolfResellSweden</a></p>
</section>

<script>
// CART
let cart = 0;
let cartItems = [];
function addToCart(item) {
    cart++;
    document.getElementById("cartCount").innerText = cart;
    if(item) cartItems.push(item);
    renderCart();
}
function addToCartWithAnimation() {
    const name = document.getElementById("productNameFull").innerText;
    const price = document.getElementById("productPriceFull").innerText;
    addToCart({name, price});
    alert(name + " lades till i kundvagnen!");
}
function renderCart() {
    const container = document.getElementById("cartContent");
    container.innerHTML = "";
    if(cartItems.length === 0) { container.innerHTML = "<p>Varukorgen är tom</p>"; return; }
    cartItems.forEach((item,i)=>{
        const div = document.createElement("div"); div.className="cart-item";
        div.innerHTML = `<p>${item.name}</p><p>${item.price}</p>`;
        container.appendChild(div);
    });
    const payBtn = document.createElement("button");
    payBtn.innerText = "Betala med Swish";
    payBtn.style.width = "100%"; payBtn.style.marginTop="10px";
    payBtn.onclick = () => {
        let total = cartItems.reduce((sum,item)=>sum+parseInt(item.price.replace(/\D/g,'')),0);
        let swishNumber = "1234567890";
        alert(`Skicka ${total} kr till Swish-nummer ${swishNumber} för att slutföra betalningen.\n\nObs: Detta är en simulerad betalning.`);
    };
    container.appendChild(payBtn);
}
function toggleCart() {
    const c = document.getElementById("cartContent");
    if(c.style.display==="block"){ c.style.display="none"; } else { c.style.display="block"; }
}

// SÖK
function toggleSearch(){
    const input = document.getElementById("searchInput");
    if(input.style.display==="block"){ input.style.display="none"; } else { input.style.display="block"; input.focus(); }
}
function searchBollar(){
    const term = document.getElementById("searchInput").value.toLowerCase();
    const filtered = golfProductsData.filter(p=>p.name.toLowerCase().includes(term));
    renderBollar(filtered);
}

// PRODUKTSIDA
function openProductPageFull(name,img,desc,price){
    document.getElementById("productPageFull").style.display="block";
    document.getElementById("productImgFull").src=img;
    document.getElementById("productNameFull").innerText=name;
    document.getElementById("productDescFull").innerText=desc;
    document.getElementById("productPriceFull").innerText=price;
    window.scrollTo(0,0);
}
function closeProductPageFull(){ document.getElementById("productPageFull").style.display="none"; }

// BÄSTSÄLLARE DATA
const golfProductsData = [
    {name:"Titleist PRO V1", img:"prov1.jpg", desc:"Premium golfboll för högsta kvalitet.", price:"299 kr"},
    {name:"Callaway Chrome Soft", img:"https://cdn.pixabay.com/photo/2017/09/26/19/48/golf-ball-2782008_1280.jpg", desc:"Mjuk och kontrollerad boll.", price:"249 kr"},
    {name:"TaylorMade TP5", img:"https://cdn.pixabay.com/photo/2017/09/26/19/48/golf-ball-2782008_1280.jpg", desc:"Optimal spinn och distans.", price:"289 kr"},
    {name:"Florida Mix 50", img:"https://cdn.pixabay.com/photo/2017/09/26/19/48/golf-ball-2782008_1280.jpg", desc:"Mix av olika premiumbollar.", price:"150 kr"}
];

const container = document.getElementById("golfProducts");
function renderBollar(list){
    container.innerHTML="";
    list.forEach(p=>{
        let card = document.createElement("div"); card.className="card";
        card.innerHTML=`<img src="${p.img}" onerror="this.src='https://via.placeholder.com/150'"><p>${p.name}</p>
        <button class="btn" onclick="openProductPageFull('${p.name}','${p.img}','${p.desc}','${p.price}')">Se mer</button>`;
        container.appendChild(card);
    });
}
// Visa endast 3 första (bästsäljare) först
renderBollar(golfProductsData.slice(0,3));
function showAllBollar(){ renderBollar(golfProductsData); }

</script>
</body>
</html>
