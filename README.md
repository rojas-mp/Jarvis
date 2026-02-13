<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FinStart</title>

<style>
:root{
--azul:#0f172a;
--azul2:#1e293b;
--verde:#22c55e;
--verde2:#16a34a;
}

body{
margin:0;
font-family:'Segoe UI',sans-serif;
background:var(--azul);
color:white;
}

header{
background:var(--azul2);
padding:20px;
text-align:center;
font-size:24px;
font-weight:bold;
}

nav{
display:flex;
justify-content:center;
gap:20px;
flex-wrap:wrap;
padding:10px;
background:rgba(255,255,255,0.05);
}

nav a{
color:white;
text-decoration:none;
}

section{
max-width:1000px;
margin:30px auto;
padding:20px;
}

.card{
background:var(--azul2);
padding:20px;
border-radius:12px;
margin-bottom:20px;
}

input{
width:100%;
padding:10px;
margin-bottom:10px;
border:none;
border-radius:8px;
}

button{
background:var(--verde);
border:none;
padding:10px;
border-radius:8px;
color:white;
font-weight:bold;
cursor:pointer;
}

button:hover{
background:var(--verde2);
}

.hidden{
display:none;
}

.locked{
opacity:0.4;
pointer-events:none;
}

footer{
text-align:center;
padding:20px;
background:rgba(255,255,255,0.05);
font-size:14px;
}
</style>
</head>

<body>

<header>🚀 FinStart</header>

<nav id="menu" class="hidden">
<a href="#inicio">Início</a>
<a href="#calculadoras">Calculadoras</a>
<a href="#premium">Premium</a>
<a href="#" onclick="logout()">Sair</a>
</nav>

<section id="auth">

<div class="card">
<h2>Login</h2>
<input type="text" id="loginEmail" placeholder="Email">
<input type="password" id="loginSenha" placeholder="Senha">
<button onclick="login()">Entrar</button>
</div>

<div class="card">
<h2>Criar Conta</h2>
<input type="text" id="cadEmail" placeholder="Email">
<input type="password" id="cadSenha" placeholder="Senha">
<button onclick="cadastrar()">Cadastrar</button>
</div>

</section>

<section id="site" class="hidden">

<div id="inicio" class="card">
<h2>Bem-vindo!</h2>
<p>Investir é fazer seu dinheiro crescer ao longo do tempo. Comece pequeno e evolua.</p>
</div>

<div id="calculadoras" class="card">
<h2>🧮 Calculadora</h2>
<input type="number" id="renda" placeholder="Renda">
<input type="number" id="gastos" placeholder="Gastos">
<button onclick="calc()">Calcular</button>
<p id="resultado"></p>
</div>

<div id="premium">
<div class="card">
<h2>💎 Plano Premium</h2>
<p>R$ 20,00 por mês</p>
<button onclick="assinar()">Assinar Premium</button>
</div>

<div class="card locked" id="areaPremium">
<h2>🚀 IA Avançada</h2>
<input type="text" id="perguntaPremium" placeholder="Pergunte algo...">
<button onclick="responderPremium()">Perguntar</button>
<p id="respostaPremium"></p>
</div>
</div>

</section>

<footer>
Site educativo. Não é recomendação financeira oficial.
</footer>

<script>

let usuarioLogado = null;
let premiumAtivo = false;

function cadastrar(){
let email = cadEmail.value;
let senha = cadSenha.value;

if(email && senha){
localStorage.setItem("usuario", JSON.stringify({email, senha, premium:false}));
alert("Conta criada!");
}
}

function login(){
let email = loginEmail.value;
let senha = loginSenha.value;
let usuario = JSON.parse(localStorage.getItem("usuario"));

if(usuario && usuario.email===email && usuario.senha===senha){
usuarioLogado = usuario;
premiumAtivo = usuario.premium;
auth.classList.add("hidden");
site.classList.remove("hidden");
menu.classList.remove("hidden");
if(premiumAtivo){
areaPremium.classList.remove("locked");
}
}else{
alert("Login inválido");
}
}

function logout(){
location.reload();
}

function calc(){
let r = parseFloat(renda.value)||0;
let g = parseFloat(gastos.value)||0;
resultado.innerHTML="Sobra: R$ "+(r-g).toFixed(2);
}

function assinar(){
let usuario = JSON.parse(localStorage.getItem("usuario"));
usuario.premium = true;
localStorage.setItem("usuario", JSON.stringify(usuario));
premiumAtivo = true;
areaPremium.classList.remove("locked");
alert("Premium ativado!");
}

function responderPremium(){
if(!premiumAtivo) return;
let pergunta = perguntaPremium.value.toLowerCase();
let resposta="Estratégia recomendada: diversifique.";
if(pergunta.includes("1000")){
resposta="Com R$1000: 60% renda fixa, 30% fundos, 10% variável.";
}
respostaPremium.innerHTML=resposta;
}

</script>

</body>
</html>
