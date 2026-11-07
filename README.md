html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>Ninja World 3D</title>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
  user-select:none;
  -webkit-user-select:none;
}

html,body{
  width:100%;
  height:100%;
  overflow:hidden;
  background:#07111c;
  font-family:Arial,sans-serif;
}

#game{
  position:fixed;
  inset:0;
  overflow:hidden;
}

#scene{
  position:absolute;
  inset:0;
}

canvas{
  display:block;
  width:100%;
  height:100%;
  touch-action:none;
}

.hidden{
  display:none!important;
}

/* HUD */

#hud{
  position:absolute;
  z-index:20;
  top:8px;
  left:7px;
  right:7px;
  display:flex;
  justify-content:space-between;
  gap:5px;
  pointer-events:none;
}

.stat{
  min-width:64px;
  padding:6px;
  border-radius:13px;
  text-align:center;
  color:white;
  font-size:10px;
  font-weight:900;
  background:rgba(4,12,23,.88);
  border:1px solid rgba(255,255,255,.15);
  box-shadow:0 4px 14px rgba(0,0,0,.4);
}

.stat span{
  color:#ffd84a;
  font-size:13px;
}

/* ABILITIES */

#abilities{
  position:absolute;
  z-index:25;
  top:72px;
  left:50%;
  transform:translateX(-50%);
  display:flex;
  gap:5px;
  pointer-events:none;
}

.ability{
  width:67px;
  padding:5px;
  border-radius:10px;
  text-align:center;
  color:white;
  font-size:18px;
  background:rgba(3,10,20,.82);
  border:1px solid rgba(255,255,255,.16);
}

.ability b{
  display:block;
  font-size:8px;
}

.ability.active{
  box-shadow:0 0 18px currentColor;
}

/* SCREENS */

.screen{
  position:absolute;
  inset:0;
  z-index:80;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  gap:12px;
  padding:18px;
  color:white;
  text-align:center;
  background:
    radial-gradient(circle at 50% 18%,rgba(255,45,70,.22),transparent 32%),
    linear-gradient(155deg,#06111e,#111e30 55%,#180c15);
}

.logo{
  font-size:42px;
  font-weight:1000;
  letter-spacing:2px;
  text-shadow:
    0 4px 0 #111,
    0 0 15px #ff3150,
    0 0 35px rgba(255,30,60,.5);
}

.logo span{
  color:#ff3654;
}

.subtitle{
  color:#ffd74c;
  font-size:10px;
  letter-spacing:4px;
  font-weight:900;
}

.screen p{
  color:#d7e3e9;
  line-height:1.65;
}

.small{
  max-width:330px;
  color:#9aacb7!important;
  font-size:10px;
}

button{
  min-width:175px;
  padding:13px 20px;
  border:0;
  border-radius:14px;
  color:white;
  font-size:14px;
  font-weight:900;
  background:linear-gradient(#ff4562,#d91d40);
  box-shadow:
    0 5px 0 #82162b,
    0 8px 20px rgba(0,0,0,.35);
  touch-action:manipulation;
}

button:active{
  transform:translateY(4px);
  box-shadow:0 1px 0 #82162b;
}

/* CONTROLS */

#controls{
  position:absolute;
  z-index:30;
  left:9px;
  right:9px;
  bottom:11px;
  display:none;
  justify-content:space-between;
  pointer-events:none;
}

.controlGroup{
  display:flex;
  gap:7px;
}

.control{
  width:64px;
  height:64px;
  min-width:64px;
  padding:0;
  border-radius:18px;
  background:rgba(5,15,27,.82);
  border:1px solid rgba(255,255,255,.18);
  box-shadow:
    0 5px 15px rgba(0,0,0,.4),
    inset 0 1px rgba(255,255,255,.1);
  font-size:24px;
  pointer-events:auto;
}

.control.jump{
  background:rgba(20,100,145,.82);
}

.control.slide{
  background:rgba(135,42,55,.82);
}

/* MESSAGE */

#message{
  position:absolute;
  z-index:45;
  top:20%;
  left:0;
  right:0;
  text-align:center;
  color:white;
  font-size:25px;
  font-weight:1000;
  text-shadow:0 3px 6px black;
  pointer-events:none;
}

