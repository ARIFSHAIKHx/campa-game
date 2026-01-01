<!DOCTYPE html>
<html lang="mr">
<head>
<meta charset="UTF-8">
<title>Hidden Number Elimination Game</title>

<style>
body{
    margin:0;
    font-family: 'Poppins', sans-serif;
    background: radial-gradient(circle at top,#1e3c72,#2a5298);
    color:white;
    text-align:center;
}

h1{
    margin-top:20px;
    font-size:36px;
    text-shadow:0 0 10px #00eaff;
}

.container{
    width:95%;
    max-width:1200px;
    margin:auto;
}

.setup, .game{
    background:rgba(255,255,255,0.1);
    padding:20px;
    border-radius:15px;
    margin-top:20px;
    box-shadow:0 0 20px rgba(0,0,0,0.4);
}

input, button{
    padding:10px;
    border-radius:8px;
    border:none;
    outline:none;
    font-size:16px;
}

button{
    background:linear-gradient(45deg,#00eaff,#00ffa2);
    cursor:pointer;
    transition:0.3s;
}
button:hover{
    transform:scale(1.05);
    box-shadow:0 0 10px #00eaff;
}

.players{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:10px;
    margin-top:15px;
}

.player-card{
    background:rgba(0,0,0,0.4);
    padding:10px 15px;
    border-radius:10px;
    min-width:140px;
    transition:0.3s;
}
.player-card.eliminated{
    opacity:0.3;
    text-decoration:line-through;
}

.number-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(60px,1fr));
    gap:10px;
    margin-top:20px;
}

.num-box{
    background:linear-gradient(145deg,#ffffff,#ccefff);
    color:#000;
    font-size:20px;
    font-weight:bold;
    padding:15px;
    border-radius:12px;
    cursor:pointer;
    box-shadow:0 5px 15px rgba(0,0,0,0.3);
    transition:0.25s;
}
.num-box:hover{
    transform:translateY(-6px) scale(1.05);
    box-shadow:0 10px 25px rgba(0,0,0,0.5);
}

.log{
    margin-top:20px;
    background:rgba(0,0,0,0.4);
    padding:15px;
    border-radius:10px;
    min-height:60px;
}
</style>
</head>

<body>

<h1>🎯 Hidden Number Elimination Game</h1>

<div class="container">

<div class="setup">
    <h2>Game Setup</h2>
    <input id="playerName" placeholder="Player नाव टाका">
    <button onclick="addPlayer()">Add Player</button>
    <br><br>
    Number Range:
    <input id="startRange" type="number" value="1" style="width:80px;">
    to
    <input id="endRange" type="number" value="20" style="width:80px;">
    <br><br>
    <button onclick="startGame()">Start Game</button>

    <div class="players" id="playerList"></div>
</div>

<div class="game" style="display:none;">
    <h2 id="turnInfo"></h2>
    <div class="number-grid" id="numberGrid"></div>
    <div class="log" id="log"></div>
</div>

</div>

<script>
let players=[];
let currentPlayerIndex=0;
let rangeStart=1, rangeEnd=20;

const marathiNumbers={
1:"एक",2:"दोन",3:"तीन",4:"चार",5:"पाच",
6:"सहा",7:"सात",8:"आठ",9:"नऊ",10:"दहा",
11:"अकरा",12:"बारा",13:"तेरा",14:"चौदा",15:"पंधरा",
16:"सोळा",17:"सतरा",18:"अठरा",19:"एकोणीस",20:"वीस"
};

function speak(text){
    let msg=new SpeechSynthesisUtterance(text);
    msg.lang="mr-IN";
    speechSynthesis.speak(msg);
}

function addPlayer(){
    let name=document.getElementById("playerName").value.trim();
    if(!name) return;
    players.push({name,hidden:null,alive:true});
    document.getElementById("playerName").value="";
    renderPlayers();
}

function renderPlayers(){
    let div=document.getElementById("playerList");
    div.innerHTML="";
    players.forEach(p=>{
        let d=document.createElement("div");
        d.className="player-card"+(p.alive?"":" eliminated");
        d.innerText=p.name+(p.hidden?"":" (hidden?)");
        div.appendChild(d);
    });
}

function startGame(){
    if(players.length<2){
        alert("कमीत कमी 2 players हवेत");
        return;
    }
    rangeStart=+document.getElementById("startRange").value;
    rangeEnd=+document.getElementById("endRange").value;

    players.forEach(p=>{
        p.hidden=Math.floor(Math.random()*(rangeEnd-rangeStart+1))+rangeStart;
    });

    document.querySelector(".setup").style.display="none";
    document.querySelector(".game").style.display="block";

    createGrid();
    updateTurn();
}

function createGrid(){
    let grid=document.getElementById("numberGrid");
    grid.innerHTML="";
    for(let i=rangeStart;i<=rangeEnd;i++){
        let box=document.createElement("div");
        box.className="num-box";
        box.innerText=i;
        box.onclick=()=>numberClicked(i);
        grid.appendChild(box);
    }
}

function updateTurn(){
    let alivePlayers=players.filter(p=>p.alive);
    if(alivePlayers.length===1){
        document.getElementById("turnInfo").innerText=
            "🏆 Winner: "+alivePlayers[0].name;
        speak("विजेता आहे "+alivePlayers[0].name);
        return;
    }

    while(!players[currentPlayerIndex].alive){
        currentPlayerIndex=(currentPlayerIndex+1)%players.length;
    }

    document.getElementById("turnInfo").innerText=
        "👉 "+players[currentPlayerIndex].name+" ची Turn";
}

function numberClicked(num){
    let current=players[currentPlayerIndex];
    speak(marathiNumbers[num] || num+"");

    let eliminated=[];
    players.forEach(p=>{
        if(p.alive && p.hidden===num){
            p.alive=false;
            eliminated.push(p.name);
        }
    });

    let log=document.getElementById("log");
    if(eliminated.length>0){
        log.innerHTML="❌ Eliminate: "+eliminated.join(", ");
        speak("आऊट झाले "+eliminated.join(" "));
    }else{
        log.innerHTML="✅ कोणाचाही नंबर match नाही";
    }

    renderPlayers();
    currentPlayerIndex=(currentPlayerIndex+1)%players.length;
    updateTurn();
}
</script>

</body>
</html>
>
