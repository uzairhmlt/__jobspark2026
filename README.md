<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JobSpark 2026 - Premium Dashboard</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Poppins,sans-serif;}
body{background:#f2f7ff;}
header{
background:linear-gradient(90deg,#004aad,#00c853);
color:white;padding:15px 30px;
display:flex;justify-content:space-between;align-items:center;
}
header h1{font-size:24px;}
button{padding:8px 15px;border:none;border-radius:5px;cursor:pointer;}
.container{padding:30px;}
.card{
background:white;
padding:20px;
border-radius:10px;
box-shadow:0 4px 15px rgba(0,0,0,0.1);
margin-bottom:20px;
}
input{
width:100%;
padding:10px;
margin:10px 0;
border-radius:5px;
border:1px solid #ccc;
}
.btn-primary{
background:#004aad;color:white;
}
.btn-green{
background:#00c853;color:white;
}
.hidden{display:none;}
footer{
text-align:center;
padding:20px;
background:#004aad;
color:white;
margin-top:30px;
}
</style>
</head>

<body>

<header>
<h1>JobSpark 2026</h1>
<div id="userSection">
<button onclick="showLogin()">Login</button>
<button onclick="showSignup()">Signup</button>
</div>
</header>

<div class="container">

<!-- Signup -->
<div id="signupBox" class="card hidden">
<h2>Create Account</h2>
<input type="text" id="signupName" placeholder="Full Name">
<input type="email" id="signupEmail" placeholder="Email">
<input type="password" id="signupPass" placeholder="Password">
<button class="btn-primary" onclick="signup()">Signup</button>
</div>

<!-- Login -->
<div id="loginBox" class="card hidden">
<h2>Login</h2>
<input type="email" id="loginEmail" placeholder="Email">
<input type="password" id="loginPass" placeholder="Password">
<button class="btn-primary" onclick="login()">Login</button>
</div>

<!-- Dashboard -->
<div id="dashboard" class="hidden">

<div class="card">
<h2>Welcome, <span id="userName"></span></h2>
<h3>Balance: ₹<span id="balance">0</span></h3>
</div>

<div class="card">
<h3>Deposit</h3>
<input type="number" id="depositAmount" placeholder="Enter Amount">
<select>
<option>UPI</option>
<option>Paytm</option>
<option>Bank Transfer</option>
</select>
<button class="btn-green" onclick="deposit()">Deposit</button>
</div>

<div class="card">
<h3>Withdraw</h3>
<input type="number" id="withdrawAmount" placeholder="Enter Amount">
<button class="btn-primary" onclick="withdraw()">Withdraw</button>
</div>

</div>

<!-- Admin Panel -->
<div id="adminPanel" class="card hidden">
<h2>Admin Panel</h2>
<p>Total Registered Users: <span id="totalUsers"></span></p>
</div>

</div>

<footer>
Founder: Vedika Khanna | © 2026 JobSpark
</footer>

<script>
function showSignup(){
document.getElementById('signupBox').classList.remove('hidden');
document.getElementById('loginBox').classList.add('hidden');
}
function showLogin(){
document.getElementById('loginBox').classList.remove('hidden');
document.getElementById('signupBox').classList.add('hidden');
}

function signup(){
let name=document.getElementById('signupName').value;
let email=document.getElementById('signupEmail').value;
let pass=document.getElementById('signupPass').value;

localStorage.setItem(email,JSON.stringify({name:name,password:pass,balance:0}));
alert("Account Created Successfully");
}

function login(){
let email=document.getElementById('loginEmail').value;
let pass=document.getElementById('loginPass').value;
let user=JSON.parse(localStorage.getItem(email));

if(user && user.password===pass){
document.getElementById('dashboard').classList.remove('hidden');
document.getElementById('userName').innerText=user.name;
document.getElementById('balance').innerText=user.balance;
document.getElementById('loginBox').classList.add('hidden');
document.getElementById('userSection').innerHTML='<button onclick="logout()">Logout</button>';
}
else{
alert("Invalid Login");
}
}

function deposit(){
let amount=parseInt(document.getElementById('depositAmount').value);
let email=document.getElementById('loginEmail').value;
let user=JSON.parse(localStorage.getItem(email));
user.balance+=amount;
localStorage.setItem(email,JSON.stringify(user));
document.getElementById('balance').innerText=user.balance;
alert("Deposit Successful");
}

function withdraw(){
let amount=parseInt(document.getElementById('withdrawAmount').value);
let email=document.getElementById('loginEmail').value;
let user=JSON.parse(localStorage.getItem(email));

if(user.balance>=amount){
user.balance-=amount;
localStorage.setItem(email,JSON.stringify(user));
document.getElementById('balance').innerText=user.balance;
alert("Withdraw Successful");
}else{
alert("Insufficient Balance");
}
}

function logout(){
location.reload();
}

document.getElementById('totalUsers').innerText=localStorage.length;
</script>

</body>
</html>
