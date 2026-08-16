# Sb
Star link 
;
const state=JSON.parse(localStorage.getItem(KEY)||'{"user":null,"balance":0,"reward":28,"orders":[],"tickets":[],"transactions":[]}');
const save=()=&gt;localStorage.setItem(KEY,JSON.stringify(state));
const money=n=&gt;`₦${Number(n).toLocaleString("en-NG",{minimumFractionDigits:2})}`;
const app=document.getElementById("app");

function toast(t){const x=document.createElement("div");x.className="toast";x.textContent=t;document.body.appendChild(x);setTimeout(()=&gt;x.remove(),2200)}
function header(){return `<header class="top"><div class="logo">nix<b>a</b>roid</div>${state.user?`<span>NGN</span><button class="btn light">Logout</button>`:""}</header>`}
function nav(active){return state.user?`
<button><span>⌂</span><small>Dashboard</small></button>
<button><span>▣</span><small>Bills</small></button>
<button><span></span><small>Boost</small></button>
<button><span>▤</span><small>History</small></button>
<button><span>☰</span><small>Menu</small></button>`:""}

function login(){app.innerHTML=`${header()}<main class="container"><section class="card form">
<h1>Welcome back</h1><p class="muted">Demo account — data stays in your browser.</p>
<div class="field">Email</div>
<div class="field">Password</div>
<button class="btn" style="width:100%">Login</button>
<p class="muted">No account? <a href="#">Create one</a></p></section></main>`}
function register(){app.innerHTML=`${header()}<main class="container"><section class="card form">
<h1>Create account</h1><div class="field">Name</div>
<div class="field">Email</div>
<div class="field">Password</div>
<button class="btn" style="width:100%">Create account</button>
<p><a href="#">Back to login</a></p></section></main>`}
function doLogin(){const email=document.getElementById("email").value.trim();if(!email)return toast("Enter your email");state.user={name:email.split("@")[0],email};save();go("home")}
function doRegister(){const name=document.getElementById("name").value.trim(),email=document.getElementById("email").value.trim(),pass=document.getElementById("pass").value;if(!name||!email||pass.length&lt;6)return toast(&quot;Complete the form&quot;);state.user={name,email};save();go(&quot;home&quot;)}
function logout(){state.user=null;save();login()}