#combo{
  position:absolute;
  z-index:45;
  top:27%;
  left:0;
  right:0;
  text-align:center;
  color:#ffd84a;
  font-size:20px;
  font-weight:1000;
  opacity:0;
  pointer-events:none;
}

/* SHOP */

.shopCard{
  width:320px;
  max-width:94vw;
  padding:17px;
  border-radius:20px;
  background:rgba(7,16,28,.95);
  border:1px solid rgba(255,255,255,.15);
  box-shadow:0 0 35px rgba(0,0,0,.4);
}

.skinPreview{
  width:125px;
  height:125px;
  margin:auto;
  display:flex;
  align-items:center;
  justify-content:center;
  border-radius:50%;
  font-size:72px;
  background:radial-gradient(circle,#3d5065,#0c1724);
  box-shadow:0 0 30px rgba(255,255,255,.1);
}

.price{
  margin:9px;
  color:#ffd84a;
  font-size:17px;
  font-weight:900;
}

/* REWARD */

#rewardBox{
  width:310px;
  max-width:94vw;
  padding:20px;
  border-radius:22px;
  background:linear-gradient(145deg,#182c40,#091421);
  border:1px solid rgba(255,215,70,.55);
  box-shadow:0 0 40px rgba(255,180,30,.2);
}

.rewardIcon{
  margin:8px;
  font-size:60px;
}

.rewardText{
  color:#ffd84a;
  font-size:19px;
  font-weight:1000;
}

/* LOADING */

#loading{
  position:absolute;
  inset:0;
  z-index:200;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  gap:14px;
  color:white;
  background:#06101b;
}

.loader{
  width:52px;
  height:52px;
  border:4px solid rgba(255,255,255,.1);
  border-top-color:#ff3c59;
  border-radius:50%;
  animation:spin .8s linear infinite;
}

@keyframes spin{
  to{transform:rotate(360deg)}
}
</style>
</head>

<body>

<div id="game">

<div id="loading">
  <div class="loader"></div>
  <b>جاري تجهيز عالم النينجا...</b>
  <small>NO FOG • SUBWAY RUNNER</small>
</div>

<div id="scene"></div>

<div id="hud">
  <div class="stat">🏆<br><span id="score">0</span></div>
  <div class="stat">🪙<br><span id="coins">0</span></div>
  <div class="stat">❤️<br><span id="lives">3</span></div>
  <div class="stat">⚡<br><span id="speed">1.0x</span></div>
</div>

<div id="abilities">
  <div class="ability" id="shieldUI">🛡️<b id="shieldText">درع</b></div>
  <div class="ability" id="magnetUI">🧲<b id="magnetText">مغناطيس</b></div>
  <div class="ability" id="boostUI">🚀<b id="boostText">سرعة</b></div>
</div>

<div id="message"></div>
<div id="combo"></div>

<!-- MENU -->

<div id="menu" class="screen">

  <div class="logo">NINJA <span>WORLD</span></div>

  <div class="subtitle">SUBWAY RUNNER 3D</div>

  <p>
    🥷 اهرب بأقصى سرعة<br>
    🛣️ بدّل بين 3 مسالك<br>
    🪙 اجمع العملات والقدرات
  </p>

  <button id="start">▶️ ابدأ الجري</button>
  <button id="shop">🥷 متجر الأزياء</button>
  <button id="soundButton">🔊 الصوت: ON</button>

  <p class="small">
    اسحب يمين / يسار للتحرك<br>
    اسحب لفوق للقفز • اسحب لتحت للانبطاح
  </p>

</div>

<!-- SHOP -->

