<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Password Strength Checker</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, sans-serif;
}

body{
    background:linear-gradient(135deg,#38534edf,#00f2fe);
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

.container{
    background:#edc7a1;
    padding:25px;
    width:350px;
    border-radius:60px;
    box-shadow:0 10px 20px rgba(182, 167, 119, 0.2);
}

h2{
    text-align:center;
    margin: bottom 30px;
}

input{
    width:100%;
    padding:12px;
    border:2px solid #ccc;
    border-radius:6px;
    font-size:16px;
}

.bar{
    width:100%;
    height:10px;
    background:#ec3e3e;
    border: radius 10px;
    margin-top:15px;
    overflow:hidden;
}

#progress{
    height:100%;
    width:0%;
    background:rgb(217, 70, 153);
    transition:.3s;
}

#text{
    margin-top:12px;
    font-weight:bold;
    text-align:center;
}

ul{
    margin-top:15px;
    padding-left:20px;
}

li{
    color:red;
    margin:5px 0;
}

.valid{
    color:green;
}
</style>

</head>
<body>

<div class="container">
    <h2>Password Strength Checker</h2>

    <input type="password" id="password" placeholder="Enter Password">

    <div class="bar">
        <div id="progress"></div>
    </div>

    <p id="text">Strength:</p>
    <p id="strength">strength:</p>

    <ul>
        <li id="len">At least 8 characters</li>
        <li id="up">Uppercase letter</li>
        <li id="low">Lowercase letter</li>
        <li id="num">Number</li>
        <li id="sp">Special character</li>
        <li id="no-spaces">No spaces</li>
      
    </ul>
</div>

<script>
const password=document.getElementById("password");
const showpassword=document.getElementById("showpassword");
const progress=document.getElementById("progress");
const text=document.getElementById("text");


password.addEventListener("input",()=>{

let value=password.value;
let score=0;

check(value.length>=8,"len");
check(/[A-Z]/.test(value),"up");
check(/[a-z]/.test(value),"low");
check(/[0-9]/.test(value),"num");
check(/[^A-Za-z0-9]/.test(value),"sp");

function check(condition,id){
    if(condition){
        score++;
        document.getElementById(id).classList.add("valid");
    }else{
        document.getElementById(id).classList.remove("valid");
    }
}

if(value.length===0){
    progress.style.width="0%";
    text.innerHTML="Strength:";
    return;
}
if(this.checked){
    password.type="text";
}else{
    password.type="password";
}   

if(score<=1){
    progress.style.width="20%";
    progress.style.background="red";
    text.innerHTML="Strength: Very Weak";
}
else if(score==2){
    progress.style.width="40%";
    progress.style.background="orange";
    text.innerHTML="Strength: Weak";
}
else if(score==3){
    progress.style.width="60%";
    progress.style.background="gold";
    text.innerHTML="Strength: Medium";
}
else if(score==4){
    progress.style.width="80%";
    progress.style.background="dodgerblue";
    text.innerHTML="Strength: Strong";
}
else{
    progress.style.width="100%";
    progress.style.background="green";
    text.innerHTML="Strength: Very Strong";
}

});
</script>

</body>
</html>
