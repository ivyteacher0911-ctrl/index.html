<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Baloo+2:wght@400;700&display=swap" rel="stylesheet">

<title>Đi hẹn hò hok mom?</title>

<style>

body{
    margin:0;
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    background:linear-gradient(135deg,#ffe0ec,#fff5f8,#ffd6e7);
    overflow:hidden;
    font-family:'Baloo 2',cursive;
}

.card{
    text-align:center;
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
    font-size:28px;
    color:#ff5d95;
    cursor:pointer;
    animation:blink 1s infinite;
}

@keyframes blink{
    50%{
        opacity:.5;
    }
}

h1{
    color:#ff5d95;
    font-family:'Pacifico';
    font-size:50px;
    min-height:100px;
}

.buttons{
    margin-top:20px;
}

button{
    border:none;
    border-radius:50px;
    padding:18px 45px;
    font-size:30px;
    cursor:pointer;
    font-family:'Baloo 2';
    transition:.2s;
}

#yes{
    background:#ff77a8;
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

    <img src="cat.png" id="cat">

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

document.getElementById("start").onclick=function(){

    this.style.display="none";

    let i=0;

    function type(){

        if(i<message.length){
            document.getElementById("text").innerHTML+=message.charAt(i);
            i++;
            setTimeout(type,100);
        }
        else{
            document.getElementById("buttons").style.display="block";
        }
    }

    type();
};

const noBtn=document.getElementById("no");
const yesBtn=document.getElementById("yes");

let scale=1;

document.addEventListener("mousemove",function(e){

    const rect=noBtn.getBoundingClientRect();

    const x=rect.left+rect.width/2;
    const y=rect.top+rect.height/2;

    const distance=Math.sqrt(
        (e.clientX-x)**2+
        (e.clientY-y)**2
    );

    if(distance<170){

        let newX=e.clientX+50;
        let newY=e.clientY+20;

        if(newX>window.innerWidth-100){
            newX=e.clientX-130;
        }

        if(newY>window.innerHeight-50){
            newY=e.clientY-50;
        }

        noBtn.style.left=newX+"px";
        noBtn.style.top=newY+"px";

        scale-=0.05;

        if(scale<0.3){
            scale=0.3;
        }

        noBtn.style.transform=
            `scale(${scale})`;

        let yesScale=
            Number(
                yesBtn.dataset.scale || 1
            );

        yesScale+=0.05;

        yesBtn.dataset.scale=yesScale;

        yesBtn.style.transform=
            `scale(${yesScale})`;
    }
});

yesBtn.onclick=function(){

    document.querySelector(".card").innerHTML=`

        <img src="cat.png" width="280">

        <h1>
        Yaaaayyy 🥺💗<br>
        Em biết mom sẽ chọn Kó màaaa!!!
        </h1>

    `;

    setInterval(()=>{

        const heart=document.createElement("div");

        heart.className="heart";
        heart.innerHTML="💗";

        heart.style.left=
            Math.random()*100+"%";

        heart.style.bottom="-30px";

        heart.style.fontSize=
            (20+Math.random()*30)+"px";

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