<div id="shopPanel" class="screen hidden">

  <h1>🥷 متجر النينجا</h1>

  <div class="shopCard">

    <div id="skinPreview" class="skinPreview">🥷</div>

    <h2 id="skinName">Shadow</h2>

    <p id="skinDescription">
      نينجا سريع ومتوازن.
    </p>

    <div class="price">
      🪙 <span id="shopCoins">0</span>
    </div>

    <button id="nextSkin">➡️ الزي التالي</button>
    <button id="buySkin">🪙 شراء</button>
    <button id="closeShop">رجوع</button>

  </div>

</div>

<!-- REWARD -->

<div id="reward" class="screen hidden">

  <div id="rewardBox">

    <h1>🎁 هدية الجولة!</h1>

    <div id="rewardIcon" class="rewardIcon">🎁</div>

    <div id="rewardText" class="rewardText">
      +50 🪙
    </div>

    <p>الهدية تحفّظت في حسابك 💾</p>

    <button id="rewardContinue">🔥 مواصلة</button>

  </div>

</div>

<!-- GAME OVER -->

<div id="gameover" class="screen hidden">

  <h1>💥 انتهى الجري!</h1>

  <p>🏆 النتيجة: <b id="finalScore">0</b></p>
  <p>🪙 ربح الجولة: <b id="finalCoins">0</b></p>
  <p>👑 أفضل نتيجة: <b id="bestScore">0</b></p>

  <button id="restart">🔥 جولة جديدة</button>
  <button id="home">🏠 القائمة</button>

</div>

<!-- CONTROLS -->

<div id="controls">

  <div class="controlGroup">
    <button class="control" id="left">◀</button>
    <button class="control" id="right">▶</button>
  </div>

  <div class="controlGroup">
    <button class="control slide" id="slide">↘</button>
    <button class="control jump" id="jump">⬆</button>
  </div>

</div>

</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/0.160.0/three.min.js"></script>

<script>
"use strict";

/* =========================================================
   NINJA WORLD 3D
   COMPLETE VERSION
   NO FOG
========================================================= */

const $=id=>document.getElementById(id);

let scene,camera,renderer,clock;
let player;
let playerParts={};

let obstacles=[];
let coinObjects=[];
let powerObjects=[];
let scenery=[];
let particles=[];

let running=false;
let gameEnded=false;

let score=0;
let wallet=0;
let runCoins=0;
let lives=3;
let bestScore=0;

let lane=1;
let targetX=0;

let jumpY=0;
let velocityY=0;
let jumping=false;

let sliding=false;
let slideTimer=0;

let speed=18;
let baseSpeed=18;

let distance=0;

let obstacleTimer=0;
let coinTimer=0;
let powerTimer=0;

let shieldTime=0;
let magnetTime=0;
let boostTime=0;

let damageCooldown=0;

let combo=0;
let comboTimer=0;

let skinIndex=0;

let soundEnabled=true;
let audioContext=null;

let touchStartX=0;
let touchStartY=0;

const lanes=[-2.45,0,2.45];

const SAVE_KEY="NINJA_WORLD_COMPLETE_V1";

const skins=[
  {
    name:"Shadow",
    description:"نينجا أسود سريع ومتوازن.",
    color:0x151a22,
    cloth:0xb9213e,
    eye:0x55eaff,
    icon:"🥷",
    price:0
  },
  {
    name:"Red Storm",
    description:"درع أحمر مع وشاح هجومي.",
    color:0x45151c,
    cloth:0xff3b30,
    eye:0xffd84a,
    icon:"🔥",
    price:150
  },
  {
    name:"Cyber",
    description:"نينجا مستقبلي بإضاءة نيون.",
    color:0x162f42,
    cloth:0x00d9ff,
    eye:0xffffff,
    icon:"🤖",
    price:300
  },
  {
    name:"Samurai",
    description:"درع ساموراي وسيف ثقيل.",
    color:0x272b31,
    cloth:0xc9a84a,
    eye:0xff4949,
    icon:"⚔️",
    price:500
  },
  {
    name:"Phantom",
    description:"نينجا غامض بتأثير بنفسجي.",
    color:0x20152e,
    cloth:0x9d4edd,
    eye:0xe9c2ff,
    icon:"👻",
    price:800
  },
  {
    name:"Golden",
    description:"الزي الأسطوري الذهبي.",
    color:0x6e5013,
    cloth:0xffd84a,
    eye:0xffffff,
    icon:"👑",
    price:1200
  }
];

