<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Crunchtude</title>

<style>
body{margin:0;background:#0f0f0f;color:white;font-family:Arial}
header{background:#1a1a1a;padding:10px;font-size:18px}
.page{display:none;padding-bottom:70px}
.page.active{display:block}
video{width:100%;background:black}
.card{display:flex;gap:10px;margin:10px;background:#1c1c1c;padding:8px;border-radius:8px}
.card img{width:120px;border-radius:6px}
button{background:#333;border:none;color:white;padding:6px 10px;border-radius:6px}
nav{position:fixed;bottom:0;width:100%;background:#1a1a1a;display:flex;justify-content:space-around;padding:10px}
input{width:90%;margin:10px;padding:6px;background:#333;border:none;color:white}
</style>
</head>

<body>

<header>Crunchtude</header>

<!-- HOME -->
<div id="home" class="page active">
 <h3 style="margin-left:10px">Online Videos</h3>
 <div id="onlineList"></div>
</div>

<!-- DEVICE -->
<div id="device" class="page">
 <h3 style="margin-left:10px">
  Device Videos
  <button onclick="pickVideos()">📁 Pick</button>
 </h3>
 <div id="deviceList"></div>
</div>

<!-- PLAYER -->
<div id="player" class="page">
 <video id="video" controls></video>
</div>

<!-- PROFILE -->
<div id="profile" class="page">
 <input id="name" placeholder="Your name">
 <button onclick="saveName()">Save</button>
</div>

<nav>
 <button onclick="show('home')">Home</button>
 <button onclick="show('device')">Device</button>
 <button onclick="show('player')">Player</button>
 <button onclick="show('profile')">Profile</button>
</nav>

<input type="file" id="picker" accept="video/*" multiple style="display:none">

<script>
/* NAV */
function show(p){
 document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
 document.getElementById(p).classList.add('active');
}

/* ONLINE VIDEOS */
const online=[
 {t:"Big Buck Bunny",u:"https://www.w3schools.com/html/mov_bbb.mp4"},
 {t:"Bear Video",u:"https://www.w3schools.com/html/movie.mp4"}
];

const onlineList=document.getElementById("onlineList");
onlineList.innerHTML=online.map((v,i)=>`
 <div class="card" onclick="play('${v.u}')">
  <img src="https://i.imgur.com/9Q9ZQZy.png">
  <div>${v.t}</div>
 </div>
`).join("");

/* DEVICE VIDEOS */
const picker=document.getElementById("picker");
const deviceList=document.getElementById("deviceList");

function pickVideos(){picker.click();}

picker.onchange=()=>{
 deviceList.innerHTML="";
 [...picker.files].forEach(f=>{
  const url=URL.createObjectURL(f);
  deviceList.innerHTML+=`
   <div class="card" onclick="play('${url}')">
    <img src="https://i.imgur.com/9Q9ZQZy.png">
    <div>${f.name}</div>
   </div>
  `;
 });
};

/* PLAYER */
const video=document.getElementById("video");
function play(url){
 video.src=url;
 video.play();
 show("player");
}

/* PROFILE */
function saveName(){
 localStorage.setItem("name",name.value);
 alert("Saved");
}
name.value=localStorage.getItem("name")||"";
</script>

</body>
</html>
