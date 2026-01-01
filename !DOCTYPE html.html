<!DOCTYPE html>
<html lang="mr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Marathi Number Game 🎮</title>
    <style>
        :root { --main: #4a4e69; --out: #e63946; --miss: #2a9d8f; }
        body { font-family: sans-serif; background: #f8f9fa; display: flex; flex-direction: column; align-items: center; padding: 20px; }
        .card { background: white; padding: 20px; border-radius: 15px; box-shadow: 0 5px 20px rgba(0,0,0,0.1); width: 100%; max-width: 400px; text-align: center; }
        input { width: 85%; padding: 12px; margin: 5px; border: 2px solid #ddd; border-radius: 8px; font-size: 16px; }
        .btn-add { background: var(--main); color: white; border: none; padding: 12px; border-radius: 8px; width: 90%; cursor: pointer; font-weight: bold; }
        .grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 8px; margin: 20px 0; }
        .box { height: 55px; background: white; border: 2px solid var(--main); border-radius: 10px; display: flex; align-items: center; justify-content: center; font-size: 18px; font-weight: bold; cursor: pointer; color: var(--main); }
        .box.used { background: #d1d1d1; border-color: #888; color: #777; pointer-events: none; }
        #msg { padding: 12px; border-radius: 10px; font-weight: bold; margin-bottom: 15px; display: none; }
        .p-list { text-align: left; background: #f1f1f1; padding: 10px; border-radius: 8px; font-size: 14px; }
    </style>
</head>
<body>

<div class="card">
    <h2>१-२० लपाछपी 🎯</h2>
    <div style="margin-bottom:15px;">
        <input type="text" id="name" placeholder="प्लेयरचे नाव">
        <input type="password" id="num" placeholder="गुपित नंबर (1-20)">
        <button class="btn-add" onclick="register()">Add Player</button>
    </div>
    <div id="msg"></div>
    <div class="grid" id="grid"></div>
    <div class="p-list" id="list">प्लेयर्स येणे बाकी...</div>
</div>

<script>
    let players = [];
    const marathiNumbers = {1:"एक", 2:"दोन", 3:"तीन", 4:"चार", 5:"पाच", 6:"सहा", 7:"सात", 8:"आठ", 9:"नऊ", 10:"दहा", 11:"अकरा", 12:"बारा", 13:"तेरा", 14:"चौदा", 15:"पंधरा", 16:"सोळा", 17:"सतरा", 18:"अठरा", 19:"एकोणीस", 20:"वीस"};

    function speak(text) {
        let u = new SpeechSynthesisUtterance(text);
        u.lang = 'mr-IN';
        window.speechSynthesis.speak(u);
    }

    function register() {
        let n = document.getElementById('name').value;
        let v = parseInt(document.getElementById('num').value);
        if(!n || v < 1 || v > 20) return alert("योग्य माहिती भरा!");
        players.push({ name: n, secret: v, alive: true });
        document.getElementById('name').value = ''; document.getElementById('num').value = '';
        updateList();
        alert(n + " ऍड झाला!");
    }

    function play(n, el) {
        if(players.length === 0) return alert("आधी प्लेयर ऍड करा!");
        speak(marathiNumbers[n]);
        let msg = document.getElementById('msg');
        let found = false;
        players.forEach(p => {
            if(p.alive && p.secret === n) {
                p.alive = false; found = true;
                msg.style.display = "block"; msg.style.background = "#e63946"; msg.style.color = "white";
                msg.innerHTML = p.name + " आउट झाला! 💀";
                speak(p.name + " आउट झाला");
            }
        });
        if(!found) {
            msg.style.display = "block"; msg.style.background = "#2a9d8f"; msg.style.color = "white";
            msg.innerHTML = "Miss Number! ✅";
            speak("मिस नंबर");
        }
        el.classList.add('used');
        updateList();
    }

    function updateList() {
        document.getElementById('list').innerHTML = players.map(p => `<div>${p.alive ? '👤' : '❌'} ${p.name}</div>`).join('');
    }

    for (let i = 1; i <= 20; i++) {
        let b = document.createElement('div'); b.className = 'box'; b.innerText = i;
        b.onclick = () => play(i, b); document.getElementById('grid').appendChild(b);
    }
</script>
</body>
</html>