let owned=[true,false,false,false,false,false];

/* =========================================================
 SAVE
========================================================= */

function saveGame(){
  try{
    localStorage.setItem(
      SAVE_KEY,
      JSON.stringify({
        wallet,
        bestScore,
        skinIndex,
        owned,
        soundEnabled
      })
    );
  }catch(e){}
}

function loadGame(){
  try{
    const raw=localStorage.getItem(SAVE_KEY);
    if(!raw)return;

    const d=JSON.parse(raw);

    wallet=Math.max(0,Number(d.wallet)||0);
    bestScore=Math.max(0,Number(d.bestScore)||0);
    skinIndex=Math.max(0,Math.min(5,Number(d.skinIndex)||0));

    if(Array.isArray(d.owned)){
      owned=d.owned.slice(0,6);
      while(owned.length<6)owned.push(false);
      owned[0]=true;
    }

    soundEnabled=d.soundEnabled!==false;

  }catch(e){}
}

/* =========================================================
 MATERIALS
========================================================= */

function mat(
  color,
  rough=.7,
  metal=0,
  emissive=0,
  power=0
){
  return new THREE.MeshStandardMaterial({
    color,
    roughness:rough,
    metalness:metal,
    emissive,
    emissiveIntensity:power
  });
}

function make(
  geometry,
  material,
  x=0,
  y=0,
  z=0
){
  const m=new THREE.Mesh(geometry,material);
  m.position.set(x,y,z);
  m.castShadow=true;
  m.receiveShadow=true;
  return m;
}

/* =========================================================
 AUDIO
========================================================= */

function initAudio(){
  if(!soundEnabled)return;

  try{
    if(!audioContext){
      audioContext=new(
        window.AudioContext||
        window.webkitAudioContext
      )();
    }

    if(audioContext.state==="suspended"){
      audioContext.resume();
    }
  }catch(e){}
}

function beep(
  frequency,
  duration=.1,
  type="sine",
  volume=.035
){
  if(!soundEnabled||!audioContext)return;

  try{
    const osc=audioContext.createOscillator();
    const gain=audioContext.createGain();

    osc.type=type;
    osc.frequency.value=frequency;

    gain.gain.setValueAtTime(
      volume,
      audioContext.currentTime
    );

    gain.gain.exponentialRampToValueAtTime(
      .001,
      audioContext.currentTime+duration
    );

    osc.connect(gain);
    gain.connect(audioContext.destination);

    osc.start();
    osc.stop(audioContext.currentTime+duration);

  }catch(e){}
}

/* =========================================================
 INIT
========================================================= */

