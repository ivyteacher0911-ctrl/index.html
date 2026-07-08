<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Date with me?</title>

<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Quicksand:wght@400;700&display=swap" rel="stylesheet">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    background:linear-gradient(135deg,#ffd6e7,#ffeef5,#fff5f8);
    overflow:hidden;
    font-family:'Quicksand',sans-serif;
}

.card{
    background:rgba(255,255,255,0.95);
    padding:50px;
    border-radius:35px;
    box-shadow:0 15px 35px rgba(0,0,0,0.15);
    text-align:center;
    width:700px;
    position:relative;
    border:5px solid #ffd1dc;
}

h1{
    font-family:'Pacifico',cursive;
    color:#ff5c8a;
    font-size:40px;
    min-height:120px;
}

.buttons{
    margin-top:40px;
    position:relative;
    height:120px;
}

button{
    border:none;
    padding:18px 45px;
    font-size:24px;
    border-radius:50px;
    cursor:pointer;
    transition:0.3s;
    font-family:'Quicksand',sans-serif;
    font-weight:bold;
}

#yes{
    background:#ff7aa2;
    color:white;
    margin-right:25px;
}

#yes:hover{
    transform:scale(1.1);
}

#no{
    background:#d8d8d8;
    color:#555;
    position:absolute;
}

.hearts{
    position:absolute;
    width:100%;
    height:100%;
    pointer-events:none;
    overflow:hidden;
    left:0;
    top:0;
}

.heart{
    position:absolute;
    color:#ff8fb1;
    animation:float 5s linear infinite;
}

@keyframes float{
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
    <h1 id="text"></h1>

    <div class="buttons">
        <button id="yes">💖 Yes 💖</button>
        <button id="no">🙈 No</button>
    </div>
</div>

<div class="hearts" id="hearts"></div>

<script>
// Hiệu ứng gõ chữ
const message = "Bạn có muốn đi hẹn hò với em không? 💕";
let i = 0;

function typeWriter(){
    if(i < message.length){
        document.getElementById("text").innerHTML += message.charAt(i);
        i++;
        setTimeout(typeWriter, 90);
    }
}
typeWriter();


// Nút No chạy trốn
const noBtn = document.getElementById("no");

document.addEventListener("mousemove", function(e){

    const mouseX = e.clientX;
    const mouseY = e.clientY;

    const rect = noBtn.getBoundingClientRect();

    const distance = Math.sqrt(
        (mouseX - (rect.left + rect.width/2))**2 +
        (mouseY - (rect.top + rect.height/2))**2
    );

    if(distance < 120){

        const maxX = window.innerWidth - rect.width - 20;
        const maxY = window.innerHeight - rect.height - 20;

        const randomX = Math.random() * maxX;
        const randomY = Math.random() * maxY;

        noBtn.style.left = randomX + "px";
        noBtn.style.top = randomY + "px";
    }
});


// Khi nhấn Yes
document.getElementById("yes").onclick = function(){

    document.querySelector(".card").innerHTML =
    `
    <h1 style="
        color:#ff5c8a;
        font-size:42px;
        font-family:Pacifico;
    ">
        Yaaay! 💕<br>
        Em biết mà! 💖
    </h1>
    `;
};


// Tim bay
setInterval(()=>{
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "💗";
    heart.style.left = Math.random()*100+"%";
    heart.style.fontSize = (20 + Math.random()*30)+"px";

    document.getElementById("hearts").appendChild(heart);

    setTimeout(()=>{
        heart.remove();
    },5000);

},400);
</script>

</body>
</html>
