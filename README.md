<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Đi hẹn hò hok mom?</title>

<link href="https://fonts.googleapis.com/css2?family=Baloo+2:wght@400;600;700&family=Nunito:wght@400;700&display=swap" rel="stylesheet">

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
    overflow:hidden;
    background:linear-gradient(135deg,#ffe4ef,#fff4f8,#ffd8e8);
    font-family:'Nunito',sans-serif;
}

.card{
    text-align:center;
    width:90%;
    max-width:700px;
}

#cat{
    width:260px;
    animation:float 2s infinite ease-in-out;
}

@keyframes float{
    50%{
        transform:translateY(-12px);
    }
}

#start{
    margin-top:20px;
    color:#ff5f95;
    font-size:28px;
    font-family:'Baloo 2',cursive;
    line-height:1.5;
    cursor:pointer;
    animation:blink 1s infinite;
}

@keyframes blink{
    50%{
        opacity:0.5;
    }
}

h1{
    margin-top:30px;
    color:#ff5f95;
    font-size:42px;
    font-family:'Baloo 2',cursive;
    line-height:1.5;
    min-height:120px;
}

.buttons{
    margin-top:30px;
}

button{
    border:none;
    border-radius:50px;
    padding:18px 45px;
    font-size:28px;
    font-family:'Baloo 2',cursive;
    font-weight:700;
    cursor:pointer;
    transition:0.2s;
}

#yes{
    background:#ff7aa8;
    color:white;
}

#no{
    background:#eeeeee;
    color:#666;
    position:fixed;
}

.hearts{
    position:fixed;
    inset:0;
    pointer-events:none;
}

.heart{
    position:absolute;
    animation:fly 4s linear forwards;
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

    <img src="conmeo1.jpg" id="cat">

    <div id="start">
        ✨ Click vào đây để khám phá option nhé sốp! ✨
    </div>

    <h1 id="text"></h1>

    <div class="buttons" id="buttons" style="display:none;">
        <button id="yes">💗 Kó</button>
        <button id="no">🙈 Hok</button>
    </div>

</div>

<div class="hearts" id="hearts"></div>

<script>

const message = "💕 Đi hẹn hò hok mom? 💕";

document.getElementById("start").onclick = function(){

    this.style.display = "none";

    let i = 0;

    function type(){

        if(i < message.length){
            document.getElementById("text").innerHTML += message.charAt(i);
            i++;
            setTimeout(type,100);
        }
        else{
            document.getElementById("buttons").style.display = "block";
        }
    }

    type();
};

const noBtn = document.getElementById("no");
const yesBtn = document.getElementById("yes");

let noScale = 1;
let yesScale = 1;

document.addEventListener("mousemove",function(e){

    if(
        document.getElementById("buttons").style.display
        !== "block"
    ){
        return;
    }

    const rect = noBtn.getBoundingClientRect();

    const x = rect.left + rect.width/2;
    const y = rect.top + rect.height/2;

    const distance = Math.sqrt(
        (e.clientX-x)*(e.clientX-x) +
        (e.clientY-y)*(e.clientY-y)
    );

    if(distance < 180){

        let newX = e.clientX + 50;
        let newY = e.clientY + 20;

        if(newX > window.innerWidth-120){
            newX = e.clientX - 150;
        }

        if(newY > window.innerHeight-60){
            newY = e.clientY - 60;
        }

        noBtn.style.left = newX + "px";
        noBtn.style.top = newY + "px";

        noScale -= 0.05;

        if(noScale < 0.3){
            noScale = 0.3;
        }

        noBtn.style.transform =
            `scale(${noScale})`;

        yesScale += 0.05;

        yesBtn.style.transform =
            `scale(${yesScale})`;
    }
});

yesBtn.onclick = function(){

    document.querySelector(".card").innerHTML = `
        <img src="anhconmeo.jpg"
             style="width:280px;">

        <h1>
            Yaaayyy 🥺💗<br>
            Biết ngay là chọn Kó mà,<br>
            mê tôi rồi chứ gì! 😘💕
        </h1>
    `;

    setInterval(()=>{

        const heart =
            document.createElement("div");

        heart.className = "heart";
        heart.innerHTML = "💗";

        heart.style.left =
            Math.random()*100 + "%";

        heart.style.bottom = "-30px";

        heart.style.fontSize =
            (20 + Math.random()*30) + "px";

        document.getElementById("hearts")
            .appendChild(heart);

        setTimeout(()=>{
            heart.remove();
        },4000);

    },250);
};

</script>

</body>
</html>