function home(){app.innerHTML=`${header()}<main class="container">
<div class="notice"><span>Enable notifications to stay updated with your account and orders.</span><button class="btn">Allow</button></div>
<section class="wallet"><div class="row between"><div><small>MAIN BALANCE</small><h1 id="bal">${money(state.balance)}</h1></div><button class="btn light">◉</button></div>
<div class="row"><div class="reward"><b>★ Reward</b><br><small>Balance: ${money(state.reward)}</small></div><button class="btn">⊕ Deposit</button></div>
<div class="stats"><div class="stat"><small>DEPOSITS</small><strong>${money(state.transactions.filter(x=&gt;x.type==="Deposit").reduce((a,x)=&gt;a+x.amount,0))}</strong></div><div class="stat"><small>ORDERS</small><strong>${state.orders.length}</strong><small class="gold">0 Active</small></div><div class="stat"><small>SUPPORT</small><strong>${state.tickets.length}</strong><small class="gold">0 Pending</small></div></div></section>
<div class="section-title"> QUICK ACCESS</div><div class="quick">
<button><span></span>Social Boost</button><button><span>☎</span>Airtime</button><button><span>🎟</span>New Ticket</button><button><span>▣</span>Pay Bills</button><button><span></span>History</button></div>
<div class="section-title">OUR SERVICES</div><div class="services"><article class="service purple"><div class="service-icon">▣</div><h2>Bills &amp; Payments</h2><p class="muted">Airtime, data, cable, electricity</p></article><article class="service blue"><div class="service-icon"></div><h2>Social Boost</h2><p class="muted">Followers, likes, views, engagement</p></article></div>
</main>${nav("home")}`}
function toggleBalance(){const b=document.getElementById("bal");b.dataset.hidden=b.dataset.hidden==="1"?"0":"1";b.textContent=b.dataset.hidden==="1"?"₦••••••":money(state.balance)}
function deposit(){const n=prompt("Demo deposit amount (no real payment):","5000");const amount=Number(n);if(!amount||amount&lt;1)return;state.balance+=amount;state.transactions.unshift({type:&quot;Deposit&quot;,amount,date:new Date().toLocaleString()});save();home();toast(&quot;Demo balance updated&quot;)}
function bills(){app.innerHTML=`${header()}<main class="container"><section class="card"><h1>Bills &amp; Payments</h1><p class="muted">Demo interface — no real transaction is processed.</p>
<div class="field">ServiceAirtimeMobile DataCable TVElectricity</div>
<div class="field">Phone / Account number</div><div class="field">Amount</div>
<button class="btn">Continue</button></section></main>${nav("bills")}`}
function buyBill(){const amount=Number(document.getElementById("amt").value);if(!amount||amount&gt;state.balance)return toast("Insufficient demo balance");state.balance-=amount;state.transactions.unshift({type:"Bill",amount:-amount,date:new Date().toLocaleString()});save();home();toast("Demo bill recorded")}
function boost(){app.innerHTML=`${header()}<main class="container"><section class="card"><h1>Social Boost</h1><p class="muted">Demo order form. No social-media action is performed.</p>
<div class="field">ServiceFollowersLikesViewsComments</div><div class="field">Profile / post URL</div><div class="field">Quantity</div><button class="btn">Place demo order</button></section></main>${nav("boost")}`}
function placeOrder(){const q=Number(document.getElementById("qty").value);if(!q)return toast("Enter quantity");state.orders.unshift({service:document.getElementById("service").value,quantity:q,date:new Date().toLocaleString(),status:"Pending"});save();toast("Demo order created");go("history")}
function history(){app.innerHTML=`${header()}<main class="container"><section class="card"><h1>History</h1><div class="section-title">Transactions</div><div class="list">${state.transactions.length?state.transactions.map(x=&gt;`<div class="item"><span>${x.type}<br><small>${x.date}</small></span><b>${money(x.amount)}</b></div>`).join(""):"<div class='empty muted'>No transactions yet.</div>"}</div><div class="section-title">Orders</div><div class="list">${state.orders.length?state.orders.map(x=&gt;`<div class="item"><span>${x.service} × ${x.quantity}<br><small>${x.date}</small></span><b>${x.status}</b></div>`).join(""):"<div class='empty muted'>No orders yet.</div>"}</div></section></main>${nav("history")}`}
function ticket(){const t=prompt("Describe your support issue:");if(!t)return;state.tickets.unshift({text:t,date:new Date().toLocaleString()});save();toast("Demo ticket created")}
function menu(){app.innerHTML=`${header()}<main class="container"><section class="card"><h1>Account</h1><p><b>${state.user.name}</b><br><span class="muted">${state.user.email}</span></p><hr><button class="btn light">Create support ticket</button> <button class="btn">Logout</button></section></main>${nav("menu")}`}
function go(p){({home,bills,boost,history,menu}[p])()}
if(state.user)home();else login();

<!-- /wp:query-no-results -->

<!-- wp:group {"layout":{"type":"default"}} -->
<div class="wp-block-group"><!-- wp:post-template {"align":"full","style":{"spacing":{"blockGap":"var:preset|spacing|20"}},"layout":{"type":"grid","columnCount":3}} -->
<!-- wp:post-featured-image {"isLink":true,"aspectRatio":"4/3","style":{"spacing":{"margin":{"bottom":"var:preset|spacing|20"}}}} /-->

<!-- wp:group {"layout":{"type":"flex","orientation":"vertical","flexWrap":"nowrap"}} -->
<div class="wp-block-group"><!-- wp:post-title {"isLink":true,"className":"no-underline","fontSize":"medium"} /-->

<!-- wp:post-excerpt {"excerptLength":16,"style":{"layout":{"flexSize":"min(2.5rem, 3vw)","selfStretch":"fixed"}},"textColor":"contrast-2","fontSize":"small"} /-->

<!-- wp:spacer {"height":"0px","style":{"layout":{"flexSize":"min(2.5rem, 3vw)","selfStretch":"fixed"}}} -->
<div style="height:0px" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer --></div>
<!-- /wp:group -->
<!-- /wp:post-template -->

<!-- wp:spacer {"height":"var:preset|spacing|40","style":{"spacing":{"margin":{"top":"0","bottom":"0"}}}} -->
<div style="margin-top:0;margin-bottom:0;height:var(--wp--preset--spacing--40)" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:query-pagination {"paginationArrow":"arrow","layout":{"type":"flex","justifyContent":"space-between"}} -->
<!-- wp:query-pagination-previous /-->

<!-- wp:query-pagination-next /-->
<!-- /wp:query-pagination --></div>
<!-- /wp:group --></div>
<!-- /wp:query --></main>
<!-- /wp:group -->

<!-- wp:spacer {"height":"var:preset|spacing|20"} -->
<div style="height:var(--wp--preset--spacing--20)" aria-hidden="true" class="wp-block-spacer"></div>
<!-- /wp:spacer -->

<!-- wp:template-part {"slug":"footer","theme":"pub/assembler"} /-->