function init(){

  loadGame();

  if(!window.THREE){
    $("loading").innerHTML=
      "<h2>❌ Three.js ما تحمّلش</h2>"+
      "<p>تأكد من الإنترنت ثم اعمل Refresh.</p>";
    return;
  }

  scene=new THREE.Scene();

  /* IMPORTANT:
     NO FOG
  */
  scene.background=new THREE.Color(0x081525);

  camera=new THREE.PerspectiveCamera(
    68,
    innerWidth/innerHeight,
    .1,
    600
  );

  camera.position.set(0,4.6,9);

  renderer=new THREE.WebGLRenderer({
    antialias:true,
    powerPreference:"high-performance"
  });

  renderer.setSize(
    innerWidth,
    innerHeight
  );

  renderer.setPixelRatio(
    Math.min(devicePixelRatio||1,1.25)
  );

  renderer.shadowMap.enabled=true;
  renderer.shadowMap.type=
    THREE.PCFSoftShadowMap;

  renderer.toneMapping=
    THREE.ACESFilmicToneMapping;

  renderer.toneMappingExposure=1.15;

  renderer.outputColorSpace=
    THREE.SRGBColorSpace;

  $("scene").appendChild(
    renderer.domElement
  );

  clock=new THREE.Clock();

  const hemi=new THREE.HemisphereLight(
    0x9edcff,
    0x162020,
    2.4
  );

  scene.add(hemi);

  const sun=new THREE.DirectionalLight(
    0xffe2b8,
    3
  );

  sun.position.set(-15,30,20);
  sun.castShadow=true;

  sun.shadow.mapSize.set(1024,1024);

  sun.shadow.camera.left=-30;
  sun.shadow.camera.right=30;
  sun.shadow.camera.top=30;
  sun.shadow.camera.bottom=-30;

  scene.add(sun);

  createWorld();
  createSky();
  createPlayer();

  bindControls();
  updateHUD();
  updateShop();

  window.addEventListener(
    "resize",
    resize
  );

  requestAnimationFrame(animate);

  setTimeout(()=>{
    $("loading").classList.add("hidden");
  },700);
}

/* =========================================================
 WORLD
========================================================= */

function createWorld(){

  const ground=make(
    new THREE.PlaneGeometry(180,600),
    mat(0x25352f,.98),
    0,-.25,-250
  );

  ground.rotation.x=-Math.PI/2;
  scene.add(ground);

  const road=make(
    new THREE.PlaneGeometry(8.2,600),
    mat(0x20252b,.92),
    0,0,-250
  );

  road.rotation.x=-Math.PI/2;
  scene.add(road);

  /* road edges */

  for(const x of[-4.35,4.35]){

    const edge=make(
      new THREE.BoxGeometry(.28,.15,600),
      mat(0x62676a,.8),
      x,.08,-250
    );

    scene.add(edge);
  }

  /* 3 lane separators */

  for(const x of[-1.225,1.225]){

    for(let i=0;i<80;i++){

      const line=make(
        new THREE.BoxGeometry(.055,.035,3.8),
        mat(0xf1e7bd,.65),
        x,.035,-i*7
      );

      scenery.push({
        object:line,
        type:"road"
      });

      scene.add(line);
    }
  }

  /* side city */

  for(let i=0;i<42;i++){

    createBuilding(-1,-15-i*14);
    createBuilding(1,-22-i*14);
  }

  for(let i=0;i<40;i++){

    createTree(-7,-12-i*10);
    createTree(7,-17-i*10);
  }

  for(let i=0;i<34;i++){

    createLamp(
      i%2?-5.3:5.3,
      -12-i*13
    );
  }
}

/* =========================================================
 BUILDINGS
========================================================= */

function createBuilding(side,z){

  const g=new THREE.Group();

  const width=3+Math.random()*2;
  const height=6+Math.random()*11;
  const depth=4+Math.random()*2;

  const colors=[
    0x414a53,
    0x555d66,
    0x374149,
    0x62564e
  ];

  const body=make(
    new THREE.BoxGeometry(
      width,height,depth
    ),
    mat(
      colors[
        Math.floor(Math.random()*colors.length)
      ],
      .9
    ),
    0,height/2,0
  );

  g.add(body);

  const roof=make(
    new THREE.BoxGeometry(
      width+.25,.35,depth+.25
    ),
    mat(0x25292d,.7),
    0,height+.15,0
  );

  g.add(roof);

  for(let y=1.7;y<height-1;y+=1.7){

    for(
      let x=-width/2+.55;
      x<width/2;
      x+=.9
    ){

      if(Math.random()<.22)continue;

      const lit=Math.random()>.35;

      const windowMat=mat(
        lit?0xffd76a:0x294150,
        .4,
        0,
        lit?0xff7c15:0,
        lit?1.3:0
      );

      g.add(
        make(
          new THREE.BoxGeometry(
            .43,.55,.035
          ),
          windowMat,
          x,y,depth/2+.03
        )
      );
    }
  }

  g.position.set(
    side*8.2,
    0,
    z
  );

  scene.add(g);

  scenery.push({
    object:g,
    type:"building"
  });
}

