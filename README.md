<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Princess Priyanjoli 💖</title>
<style>
body {
  font-family: "Poppins", sans-serif;
  background: linear-gradient(to bottom right, #f9d9f9, #d9b3ff);
  color: #5a2d82;
  text-align: center;
  padding: 30px;
  overflow-x: hidden;
  position: relative;
}
h1 { color:#ff69b4; text-shadow:1px 1px 3px #fff; }
.hidden { display:none; }
#loginBox { margin-top:120px; }
#password { padding:10px; border:2px solid #ff8fd8; border-radius:10px; font-size:1em; }
button { padding:10px 20px; background:#ff69b4; border:none; color:white; border-radius:10px; font-size:1em; margin-left:10px; }
.task { background: rgba(255,255,255,0.7); margin:15px auto; padding:15px; width:85%; border-radius:15px; display:flex; justify-content:space-between; align-items:center; font-size:1.1em; transition: transform 0.2s;}
.task:active { transform: scale(1.02);}
input[type="checkbox"] { width:25px; height:25px; accent-color:#ff8fd8; }
.heart { display:none; color:#ff69b4; font-size:1.3em; }
footer { margin-top:30px; font-size:1em; color:#7a3eb1; }
.floating-heart { position: fixed; z-index:9999; font-size:20px; pointer-events:none; animation: floatUp 6s linear forwards;}
@keyframes floatUp { 0% { transform: translateY(-50px); opacity:1; } 100% { transform: translateY(110vh) rotate(360deg); opacity:0; } }
#romanticLine { font-size:1.2em; color:#ff4db8; margin-bottom:20px; }
</style>
</head>
<body>

<div id="loginBox">
  <h2>🔒 Enter Secret Password</h2>
  <input type="password" id="password" placeholder="Enter Password">
  <button id="unlockBtn">Unlock 💞</button>
  <p id="error" style="color:red;"></p>
</div>

<div id="mainContent" class="hidden">
  <div id="romanticLine"></div>
  <h1 id="greeting">Welcome Princess Priyanjoli 💖</h1>
  <p>Your daily love checklist is waiting </p>

  <div class="task"><span>💧 Drink 9 Glasses of Water</span><input type="checkbox" id="task1"><span class="heart">💖</span></div>
  <div class="task"><span>🍳 Breakfast</span><input type="checkbox" id="task2"><span class="heart">💖</span></div>
  <div class="task"><span>🍱 Lunch</span><input type="checkbox" id="task3"><span class="heart">💖</span></div>
  <div class="task"><span>🍲 Dinner</span><input type="checkbox" id="task4"><span class="heart">💖</span></div>
  <div class="task"><span>🌞 Good Morning Kiss</span><input type="checkbox" id="task5"><span class="heart">💖</span></div>
  <div class="task"><span>🌤️ Good Afternoon Kiss</span><input type="checkbox" id="task6"><span class="heart">💖</span></div>
  <div class="task"><span>🌙 Good Night Kiss</span><input type="checkbox" id="task7"><span class="heart">💖</span></div>
  <div class="task"><span>🧁 Cuteness Tax</span><input type="checkbox" id="task8"><span class="heart">💖</span></div>
  <div class="task"><span>😊 Smile for Me</span><input type="checkbox" id="task9"><span class="heart">💖</span></div>
  <div class="task"><span>👗 Wash Clothes Before Sunset</span><input type="checkbox" id="task10"><span class="heart">💖</span></div>

  <footer>Made with 💞 by Your One & Only 😘</footer>
</div>

<script>
const secret = "myprincess123";
const unlockBtn = document.getElementById("unlockBtn");
const passwordInput = document.getElementById("password");
const loginBox = document.getElementById("loginBox");
const mainContent = document.getElementById("mainContent");
const errorMsg = document.getElementById("error");
const romanticLine = document.getElementById("romanticLine");

// Romantic lines array
const lines = [
  "Every time I see you, my heart skips a beat 💖",
  "You are my sunshine on a cloudy day ☀️",
  "My favorite thought is you 😊",
  "Love grows stronger each time I think of you 🌸",
  "You make my world magical ✨"
];

// Unlock site
unlockBtn.addEventListener("click", ()=>{
  if(passwordInput.value===secret){
    loginBox.classList.add("hidden");
    mainContent.classList.remove("hidden");
    showRomanticLine();
    loadTasks();
    addCheckboxListeners();
    startHeartRain(); // start continuous heart rain
  } else {
    errorMsg.textContent = "Wrong password 💔";
  }
});

// Show random romantic line
function showRomanticLine(){
  const index = Math.floor(Math.random()*lines.length);
  romanticLine.textContent = lines[index];
}

// Save/load tasks
const checkboxes = document.querySelectorAll('input[type="checkbox"]');
function saveTasks(){
  const data = {};
  checkboxes.forEach(box => data[box.id] = box.checked);
  localStorage.setItem("priyanjoli_tasks", JSON.stringify(data));
}
function loadTasks(){
  const saved = JSON.parse(localStorage.getItem("priyanjoli_tasks")||"{}");
  checkboxes.forEach(box=>{
    if(saved[box.id]){
      box.checked = true;
      box.nextElementSibling.style.display="inline";
    }
  });
}

// Checkbox listeners & completion check
function addCheckboxListeners(){
  checkboxes.forEach(box=>{
    box.addEventListener("change",()=>{
      const heart = box.nextElementSibling;
      heart.style.display = box.checked ? "inline" : "none";
      saveTasks();
      checkCompletion();
    });
  });
}

// Animation when all tasks done
function checkCompletion(){
  const allDone = Array.from(checkboxes).every(box=>box.checked);
  if(allDone){
    for(let i=0;i<50;i++){
      createFloatingHeart();
    }
  }
}

// Continuous heart rain
function startHeartRain(){
  setInterval(createFloatingHeart, 400); // create new heart every 0.4s
}

function createFloatingHeart(){
  const heart = document.createElement("div");
  heart.textContent = "💖";
  heart.className = "floating-heart";
  heart.style.left = Math.random()*window.innerWidth + "px";
  heart.style.fontSize = Math.random()*30+15+"px";
  document.body.appendChild(heart);
  setTimeout(()=>heart.remove(),6000);
}
</script>

</body>
</html>
