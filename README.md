<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>मेरी आख़िरी बात ❤️</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{
  font-family: 'Poppins', Arial, sans-serif;
  background: radial-gradient(circle at top,#101a3a,#030611 70%);
  color:#fff;
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  user-select:none;
}
.container{
  width:96%;
  max-width:900px;
  min-height:75vh;
  background:rgba(255,255,255,0.04);
  border-radius:26px;
  padding:40px 28px;
  text-align:center;
  box-shadow:0 20px 60px rgba(0,0,0,0.6);
}
h1{font-size:38px;margin-bottom:14px}
.lead{opacity:.85;font-size:18px}
.btn{
  margin-top:30px;
  padding:14px 34px;
  background:#ff3b6b;
  color:#fff;
  border:0;
  border-radius:14px;
  font-size:18px;
  cursor:pointer;
}
.overlay{
  position:fixed;
  inset:0;
  background:rgba(0,0,0,.92);
  display:none;
  align-items:center;
  justify-content:center;
  z-index:99;
}
.overlay.open{display:flex}
.modal{
  background:#0b1220;
  padding:35px 30px;
  border-radius:24px;
  max-width:920px;
  width:96%;
  min-height:80vh;
  text-align:center;
  position:relative;
}
.close-btn{
  position:absolute;
  right:18px;
  top:14px;
  background:none;
  border:0;
  color:#fff;
  font-size:26px;
  cursor:pointer;
}

/* ✅ ONLY SCROLL FIX — NOTHING ELSE */
#page{
  font-size:20px;
  line-height:1.8;
  margin-top:30px;
  min-height:48vh;
  max-height:55vh;
  padding:0 16px;
  position:relative;
  overflow-y:auto;
  -webkit-overflow-scrolling:touch;
}

.nav{
  display:flex;
  justify-content:space-between;
  align-items:center;
  margin-top:20px;
}
.nav button{
  padding:10px 22px;
  border-radius:12px;
  border:0;
  background:#ff3b6b;
  color:#fff;
  font-size:16px;
}
.counter{opacity:.8;font-size:16px}
#lockScreen{display:none}
input{
  padding:12px 14px;
  border-radius:12px;
  border:0;
  font-size:18px;
  width:200px;
  text-align:center;
  margin-top:16px;
}

/* Background animation */
#page::before{
  content:"";
  position:absolute;
  inset:0;
  background:url('https://cdn-icons-png.flaticon.com/512/833/833472.png') repeat;
  background-size:60px;
  opacity:0.08;
  animation:heartbeatBg 6s infinite linear;
  pointer-events:none;
}
@keyframes heartbeatBg{
  from{background-position:0 0;}
  to{background-position:200px 200px;}
}

/* Shake + red glow (WRONG PASSWORD) */
.shake{
  animation: shakeAnim 0.4s ease;
  box-shadow:0 0 18px #ff1a1a;
}
@keyframes shakeAnim{
  0%{transform:translateX(0)}
  20%{transform:translateX(-8px)}
  40%{transform:translateX(8px)}
  60%{transform:translateX(-6px)}
  80%{transform:translateX(6px)}
  100%{transform:translateX(0)}
}

/* ❤️ Background Floating Hearts */
.bg-heart{
  position:absolute;
  width:18px;
  height:18px;
  background:#ff3b6b;
  transform:rotate(45deg);
  opacity:0.35;
  animation:heartFloat linear forwards;
}
.bg-heart::before,
.bg-heart::after{
  content:"";
  position:absolute;
  width:18px;
  height:18px;
  background:#ff3b6b;
  border-radius:50%;
}
.bg-heart::before{top:-9px;left:0}
.bg-heart::after{left:-9px;top:0}

@keyframes heartFloat{
  from{transform:translateY(0) rotate(45deg);opacity:0.4}
  to{transform:translateY(-120vh) rotate(45deg);opacity:0}
}


