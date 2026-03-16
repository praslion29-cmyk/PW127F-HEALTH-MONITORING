# PW127F-HEALTH-MONITORING
<!DOCTYPE html>


<head>

<title>PW127F Engine Health Monitoring</title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>

body{
font-family: Arial;
margin:40px;
background:#f4f6f8;
}

h1{
color:#003366;
}

.container{
background:white;
padding:20px;
border-radius:10px;
box-shadow:0 0 10px rgba(0,0,0,0.1);
}

input{
margin:5px;
padding:5px;
}

button{
padding:10px 20px;
background:#003366;
color:white;
border:none;
border-radius:5px;
}

.green{color:green;}
.yellow{color:orange;}
.red{color:red;}

</style>

</head>


<body>

<div class="container">

<img src="pw.png" width="120">

<h1>PW127F ENGINE HEALTH MONITORING</h1>

<h3>Create by Y.A. PRASETYA PUTRA</h3>

<hr>

<h3>Aircraft Information</h3>

Date
<input type="date" id="date">

Aircraft Reg
<input type="text" id="reg">

Engine Number
<input type="text" id="eng">

Route
<input type="text" id="route">

<hr>

<h3>Flight Power Parameters</h3>

Torque %
<input id="tq">

NP %
<input id="np">

ITT °C
<input id="itt">

NH %
<input id="nh">

Fuel Flow
<input id="ff">

Oil Pressure
<input id="oilp">

Oil Temp
<input id="oilt">

<br><br>

<button onclick="checkEngine()">CHECK ENGINE</button>

<h3 id="status"></h3>
<p id="recommendation"></p>

<hr>

<h2>Engine Trend Monitoring</h2>

<canvas id="ittChart"></canvas>
<br>
<canvas id="nhChart"></canvas>
<br>
<canvas id="ffChart"></canvas>

</div>


<script>

let cycle=[]
let ittData=[]
let nhData=[]
let ffData=[]

function checkEngine(){

let tq = parseFloat(document.getElementById("tq").value)
let itt = parseFloat(document.getElementById("itt").value)
let nh = parseFloat(document.getElementById("nh").value)
let ff = parseFloat(document.getElementById("ff").value)

let status=""
let rec=""

if(itt < 700){

status="<span class='green'>NORMAL</span>"
rec="Engine parameters within limit"

}

else if(itt < 740){

status="<span class='yellow'>APPROACHING LIMIT</span>"
rec="Monitor turbine temperature trend"

}

else{

status="<span class='red'>OVER LIMIT</span>"
rec="Inspect hot section and turbine efficiency"

}

document.getElementById("status").innerHTML=status
document.getElementById("recommendation").innerHTML=rec


let c = cycle.length + 1

cycle.push(c)
ittData.push(itt)
nhData.push(nh)
ffData.push(ff)

updateCharts()

}

function updateCharts(){

new Chart(document.getElementById("ittChart"),{
type:'line',
data:{
labels:cycle,
datasets:[{
label:'ITT Trend',
data:ittData
}]
}
})


new Chart(document.getElementById("nhChart"),{
type:'line',
data:{
labels:cycle,
datasets:[{
label:'NH Trend',
data:nhData
}]
}
})


new Chart(document.getElementById("ffChart"),{
type:'line',
data:{
labels:cycle,
datasets:[{
label:'Fuel Flow Trend',
data:ffData
}]
}
})

}

</script>