/* =========================================================
 TREES
========================================================= */

function createTree(x,z){

  const g=new THREE.Group();

  g.add(
    make(
      new THREE.CylinderGeometry(
        .18,.34,3,8
      ),
      mat(0x513522,.95),
      0,1.5,0
    )
  );

  for(let i=0;i<3;i++){

    const leaf=make(
      new THREE.SphereGeometry(
        1.3-i*.1,
        10,8
      ),
      mat(
        i%2?0x237047:0x155a38,
        .98
      ),
      0,
      3+i*.62,
      0
    );

    leaf.scale.set(1,.72,1);

    g.add(leaf);
  }

  g.position.set(x,0,z);

  scene.add(g);

  scenery.push({
    object:g,
    type:"tree"
  });
}

/* =========================================================
 LAMPS
========================================================= */

function createLamp(x,z){

  const g=new THREE.Group();

  g.add(
    make(
      new THREE.CylinderGeometry(
        .07,.12,4,8
      ),
      mat(0x20252a,.6,.5),
      0,2,0
    )
  );

  const armX=x>0?-.45:.45;

  g.add(
    make(
      new THREE.BoxGeometry(
        .8,.08,.08
      ),
      mat(0x20252a,.6,.5),
      armX,3.8,0
    )
  );

  g.add(
    make(
      new THREE.SphereGeometry(
        .18,10,10
      ),
      mat(
        0xffd85a,
        .3,
        0,
        0xff7300,
        2
      ),
      x>0?-.78:.78,
      3.72,
      0
    )
  );

  g.position.set(x,0,z);

  scene.add(g);

  scenery.push({
    object:g,
    type:"lamp"
  });
}

/* =========================================================
 SKY
========================================================= */

function createSky(){

  const moon=make(
    new THREE.SphereGeometry(
      5,24,24
    ),
    new THREE.MeshBasicMaterial({
      color:0xfff1c2
    }),
    -32,42,-180
  );

  scene.add(moon);

  const geo=new THREE.BufferGeometry();
  const positions=[];

  for(let i=0;i<500;i++){

    positions.push(
      (Math.random()-.5)*200,
      18+Math.random()*80,
      -30-Math.random()*350
    );
  }

  geo.setAttribute(
    "position",
    new THREE.Float32BufferAttribute(
      positions,3
    )
  );

  scene.add(
    new THREE.Points(
      geo,
      new THREE.PointsMaterial({
        color:0xffffff,
        size:.28
      })
    )
  );
}

/* =========================================================
 PLAYER
========================================================= */

function createPlayer(){

  if(player){
    scene.remove(player);
  }

  player=new THREE.Group();

  const s=skins[skinIndex];

  const bodyMat=mat(
    s.color,.5,.2
  );

  const clothMat=mat(
    s.cloth,.48,.2
  );

  const metalMat=mat(
    0x3b4148,.35,.85
  );

  const eyeMat=mat(
    s.eye,.25,.15,s.eye,2
  );

  /* root */

  const body=new THREE.Group();
  body.name="body";

  /* hips */

  const hips=make(
    new THREE.BoxGeometry(
      .68,.32,.48
    ),
    bodyMat,
    0,1.02,0
  );

  body.add(hips);
  playerParts.hips=hips;

  /* torso */

  const torso=make(
    new THREE.CapsuleGeometry(
      .43,.7,6,12
    ),
    bodyMat,
    0,1.48,0
  );

  body.add(torso);
  playerParts.torso=torso;

  /* chest armor */

  body.add(
    make(
      new THREE.BoxGeometry(
        .65,.45,.22