@keyframes pulse{
  0%{transform:scale(1)}
  50%{transform:scale(1.08)}
  100%{transform:scale(1)}
}
.fall-heart{
  position:fixed;
  top:-40px;
  width:18px;height:18px;
  background:#ff3b6b;
  transform:rotate(45deg);
  animation:fall 2s linear forwards;
  z-index:999;
}
.fall-heart:before,.fall-heart:after{
  content:'';
  position:absolute;
  width:18px;height:18px;
  background:#ff3b6b;
  border-radius:50%;
}
.fall-heart:before{top:-9px;left:0}
.fall-heart:after{left:-9px;top:0}
@keyframes fall{
  to{transform:translateY(110vh) rotate(45deg);opacity:0}
}

</style>

</head>
<body>

<audio id="bgMusic" loop>
  <source src="https://cdn.pixabay.com/download/audio/2022/11/15/audio_38c9c83894.mp3" type="audio/mpeg">
</audio>

<div class="container" id="home">
  <h1>मेरी आख़िरी बात ❤️</h1>
  <p class="lead">यह पेज सिर्फ तुम्हारे लिए…</p>
  <button class="btn" id="openBtn">Open Message 🔒</button>
</div>

<div class="overlay" id="overlay">
  <div class="modal">

    <div id="lockScreen">
      <h2>Private Message 🔐</h2>
      <p style="opacity:.8">Password डालिए</p>
      <div style="opacity:.8;margin-bottom:6px">kon ?</div>
      <div id="pwdError" style="color:#ff3b6b;font-size:13px;height:18px"></div>
      <input type="password" id="pwd">
      <br>
      <button class="btn" id="unlockBtn">Unlock</button>
    </div>

    <div id="content" style="display:none">
      <button class="close-btn" id="closeBtn">✕</button>
      <div id="page"></div>

      <div class="nav">
        <button id="prevBtn">◀ Back</button>
        <div class="counter" id="count"></div>
        <button id="nextBtn">Next ▶</button>
      </div>
    </div>

  </div>
</div>

