# 单词拼写游戏



## 说明

显示乱序字母和图片，拖动或输入正确拼写。通过 image 和 letter 组合练习英语单词。



## 代码

```html

<!DOCTYPE html>

<html lang="zh">

<head><meta charset="UTF-8"><title>单词拼写</title>

<style>

body{text-align:center;font-family:Arial;margin:20px;background:#e8f5e9}

.pic{font-size:80px;margin:15px}

.letters{display:flex;justify-content:center;gap:10px;margin:15px}

.letter{width:50px;height:50px;font-size:28px;background:white;border:2px solid #4CAF50;border-radius:10px;cursor:pointer;display:flex;align-items:center;justify-content:center;font-weight:bold}

.answer{display:flex;justify-content:center;gap:5px;margin:15px;min-height:55px}

.slot{width:50px;height:50px;border:2px dashed #999;border-radius:10px;font-size:28px;display:flex;align-items:center;justify-content:center;font-weight:bold}

.slot.filled{background:#c8e6c9;border-color:#4CAF50}

#score{font-size:20px;color:#2e7d32}

</style></head>

<body>

<h2>📝 单词拼写</h2>

<div class="pic" id="pic"></div>

<div class="answer" id="answer"></div>

<div class="letters" id="letters"></div>

<div id="score">得分: 0</div>

<button onclick="nextWord()" style="padding:10px 25px;background:#4CAF50;color:white;border:none;border-radius:8px;cursor:pointer;font-size:16px">下一题</button>



<script>

const words=[{emoji:"🐶",word:"DOG"},{emoji:"🐱",word:"CAT"},{emoji:"🐟",word:"FISH"},{emoji:"🐰",word:"RABBIT"},{emoji:"🐦",word:"BIRD"}];

let current=0,score=0,placed=[];

function shuffle(s){let a=[...s];for(let i=a.length-1;i>0;i--){let j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}return a;}



function load(){let w=words[current];placed=Array(w.word.length).fill(null);document.getElementById("pic").textContent=w.emoji;render();}

function render(){

  let w=words[current];let a=document.getElementById("answer");a.innerHTML="";

  placed.forEach((l,i)=>{let s=document.createElement("div");s.className="slot";if(l){s.classList.add("filled");s.textContent=l;s.addEventListener("click",()=>{placed[i]=null;render();});}a.appendChild(s);});

  let letters=shuffle(w.word.split(""));

  let l=document.getElementById("letters");l.innerHTML="";

  letters.forEach(ch=>{let d=document.createElement("div");d.className="letter";d.textContent=ch;d.addEventListener("click",()=>{let idx=placed.indexOf(null);if(idx>=0){placed[idx]=ch;render();check();}});l.appendChild(d);});

}

function check(){let w=words[current];if(placed.join("")===w.word){score+=10;document.getElementById("score").textContent="得分: "+score;setTimeout(()=>alert("✅ 正确!"),100);}}

function nextWord(){current=(current+1)%words.length;place=[];load();}

load();

</script></body></html>

```

