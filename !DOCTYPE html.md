<!DOCTYPE html>  
<html>  
<head>  
<meta charset="UTF-8">  
  
<title>Carwash Stankovic</title>  
  
<!-- 📱 iOS APP MODE -->  
<meta name="apple-mobile-web-app-capable" content="yes">  
<meta name="apple-mobile-web-app-status-bar-style" content="black">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
  
<!-- 📲 ICON -->  
<link rel="apple-touch-icon" href="icon.png">  
  
<style>  
body {  
    margin:0;  
    font-family: -apple-system;  
    background:#0f0f0f;  
    color:white;  
}  
  
.header {  
    background:#111;  
    padding:15px;  
    font-size:20px;  
    text-align:center;  
    font-weight:bold;  
}  
  
input, button {  
    width:90%;  
    margin:10px;  
    padding:12px;  
    border-radius:10px;  
    border:none;  
    font-size:16px;  
}  
  
button {  
    background:#0a84ff;  
    color:white;  
}  
  
.card {  
    background:#1c1c1e;  
    margin:10px;  
    padding:12px;  
    border-radius:12px;  
}  
</style>  
  
</head>  
  
<body>  
  
<div class="header">🚗 Carwash Stankovic</div>  
  
<input id="plate" placeholder="Tablica">  
<input id="phone" placeholder="Telefon">  
<input id="email" placeholder="Email (opciono)">  
  
<button onclick="add()">Dodaj mušteriju</button>  
  
<h3 style="padding:10px;">💰 Zarada: <span id="money">0</span> RSD</h3>  
  
<div id="list"></div>  
  
<script>  
let data = JSON.parse(localStorage.getItem("cw") || "[]");  
let price = 500;  
  
function save(){  
    localStorage.setItem("cw", JSON.stringify(data));  
}  
  
function add(){  
    data.push({  
        plate: plate.value,  
        phone: phone.value,  
        email: email.value,  
        wash: 0  
    });  
    save();  
    render();  
}  
  
function wash(i){  
    data[i].wash++;  
  
    let msg = `Carwash Stankovic\nTablica: ${data[i].plate}\nPranja: ${data[i].wash}`;  
  
    if(data[i].email){  
        window.location = `mailto:${data[i].email}?subject=Pranje&body=${encodeURIComponent(msg)}`;  
    } else {  
        window.location = `sms:${data[i].phone}?body=${encodeURIComponent(msg)}`;  
    }  
  
    save();  
    render();  
}  
  
function render(){  
    list.innerHTML = "";  
    let total = 0;  
  
    data.forEach((c,i)=>{  
        total += c.wash * price;  
  
        list.innerHTML += `  
        <div class="card">  
            <b>${c.plate}</b><br>  
            Pranja: ${c.wash}<br>  
            ${c.wash>=10 ? "🎁 GRATIS PRANJE" : ""}  
            <br><br>  
            <button onclick="wash(${i})">+ Novo pranje</button>  
        </div>`;  
    });  
  
    money.innerText = total;  
}  
  
render();  
</script>  
  
</body>  
</html>  