<script>
document.addEventListener('DOMContentLoaded', ()=>{

const pages = [
`Main jaanta hoon yeh padhna aasaan nahi hoga...
Par kuch baatein dil mein hi reh jaayein
to zindagi bhar bojh ban jaati hain.

Isliye aaj,
  poori izzat aur sukoon ke saath
main apne dil ki baat rakh raha hoon.`,
`Dil ki baat ❤️

Na tere jaisa koi chahiye,
  na tujhse behtar koi chahiye.
Lakho–karodo ki bheed me bhi
mujhe bas tu hi chahiye.

Jo dard hai,
  wo main tumse hi le loonga,
  lekin mere ussi dard par
marham lagane ke liye bhi
mujhe sirf tu hi chahiye.

Agar tujhse mohabbat karna gunaah hai,
  to uski saza bhi manzoor hai,
  kyunki us saza ke baad bhi
mujhe sirf tu hi chahiye.

Kitna bhi intezaar karna pade,
  main kar loonga,
  par uske baad
mere dil ko sirf tu hi chahiye.

Haan,
  logon ki hazaar buri baatein bhi sun loonga,
  sab kuch jhel loonga,
  lekin in sabke baad bhi
mujhe sirf tu hi… sirf tu hi chahiye.

Har pal,
  har lamha,
  har ghadi…
mere dil me,
  meri duaaon me,
  sirf tu hi chahiye.`,
`Memory with U ❤️

Tumhare saath ki kuch yaadein...
Tumko yaad hai wo din,
  jis din maine anjaane me tumhe pehli baar rula diya tha…
us din ke baad maine 2 din tak tumse baat nahi ki thi,
  yaad hai?

Tumko yaad hai,
  tumhe mere baare me kitne sapne aate the...
Yaad hai,
  maine sabse pehle tumhare Abba ka naam poocha tha...
Aur tum hans padi thi.

Yaad hai jaana,
  tum mujhe kitna sataati thi...
Tum chhoti-chhoti baaton par gussa ho jaati thi...
Aur bolti thi,
  “us ladki se door raho… baat mat karo!”

Yaad hai wo ladki Sneha...
jisne mujhe message kiya tha...
Tumne usse kitni baatein ki thi sirf gussa hone ke liye.

Tumko yaad hai,
  tumne AI ko ‘I love you’ bola tha...
Aur fir hansi nahi ruk rahi thi tumhari.

Yaad hai,
  mera number tumhe kahan se mila tha...
Yaad hai,
  tumhe dekhe bina ek pal nahi rehta tha main.`,
`Tumko याद है,
  tumhare paas mobile nahi hota tha...
Isliye tum kisi ke bhi phone se call karti thi.
Kuch bhi ho jaaye,
  tum hamesha kuch na kuch karke message zaroor karti thi.

याद है na,
  tumhare liye main raat raat bhar jagta tha...
Aur tum meri बात nahi maanti thi...
Call cut karti thi...
Aur phir mood off kar leti thi.

याद है,
  maine tumhe pehli baar chocolate di thi...
Aur tum bachchon ki tarah khush ho gayi thi.

Tumko पता है?
Kaam shuru karne se pehle tumhe dekhna
mere dil ko kitna sukoon deta tha.

याद है,
  maine tumhe kuch diya tha...
Aaj bhi tumhare paas hai — wo 🔑.

याद है,
  jab tum meri बात nahi maanti thi
To main kitna gussa karta tha.

याद है...
Tum meri baat nahi maani thi ek din...
Aur maine gusse me apna haath kaat liya tha.

Yaad hai... kitni baar haath kaat diya tha maine...`,
`Tum ko yaad hai pehli baar tumko chhua tha,
  touch kiya tha,
  tum wahan se bhaag gayi thi.
Tumko yaad hai,
  tumse koi ladka baat kare to kitna gussa aata tha.
Tumko yaad hai,
  tumhe online work ke liye paise chahiye the,
  to maine diye… par tumne mujhe jhooth bolkar paise liye the.
Dukh is baat ka tha ki tumne meri baat par vishwas nahi kiya online work ke baare me.
Tumko yaad hai,
  main hamesha tum par gussa karta tha… fir agle din hum dono fir se normal ho jaate the.
Hum dono kitne acche the jaana… 😔😔
I miss you jaana… 😔
Khush rehna… ab hum kabhi nahi milenge.
Tum meri yaadon me hamesha mere saath rahogi.
Jab tak zinda hoon… mujhe ab sukoon ki talaash rahegi.
Shayad main na rahu… par tumhe hamesha protect karunga.
Ok jaana… main ja raha hoon tumhara shehar chhod kar… tumse door…
Alvida jaana… 👋😔
Alvida HYD`,
`Title Tumhari Aadat ❤️

Tumhari aadat mujhe ye he
tumhari hansi ka,
  tumhara message karna.
Tum bolti thi: hmm,
  haa,
  khana khaya,
  kya kar rahe ho,
  kya banaya,
  1 bat batao,
  ha ek bat suno,
  ny ny ny ny,
  ashe hi,
  kyu,
  gussa mat dilao,
  hloo...
Tumhari baaton me bahut kuch tha.
Main aadat ban chuka tha.

Aadat hoti hai na,
  roz thodi thodi badh jaati hai,
  aur ek din dil ka hissa ban jaati hai.
Tum bhi mere dil ka wahi hissa thi.
Par aadate kabhi kabhi
zindagi se door karni padti hain.

Tumhari aabaj ufff kitna sukun deti he.`,
`Aaj bhi jab phone ka notification aata hai,
ek pal ko lagta hai
shayad tum ho, jaana.

Har libaas me,
har bheed me,
mujhe aksar lagta hai
tum hi ho, jaana.

Tum meri aadat thi,
aur aadate aasani se chhootti nahi.

Par main tumhari majboori samajhta hoon
aur tumhari izzat karta hoon,
isliye chhod raha hoon.

Tum jaha bhi ho,
khush raho. 💔😔`,
`<div style="text-align:center;line-height:1.45;font-size:13px;">
<b>Aakhri bat</b><br><br>
Thik he jaana hamaari kahani yahi tak thi<br>
Mujhe pata he kuch nahi ho sakta is liye<br>
Ab me tum ko yaad karte huy sota hu<br><br>
aadat thi tum mere dhire dhire sayad thik ho jayga par me hamesha tum ko chaha tha tum ko hi chahunga<br><br>
Me jab tak zinda hu hamesha tumhara hi rahunga<br>
Hamesha khush rahna dhyan rkhna<br>
thankyou very much jaana<br><br>
Pata nahi me rahunga ya nahi par<br>
Meri zindagi me aai tum sach me meri zindagi me bahut sukun diya you are the best or beautiful cute and meri zindagi ki sahzadi<br><br>
kuch bhi ho jay helth ka dhyan rakhna<br>
Mujhe pata he tum teblet nhi leti ho par mere liye<br>
Teble lena mujhe sukun milega<br><br>
Milte he agle Janam me<br>
Ok jaana<br>
albida
</div>`
,
`<div style="text-align:center;line-height:1.65;font-size:17px;white-space:pre-line;">
Har pal, har lamha, har dua mein…
main bas tumhari khushi chahta hu.
Aur agar kismat ne saath diya,
to ek din tumhe apni zindagi me
izzat se, sukoon se,
bas apna kehna chahta hu
🕉️❤️☪️

❤️ I love you jaana ❤️
</div>

<button style="
  margin-top:22px;
  padding:14px 28px;
  font-size:18px;
  border:0;
  border-radius:16px;
  background:#ff3b6b;
  color:#fff;
  cursor:pointer;
  animation:pulse 1.3s infinite;
" onclick="page9Hearts()">
I love you too ❤️
<div style="font-size:14px;margin-top:6px;opacity:.9">👆 tap kro</div>
</button>

<div style="margin-top:26px;font-weight:bold;font-size:15px;">
Birthday page open karne ke liye<br>
Password: date of birth (ddmm)
</div>`
];

let i=0;
const overlay=document.getElementById('overlay');
const lockScreen=document.getElementById('lockScreen');
const content=document.getElementById('content');
const page=document.getElementById('page');
const count=document.getElementById('count');

openBtn.onclick=()=>{
  overlay.classList.add('open');
  lockScreen.style.display='block';
  content.style.display='none';
};

unlockBtn.onclick=()=>{
  if(pwd.value==='0000'){
    lockScreen.style.display='none';
    content.style.display='block';
    render();
    startPageHearts();
  }else{
    
pwdError.innerText='Password wrong — “kon ho?”';
lockScreen.classList.remove('shake');
void lockScreen.offsetWidth;
lockScreen.classList.add('shake');
if(navigator.vibrate) navigator.vibrate(150);

  }
};

closeBtn.onclick=()=>{
  overlay.classList.remove('open');
  stopPageHearts();
};
prevBtn.onclick=()=>{ if(i>0){ i--; render(); } };
nextBtn.onclick=()=>{ if(i<pages.length-1){ i++; render(); } };

function render(){
  // Pages that contain HTML markup (Page 8 & 9)
  if(i === pages.length-1 || i === pages.length-2){
    page.innerHTML = pages[i];
  }else{
    page.innerText = pages[i];
  }
  count.innerText=(i+1)+' / '+pages.length;
  page.scrollTop = 0;
}
});

