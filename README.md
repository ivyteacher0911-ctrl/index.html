<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Date With Me ❤️</title>

<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Quicksand:wght@400;700&display=swap" rel="stylesheet">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    height:100vh;
    overflow:hidden;
    display:flex;
    justify-content:center;
    align-items:center;
    background:linear-gradient(135deg,#ffe0ec,#fff5f8,#ffd6e7);
    font-family:'Quicksand',sans-serif;
}

.card{
    width:700px;
    background:white;
    border-radius:35px;
    padding:50px;
    text-align:center;
    box-shadow:0 15px 40px rgba(0,0,0,0.15);
    border:5px solid #ffd3e1;
    position:relative;
}

#cat{
    width:240px;
    margin-bottom:25px;
    animation:floatCat 2s infinite ease-in-out;
}

@keyframes floatCat{
    0%{
        transform:translateY(0);
    }
    50%{
        transform:translateY(-10px);
    }
    100%{
        transform:translateY(0);
    }
}

h1{
    font-family:'Pacifico',cursive;
    color:#ff6699;
    font-size:40px;
    min-height:120px;
    line-height:1.5;
}

.buttons{
    margin-top:30px;
}

button{
    border:none;
    padding:18px 45px;
    font-size:24px;
    border-radius:50px;
    cursor:pointer;
    font-family:'Quicksand',sans-serif;
    font-weight:bold;
    transition:.2s;
}

#yes{
    background:#ff6f9f;
    color:white;
    margin-right:25px;
}

#yes:hover{
    transform:scale(1.1);
}

#no{
    background:#ececec;
    color:#666;
    position:fixed;
}

.hearts{
    position:fixed;
    width:100%;
    height:100%;
    left:0;
    top:0;
    pointer-events:none;
}

.heart{
    position:absolute;
    animation:fly 5s linear forwards;
}

@keyframes fly{
    from{
        transform:translateY(0);
        opacity:1;
    }
    to{
        transform:translateY(-700px);
        opacity:0;
    }
}
</style>
</head>

<body>

<div class="card">

    <img src="image(53).png" id="cat">

    <h1 id="text"></h1>

    <div class="buttons" id="buttons" style="display:none;">
        <button id="yes">💖 Yes 💖</button>
        <button id="no">🙈 No</button>
    </div>

</div>

<div class="hearts" id="hearts"></div>

<script>

const message = "Bạn có muốn đi hẹn hò với em không? 💕";
let i = 0;

setTimeout(()=>{
    typeWriter();
},1500);

function typeWriter(){

    if(i < message.length){
        document.getElementById("text").innerHTML += message.charAt(i);
        i++;
        setTimeout(typeWriter,90);
    }
    else{
        document.getElementById("buttons").style.display="block";
    }
}

const noBtn = document.getElementById("no");

document.addEventListener("mousemove",function(e){

    const rect = noBtn.getBoundingClientRect();

    const x = rect.left + rect.width/2;
    const y = rect.top + rect.height/2;

    const distance = Math.sqrt(
        (e.clientX-x)*(e.clientX-x) +
        (e.clientY-y)*(e.clientY-y)
    );

    if(distance < 180){

        noBtn.style.transform="scale(0.5)";

        let newX = e.clientX + 35;
        let newY = e.clientY + 20;

        if(newX > window.innerWidth-100){
            newX = e.clientX - 120;
        }

        if(newY > window.innerHeight-50){
            newY = e.clientY - 50;
        }

        noBtn.style.left = newX + "px";
        noBtn.style.top = newY + "px";
    }
});

document.getElementById("yes").onclick = function(){

    document.querySelector(".card").innerHTML = `
        <img src="image(53).png" width="250">

        <h1 style="
            color:#ff6699;
            margin-top:25px;
            font-family:Pacifico;
        ">
            Yaaay!!! 💖<br>
            Em biết mà 🥰💕
        </h1>
    `;

    createHearts();
}

function createHearts(){

    setInterval(()=>{

        const heart = document.createElement("div");

        heart.className="heart";
        heart.innerHTML="💖";

        heart.style.left=Math.random()*100+"%";
        heart.style.bottom="-30px";
        heart.style.fontSize=(20+Math.random()*30)+"px";

        document.getElementById("hearts").appendChild(heart);

        setTimeout(()=>{
            heart.remove();
        },5000);

    },250);
}

</script>

</body>
</html>