// ❤️ Background heart animation (safe for scroll)
function startHearts(){
  heartInterval = setInterval(()=>{
    const h=document.createElement('div');
    h.className='bg-heart';
    h.style.left=Math.random()*100+'%';
    h.style.bottom='-20px';
    h.style.animationDuration=(6+Math.random()*6)+'s';
    document.body.appendChild(h);
    setTimeout(()=>h.remove(),12000);
  },900);
}



// ❤️ Background heart animation INSIDE text area (after unlock)
let heartInterval;
function startPageHearts(){
  if(heartInterval) return;
  const pageEl = document.getElementById('page');
  if(!pageEl) return;

  heartInterval = setInterval(()=>{
    const h=document.createElement('div');
    h.className='bg-heart';
    h.style.left=Math.random()*100+'%';
    h.style.bottom='-20px';
    h.style.animationDuration=(6+Math.random()*6)+'s';
    pageEl.appendChild(h);
    setTimeout(()=>h.remove(),12000);
  },900);
}


function stopPageHearts(){
  if(heartInterval){
    clearInterval(heartInterval);
    heartInterval = null;
  }
}


function page9Hearts(){
  for(let i=0;i<45;i++){
    const h=document.createElement('div');
    h.className='fall-heart';
    h.style.left=Math.random()*100+'%';
    document.body.appendChild(h);
    setTimeout(()=>h.remove(),2000);
  }
}

</script>

</body>
</html>
