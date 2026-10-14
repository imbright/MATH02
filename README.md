
<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>数学益智乐园</title>
<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family:system-ui, sans-serif;
}
body{
  background:#eeeeee; /*浅灰背景*/
  color:#222222;
  overflow-x:hidden;
}
.page{
  display:none;
  min-height:100vh;
  padding:24px;
  max-width:1200px;
  margin:0 auto;
}
.page.active{
  display:block;
}
.nav-bar{
  display:flex;
  gap:8px;
  margin-bottom:16px;
}
header{
  text-align:center;
  margin-bottom:20px;
}
header h1{
  color:#0066cc; /*标题蓝色*/
}
.top-bar{
  display:flex;
  justify-content:space-between;
  align-items:center;
  margin-bottom:16px;
}
.lang-switch button{
  padding:8px 14px;
  border:2px solid #000;
  background:#dddddd;
  color:#222;
  cursor:pointer;
  font-size:14px;
  border-radius:6px;
  margin:0 4px;
}
.lang-switch button.active{
  background:#0066cc;
  color:#fff;
}
.score-box{
  font-size:18px;
  font-weight:bold;
}
.player-setting{
  background:#ffffff;
  padding:16px;
  border-radius:8px;
  margin-bottom:16px;
  border:1px solid #cccccc;
}
.player-setting input{
  padding:6px;
  margin:0 8px;
  width:160px;
}
.btn{
  padding:10px 18px;
  font-size:16px;
  cursor:pointer;
  border:none;
  border-radius:6px;
  margin:6px;
  background:#348ede;
  color:#fff;
}
.btn-success{
  background:#22aa44;
}
.btn-danger{
  background:#dd4444;
}
.btn:disabled{
  background:#bbbbbb;
  opacity:0.6;
  cursor:not-allowed;
}
.game-card{
  background:#ffffff;
  padding:20px;
  border-radius:10px;
  margin:12px 0;
  border:1px solid #cccccc;
}
.question-area{
  font-size:24px;
  margin:16px 0;
}
.ans-input{
  padding:10px;
  width:320px;
  font-size:18px;
}
.progress-wrap{
  margin:10px 0;
}
.progress-bar{
  height:20px;
  background:#dddddd;
  border-radius:10px;
  overflow:hidden;
}
.progress-fill{
  height:100%;
  background:#22aa44;
  width:0%;
  transition:0.2s;
}
.difficulty-select{
  margin:12px 0;
}
.msg-correct{
  color:#22aa44;
  font-weight:bold;
}
.msg-wrong{
  color:#dd4444;
  font-weight:bold;
}
.tip-box{
  background:#fff8cc;
  border:1px solid #e6d270;
  padding:12px;
  border-radius:8px;
  margin:10px 0;
}
.player-row{
  display:flex;
  align-items:center;
  margin:8px 0;
  gap:10px;
}
.player-name{
  width:120px;
}
.player-prog-wrap{
  flex-grow:1;
}
</style>
</head>
<body>

<!-- ========== 主页界面 ========== -->
<div id="pageHome" class="page active">
  <div class="top-bar">
    <div class="lang-switch">
      <button id="btnZh" class="active">中文</button>
      <button id="btnEn">English</button>
    </div>
    <div class="score-box">
      <span>总分：</span>
      <span id="totalScore">0</span>
    </div>
  </div>

  <div class="player-setting">
    <span>玩家名称：</span>
    <input id="playerName" type="text" placeholder="输入名字">
    <span>玩家ID：</span>
    <input id="playerId" type="text" placeholder="自定义ID">
    <button class="btn" id="savePlayerBtn">保存资料</button>
  </div>

  <header>
    <h1>数学益智乐园</h1>
  </header>
  <div class="game-card">
    <h3>选择游戏</h3>
    <br>
    <button class="btn" data-goto="page24">24点</button>
    <button class="btn" data-goto="pageCalc">口算计算</button>
    <button class="btn" data-goto="pageWord">应用题</button>
    <button class="btn" data-goto="pageSudoku">数独</button>
    <button class="btn" data-goto="pageMulti">多人对战</button>
  </div>
</div>

<!-- ========== 24点独立界面 ========== -->
<div id="page24" class="page">
  <div class="nav-bar">
    <button class="btn" id="btnPrevPage">上一界面</button>
    <button class="btn" id="btnNextPage">下一界面</button>
    <button class="btn btn-danger" data-goto="pageHome">返回主页</button>
  </div>
  <div class="top-bar">
    <div class="lang-switch">
      <button id="btnZh24" class="active">中文</button>
      <button id="btnEn24">English</button>
    </div>
    <div class="score-box">
      <span>总分：</span>
      <span id="totalScore24">0</span>
    </div>
  </div>
  <div class="game-card">
    <h2>24点游戏</h2>
    <div class="difficulty-select">
      <label>难度：</label>
      <select id="diff24">
        <option value="easy">简单</option>
        <option value="mid">中等</option>
        <option value="hard">困难</option>
        <option value="devil">魔鬼训练(15分解锁)</option>
      </select>
    </div>
    <div class="question-area" id="q24"></div>
    <input class="ans-input" id="ans24" placeholder="写算式，使用 +-*/ ()">
    <br>
    <button class="btn btn-success" id="check24">提交答案</button>
    <button class="btn" id="next24">下一题</button>
    <button class="btn" id="prev24">上一题</button>
    <div id="msg24" style="margin-top:12px; font-size:18px;"></div>
  </div>
</div>

<!-- ========== 口算独立界面 ========== -->
<div id="pageCalc" class="page">
  <div class="nav-bar">
    <button class="btn" id="btnPrevPageC">上一界面</button>
    <button class="btn" id="btnNextPageC">下一界面</button>
    <button class="btn btn-danger" data-goto="pageHome">返回主页</button>
  </div>
  <div class="top-bar">
    <div class="lang-switch">
      <button id="btnZhC" class="active">中文</button>
      <button id="btnEnC">English</button>
    </div>
    <div class="score-box">
      <span>总分：</span>
      <span id="totalScoreC">0</span>
    </div>
  </div>
  <div class="game-card">
    <h2>口算计算</h2>
    <div class="difficulty-select">
      <label>难度：</label>
      <select id="diffCalc">
        <option value="easy">简单</option>
        <option value="mid">中等</option>
        <option value="hard">困难</option>
        <option value="devil">魔鬼训练(15分解锁)</option>
      </select>
    </div>
    <div class="question-area" id="qCalc"></div>
    <input class="ans-input" id="ansCalc">
    <br>
    <button class="btn btn-success" id="checkCalc">提交答案</button>
    <button class="btn" id="nextCalc">下一题</button>
    <button class="btn" id="prevCalc">上一题</button>
    <div id="msgCalc" style="margin-top:12px;"></div>
  </div>
</div>

<!-- ========== 应用题独立界面 ========== -->
<div id="pageWord" class="page">
  <div class="nav-bar">
    <button class="btn" id="btnPrevPageW">上一界面</button>
    <button class="btn" id="btnNextPageW">下一界面</button>
    <button class="btn btn-danger" data-goto="pageHome">返回主页</button>
  </div>
  <div class="top-bar">
    <div class="lang-switch">
      <button id="btnZhW" class="active">中文</button>
      <button id="btnEnW">English</button>
    </div>
    <div class="score-box">
      <span>总分：</span>
      <span id="totalScoreW">0</span>
    </div>
  </div>
  <div class="game-card">
    <h2>应用题（希望杯初赛难度）</h2>
    <div class="difficulty-select">
      <label>难度：</label>
      <select id="diffWord">
        <option value="easy">简单</option>
        <option value="mid">中等</option>
        <option value="hard">困难</option>
        <option value="devil">魔鬼训练(15分解锁)</option>
      </select>
    </div>
    <div class="question-area" id="qWord"></div>
    <input class="ans-input" id="ansWord" placeholder="填入答案数字">
    <br>
    <button class="btn btn-success" id="checkWord">提交答案</button>
    <button class="btn" id="nextWord">下一题</button>
    <button class="btn" id="prevWord">上一题</button>
    <div id="msgWord" style="margin-top:12px;"></div>
  </div>
</div>

<!-- ========== 数独独立界面 ========== -->
<div id="pageSudoku" class="page">
  <div class="nav-bar">
    <button class="btn" id="btnPrevPageS">上一界面</button>
    <button class="btn" id="btnNextPageS">下一界面</button>
    <button class="btn btn-danger" data-goto="pageHome">返回主页</button>
  </div>
  <div class="top-bar">
    <div class="lang-switch">
      <button id="btnZhS" class="active">中文</button>
      <button id="btnEnS">English</button>
    </div>
    <div class="score-box">
      <span>总分：</span>
      <span id="totalScoreS">0</span>
    </div>
  </div>
  <div class="game-card">
    <h2>数独</h2>
    <div class="difficulty-select">
      <label>难度：</label>
      <select id="diffSudo">
        <option value="easy">简单</option>
        <option value="mid">中等</option>
        <option value="hard">困难</option>
        <option value="devil">魔鬼训练(15分解锁)</option>
      </select>
    </div>
    <div id="sudokuBox"></div>
    <br>
    <button class="btn btn-success" id="checkSudo">检查</button>
    <button class="btn" id="nextSudo">新数独</button>
    <div id="msgSudo"></div>
  </div>
</div>

<!-- ========== 多人对战主菜单界面 ========== -->
<div id="pageMulti" class="page">
  <div class="nav-bar">
    <button class="btn" id="btnPrevPageM">上一界面</button>
    <button class="btn" id="btnNextPageM">下一界面</button>
    <button class="btn btn-danger" data-goto="pageHome">返回主页</button>
  </div>
  <div class="top-bar">
    <div class="lang-switch">
      <button id="btnZhM" class="active">中文</button>
      <button id="btnEnM">English</button>
    </div>
    <div class="score-box">
      <span>总分：</span>
      <span id="totalScoreM">0</span>
    </div>
  </div>
  <div class="game-card">
    <h2>多人对战</h2>
    <p style="margin:10px 0;">选择对战模式：</p>
    <button class="btn" data-goto="pageMultiBot">人机对战（你 vs Bot）</button>
    <button class="btn" data-goto="pageMultiBotVsBot">Bot对抗Bot</button>
    <button class="btn" id="btnMultiReal">真人联机</button>
    <div class="tip-box" id="multiRealTip">
      <b>提示：</b>真人联机需要后端服务。你可以把网页上传到GitHub，用GitHub Pages托管网页，但GitHub Pages不能处理实时联机通信，还需要搭配 Firebase/Supabase 数据库才能实现跨设备真人对战。本地打开网页只能预览界面。
    </div>
  </div>
</div>

<!-- ========== 人机对战界面（你 vs Bot） ========== -->
<div id="pageMultiBot" class="page">
  <div class="nav-bar">
    <button class="btn" id="btnPrevPageMB">上一界面</button>
    <button class="btn" id="btnNextPageMB">下一界面</button>
    <button class="btn btn-danger" data-goto="pageMulti">返回多人菜单</button>
  </div>
  <div class="top-bar">
    <div class="lang-switch">
      <button id="btnZhMB" class="active">中文</button>
      <button id="btnEnMB">English</button>
    </div>
    <div class="score-box">
      <span>总分：</span>
      <span id="totalScoreMB">0</span>
    </div>
  </div>
  <div class="game-card">
    <h2>人机对战（你 vs Bot）</h2>
    <div class="difficulty-select">
      <label>题目类型：</label>
      <select id="multiQType">
        <option value="24">24点</option>
        <option value="calc">口算</option>
        <option value="word">应用题</option>
      </select>
    </div>
    <div class="difficulty-select">
      <label>Bot难度：</label>
      <select id="botDiff">
        <option value="easy">简单Bot</option>
        <option value="mid">中等Bot</option>
        <option value="hard">困难Bot</option>
      </select>
    </div>
    <div class="player-row">
      <span class="player-name">你</span>
      <div class="player-prog-wrap">
        <div class="progress-bar"><div class="progress-fill" id="progPlayer" style="width:0%"></div></div>
      </div>
    </div>
    <div class="player-row">
      <span class="player-name">Bot</span>
      <div class="player-prog-wrap">
        <div class="progress-bar"><div class="progress-fill" id="progBot" style="width:0%"></div></div>
      </div>
    </div>
    <div class="question-area" id="multiQuestion"></div>
    <input class="ans-input" id="multiAnsInput">
    <br>
    <button class="btn btn-success" id="multiSubmit">提交答案</button>
    <button class="btn" id="startBotRace">开始比赛</button>
    <div id="multiBotMsg"></div>
    <div id="multiBotResult"></div>
  </div>
</div>

<!-- ========== Bot vs Bot 对战界面 ========== -->
<div id="pageMultiBotVsBot" class="page">
  <div class="nav-bar">
    <button class="btn" id="btnPrevPageBB">上一界面</button>
    <button class="btn" id="btnNextPageBB">下一界面</button>
    <button class="btn btn-danger" data-goto="pageMulti">返回多人菜单</button>
  </div>
  <div class="top-bar">
    <div class="lang-switch">
      <button id="btnZhBB" class="active">中文</button>
      <button id="btnEnBB">English</button>
    </div>
    <div class="score-box">
      <span>总分：</span>
      <span id="totalScoreBB">0</span>
    </div>
  </div>
  <div class="game-card">
    <h2>Bot对抗Bot</h2>
    <div class="difficulty-select">
      <label>题目类型：</label>
      <select id="bbQType">
        <option value="24">24点</option>
        <option value="calc">口算</option>
        <option value="word">应用题</option>
      </select>
    </div>
    <div class="player-row">
      <span class="player-name">Bot A</span>
      <div class="player-prog-wrap">
        <div class="progress-bar"><div class="progress-fill" id="progBotA" style="width:0%"></div></div>
      </div>
    </div>
    <div class="player-row">
      <span class="player-name">Bot B</span>
      <div class="player-prog-wrap">
        <div class="progress-bar"><div class="progress-fill" id="progBotB" style="width:0%"></div></div>
      </div>
    </div>
    <div class="question-area" id="bbQuestion"></div>
    <button class="btn" id="startBBRace">开始Bot对决</button>
    <div id="bbMsg"></div>
    <div id="bbResult"></div>
  </div>
</div>

<script>
// ========== 全局变量 ==========
let lang = "zh";
let score = 0;
let player = {name:"", id:""};
let pageHistory = [];
let historyIndex = -1;

// 语言包，所有文字+题目全部放这里，切换语言一次性全部刷新
const langPack = {
  zh:{
    totalText:"总分：",
    playerName:"玩家名称：",
    playerID:"玩家ID：",
    saveProfile:"保存资料",
    gameSelect:"选择游戏",
    game24:"24点游戏",
    gameCalc:"口算计算",
    gameWord:"应用题（希望杯初赛难度）",
    gameSudo:"数独",
    gameMulti:"多人对战",
    multiMenuTitle:"多人对战",
    modePlayerVsBot:"人机对战（你 vs Bot）",
    modeBotVsBot:"Bot对抗Bot",
    modeRealPlayer:"真人联机",
    realTip:"提示：真人联机需要后端服务。你可以把网页上传到GitHub，用GitHub Pages托管网页，但GitHub Pages不能处理实时联机通信，还需要搭配 Firebase/Supabase 数据库才能实现跨设备真人对战。本地打开网页只能预览界面。",
    diffEasy:"简单",
    diffMid:"中等",
    diffHard:"困难",
    diffDevil:"魔鬼训练(15分解锁)",
    submit:"提交答案",
    nextQ:"下一题",
    prevQ:"上一题",
    prevPage:"上一界面",
    nextPage:"下一界面",
    home:"返回主页",
    backMultiMenu:"返回多人菜单",
    check:"检查",
    newSudo:"新数独",
    progress:"答题进度",
    startRace:"开始比赛",
    startBotRace:"开始比赛",
    startBBRace:"开始Bot对决",
    qType:"题目类型：",
    botDifficulty:"Bot难度：",
    botEasy:"简单Bot",
    botMid:"中等Bot",
    botHard:"困难Bot",
    you:"你",
    bot:"Bot",
    botA:"Bot A",
    botB:"Bot B",
    correct:"答对！",
    wrong:"答案不对",
    formulaErr:"算式错误",
    raceFinish:"比赛结束！",
    rank1:"第一名",
    rank2:"第二名",
    rank3:"第三名"
  },
  en:{
    totalText:"Points: ",
    playerName:"Player Name:",
    playerID:"Player ID:",
    saveProfile:"Save Profile",
    gameSelect:"Select Game",
    game24:"24 Game",
    gameCalc:"Mental Math",
    gameWord:"Word Problems (Hope Cup Level)",
    gameSudo:"Sudoku",
    gameMulti:"Multiplayer",
    multiMenuTitle:"Multiplayer",
    modePlayerVsBot:"Player vs Bot",
    modeBotVsBot:"Bot vs Bot",
    modeRealPlayer:"Real Players Online",
    realTip:"Tip: Real online multiplayer requires backend server. You can upload website to GitHub and use GitHub Pages to host the page. GitHub Pages cannot handle realtime player communication, you need Firebase/Supabase database for cross-device multiplayer. Local file only preview UI.",
    diffEasy:"Easy",
    diffMid:"Medium",
    diffHard:"Hard",
    diffDevil:"Devil Training (Unlock at 15pts)",
    submit:"Submit Answer",
    nextQ:"Next Question",
    prevQ:"Prev Question",
    prevPage:"Prev Page",
    nextPage:"Next Page",
    home:"Back Home",
    backMultiMenu:"Back to Multi Menu",
    check:"Check",
    newSudo:"New Sudoku",
    progress:"Progress",
    startRace:"Start Race",
    startBotRace:"Start Race",
    startBBRace:"Start Bot Battle",
    qType:"Question Type:",
    botDifficulty:"Bot Difficulty:",
    botEasy:"Easy Bot",
    botMid:"Medium Bot",
    botHard:"Hard Bot",
    you:"You",
    bot:"Bot",
    botA:"Bot A",
    botB:"Bot B",
    correct:"Correct!",
    wrong:"Wrong Answer",
    formulaErr:"Invalid Formula",
    raceFinish:"Race finished!",
    rank1:"1st Place",
    rank2:"2nd Place",
    rank3:"3rd Place"
  }
}

const pages = document.querySelectorAll(".page");
// 页面跳转函数
function gotoPage(pageId){
  pageHistory.splice(historyIndex+1);
  pageHistory.push(pageId);
  historyIndex = pageHistory.length - 1;
  pages.forEach(p=>p.classList.remove("active"));
  document.getElementById(pageId).classList.add("active");
  syncScoreAll();
  updateLangUI();
  checkDevilUnlock();
}
function goPrevPage(){
  if(historyIndex <=0) return;
  historyIndex--;
  const pageId = pageHistory[historyIndex];
  pages.forEach(p=>p.classList.remove("active"));
  document.getElementById(pageId).classList.add("active");
  syncScoreAll();
  updateLangUI();
  checkDevilUnlock();
}
function goNextPage(){
  if(historyIndex >= pageHistory.length-1) return;
  historyIndex++;
  const pageId = pageHistory[historyIndex];
  pages.forEach(p=>p.classList.remove("active"));
  document.getElementById(pageId).classList.add("active");
  syncScoreAll();
  updateLangUI();
  checkDevilUnlock();
}

// 绑定页面跳转按钮
document.querySelectorAll("[data-goto]").forEach(btn=>{
  btn.onclick = ()=>{
    gotoPage(btn.getAttribute("data-goto"));
  }
})
document.getElementById("btnPrevPage").onclick = goPrevPage;
document.getElementById("btnNextPage").onclick = goNextPage;
document.getElementById("btnPrevPageC").onclick = goPrevPage;
document.getElementById("btnNextPageC").onclick = goNextPage;
document.getElementById("btnPrevPageW").onclick = goPrevPage;
document.getElementById("btnNextPageW").onclick = goNextPage;
document.getElementById("btnPrevPageS").onclick = goPrevPage;
document.getElementById("btnNextPageS").onclick = goNextPage;
document.getElementById("btnPrevPageM").onclick = goPrevPage;
document.getElementById("btnNextPageM").onclick = goNextPage;
document.getElementById("btnPrevPageMB").onclick = goPrevPage;
document.getElementById("btnNextPageMB").onclick = goNextPage;
document.getElementById("btnPrevPageBB").onclick = goPrevPage;
document.getElementById("btnNextPageBB").onclick = goNextPage;

// 真人联机按钮，只是提示弹窗
document.getElementById("btnMultiReal").onclick = function(){
  const t = langPack[lang];
  alert(t.realTip);
}

// 全局更新语言，刷新所有文字+题目
function updateLangUI(){
  const t = langPack[lang];
  document.querySelector('.score-box span').innerText = t.totalText;
  document.querySelector('.player-setting span:nth-of-type(1)').innerText = t.playerName;
  document.querySelector('.player-setting span:nth-of-type(2)').innerText = t.playerID;
  document.getElementById("savePlayerBtn").innerText = t.saveProfile;

  // 多人菜单
  document.querySelector("#pageMulti h2").innerText = t.multiMenuTitle;
  document.querySelector("#pageMulti [data-goto=pageMultiBot]").innerText = t.modePlayerVsBot;
  document.querySelector("#pageMulti [data-goto=pageMultiBotVsBot]").innerText = t.modeBotVsBot;
  document.getElementById("btnMultiReal").innerText = t.modeRealPlayer;
  document.getElementById("multiRealTip").innerHTML = `<b>${t.realTip}</b>`;

  //人机对战页
  document.querySelector("#pageMultiBot h2").innerText = t.modePlayerVsBot;
  document.querySelector("#pageMultiBot .difficulty-select:nth-of-type(1) label").innerText = t.qType;
  document.querySelector("#pageMultiBot .difficulty-select:nth-of-type(2) label").innerText = t.botDifficulty;
  document.querySelector("#botDiff option[value=easy]").innerText = t.botEasy;
  document.querySelector("#botDiff option[value=mid]").innerText = t.botMid;
  document.querySelector("#botDiff option[value=hard]").innerText = t.botHard;
  document.querySelector("#pageMultiBot .player-row:nth-child(1) .player-name").innerText = t.you;
  document.querySelector("#pageMultiBot .player-row:nth-child(2) .player-name").innerText = t.bot;
  document.getElementById("multiSubmit").innerText = t.submit;
  document.getElementById("startBotRace").innerText = t.startBotRace;
  document.querySelector("#pageMultiBot .btn-danger").innerText = t.backMultiMenu;

  //Bot vs Bot
  document.querySelector("#pageMultiBotVsBot h2").innerText = t.modeBotVsBot;
  document.querySelector("#pageMultiBotVsBot .difficulty-select label").innerText = t.qType;
  document.querySelector("#pageMultiBotVsBot .player-row:nth-child(1) .player-name").innerText = t.botA;
  document.querySelector("#pageMultiBotVsBot .player-row:nth-child(2) .player-name").innerText = t.botB;
  document.getElementById("startBBRace").innerText = t.startBBRace;
  document.querySelector("#pageMultiBotVsBot .btn-danger").innerText = t.backMultiMenu;

  // 24页
  document.querySelector("#page24 h2").innerText = t.game24;
  document.querySelector("#diff24 option[value=easy]").innerText = t.diffEasy;
  document.querySelector("#diff24 option[value=mid]").innerText = t.diffMid;
  document.querySelector("#diff24 option[value=hard]").innerText = t.diffHard;
  document.querySelector("#diff24 option[value=devil]").innerText = t.diffDevil;
  document.getElementById("check24").innerText = t.submit;
  document.getElementById("next24").innerText = t.nextQ;
  document.getElementById("prev24").innerText = t.prevQ;

  // 口算页
  document.querySelector("#pageCalc h2").innerText = t.gameCalc;
  document.querySelector("#diffCalc option[value=easy]").innerText = t.diffEasy;
  document.querySelector("#diffCalc option[value=mid]").innerText = t.diffMid;
  document.querySelector("#diffCalc option[value=hard]").innerText = t.diffHard;
  document.querySelector("#diffCalc option[value=devil]").innerText = t.diffDevil;
  document.getElementById("checkCalc").innerText = t.submit;
  document.getElementById("nextCalc").innerText = t.nextQ;
  document.getElementById("prevCalc").innerText = t.prevQ;

  //应用题
  document.querySelector("#pageWord h2").innerText = t.gameWord;
  document.querySelector("#diffWord option[value=easy]").innerText = t.diffEasy;
  document.querySelector("#diffWord option[value=mid]").innerText = t.diffMid;
  document.querySelector("#diffWord option[value=hard]").innerText = t.diffHard;
  document.querySelector("#diffWord option[value=devil]").innerText = t.diffDevil;
  document.getElementById("checkWord").innerText = t.submit;
  document.getElementById("nextWord").innerText = t.nextQ;
  document.getElementById("prevWord").innerText = t.prevQ;

  //数独
  document.querySelector("#pageSudoku h2").innerText = t.gameSudo;
  document.querySelector("#diffSudo option[value=easy]").innerText = t.diffEasy;
  document.querySelector("#diffSudo option[value=mid]").innerText = t.diffMid;
  document.querySelector("#diffSudo option[value=hard]").innerText = t.diffHard;
  document.querySelector("#diffSudo option[value=devil]").innerText = t.diffDevil;
  document.getElementById("checkSudo").innerText = t.check;
  document.getElementById("nextSudo").innerText = t.newSudo;

  //导航文字
  document.getElementById("btnPrevPage").innerText = t.prevPage;
  document.getElementById("btnNextPage").innerText = t.nextPage;
  document.querySelector("#page24 .btn-danger").innerText = t.home;
  document.querySelector("#pageCalc .btn-danger").innerText = t.home;
  document.querySelector("#pageWord .btn-danger").innerText = t.home;
  document.querySelector("#pageSudoku .btn-danger").innerText = t.home;
  document.querySelector("#pageMulti .btn-danger").innerText = t.home;

  //重新生成当前题目，题目自动切换中英文
  gen24();
  genCalc();
  genWord();
  genSudoku();
}

// 绑定语言切换按钮
function bindLangBtn(btnZhId,btnEnId){
  const bZh = document.getElementById(btnZhId);
  const bEn = document.getElementById(btnEnId);
  bZh.onclick = function(){
    lang="zh";
    updateLangUI();
    bZh.classList.add("active");
    bEn.classList.remove("active");
  }
  bEn.onclick = function(){
    lang="en";
    updateLangUI();
    bEn.classList.add("active");
    bZh.classList.remove("active");
  }
}
bindLangBtn("btnZh","btnEn");
bindLangBtn("btnZh24","btnEn24");
bindLangBtn("btnZhC","btnEnC");
bindLangBtn("btnZhW","btnEnW");
bindLangBtn("btnZhS","btnEnS");
bindLangBtn("btnZhM","btnEnM");
bindLangBtn("btnZhMB","btnEnMB");
bindLangBtn("btnZhBB","btnEnBB");

// 魔鬼训练解锁检查：分数<15，禁用魔鬼选项
function checkDevilUnlock(){
  const canDevil = score >=15;
  document.querySelector("#diff24 option[value=devil]").disabled = !canDevil;
  document.querySelector("#diffCalc option[value=devil]").disabled = !canDevil;
  document.querySelector("#diffWord option[value=devil]").disabled = !canDevil;
  document.querySelector("#diffSudo option[value=devil]").disabled = !canDevil;
}

// 分数同步
function syncScoreAll(){
  document.getElementById("totalScore").textContent = score;
  document.getElementById("totalScore24").textContent = score;
  document.getElementById("totalScoreC").textContent = score;
  document.getElementById("totalScoreW").textContent = score;
  document.getElementById("totalScoreS").textContent = score;
  document.getElementById("totalScoreM").textContent = score;
  document.getElementById("totalScoreMB").textContent = score;
  document.getElementById("totalScoreBB").textContent = score;
  checkDevilUnlock();
}
function setScore(s){
  score = s;
  syncScoreAll();
}
setScore(0);

// 保存玩家信息
document.getElementById("savePlayerBtn").onclick = function(){
  player.name = document.getElementById("playerName").value;
  player.id = document.getElementById("playerId").value;
  alert(lang==="zh"?"玩家资料已保存":"Player saved");
}

// ========== 24点逻辑 ==========
let nums24 = [];
function gen24(){
  nums24 = [];
  for(let i=0;i<4;i++) nums24.push(Math.floor(Math.random()*9)+1);
  document.getElementById("q24").innerText = nums24.join(" , ");
  document.getElementById("msg24").innerText="";
  document.getElementById("ans24").value="";
}
document.getElementById("next24").onclick = gen24;
document.getElementById("prev24").onclick = function(){
  const t = langPack[lang];
  alert(t.prevQ);
};
document.getElementById("check24").onclick = function(){
  const t = langPack[lang];
  let exp = document.getElementById("ans24").value;
  try{
    const res = Function('"use strict";return ('+exp+')')();
    if(Math.abs(res-24)<0.001){
      document.getElementById("msg24").className="msg-correct";
      document.getElementById("msg24").innerText = t.correct + " +5";
      setScore(score+5);
    }else{
      document.getElementById("msg24").className="msg-wrong";
      document.getElementById("msg24").innerText = t.wrong;
    }
  }catch(e){
    document.getElementById("msg24").innerText = t.formulaErr;
  }
}

// ========== 口算 ==========
let qCalc = {a:0,b:0,op:"+",ans:0};
function genCalc(){
  const ops = ["+","-","*"];
  qCalc.a = Math.floor(Math.random()*50)+1;
  qCalc.b = Math.floor(Math.random()*20)+1;
  qCalc.op = ops[Math.floor(Math.random()*ops.length)];
  if(qCalc.op === "+") qCalc.ans = qCalc.a+qCalc.b;
  if(qCalc.op === "-") {qCalc.ans = qCalc.a - qCalc.b; if(qCalc.ans<0){[qCalc.a,qCalc.b]=[qCalc.b,qCalc.a]; qCalc.ans=qCalc.a-qCalc.b}}
  if(qCalc.op === "*") qCalc.ans = qCalc.a*qCalc.b;
  document.getElementById("qCalc").innerText = `${qCalc.a} ${qCalc.op} ${qCalc.b} = ?`;
  document.getElementById("msgCalc").innerText="";
  document.getElementById("ansCalc").value="";
}
document.getElementById("nextCalc").onclick = genCalc;
document.getElementById("prevCalc").onclick = function(){
  const t = langPack[lang];
  alert(t.prevQ);
};
document.getElementById("checkCalc").onclick = function(){
  const t = langPack[lang];
  const user = Number(document.getElementById("ansCalc").value);
  if(user === qCalc.ans){
    document.getElementById("msgCalc").className="msg-correct";
    document.getElementById("msgCalc").innerText = t.correct + " +3";
    setScore(score+3);
  }else{
    document.getElementById("msgCalc").className="msg-wrong";
    document.getElementById("msgCalc").innerText = t.wrong;
  }
}

// ========== 应用题 ==========
let currentWord = {};
function genWord(){
  const t = langPack[lang];
  const list = t.wordList;
  currentWord = list[Math.floor(Math.random()*list.length)];
  document.getElementById("qWord").innerText = currentWord.q;
  document.getElementById("msgWord").innerText="";
  document.getElementById("ansWord").value="";
}
document.getElementById("nextWord").onclick = genWord;
document.getElementById("prevWord").onclick = function(){
  const t = langPack[lang];
  alert(t.prevQ);
};
document.getElementById("checkWord").onclick = function(){
  const t = langPack[lang];
  const u = Number(document.getElementById("ansWord").value);
  if(u === currentWord.a){
    document.getElementById("msgWord").className="msg-correct";
    document.getElementById("msgWord").innerText = t.correct + " +6";
    setScore(score+6);
  }else{
    document.getElementById("msgWord").className="msg-wrong";
    document.getElementById("msgWord").innerText = t.wrong;
  }
}

// ========== 数独 ==========
function genSudoku(){
  const box = document.getElementById("sudokuBox");
  box.innerHTML="";
  for(let r=0;r<9;r++){
    let rowDiv = document.createElement("div");
    for(let c=0;c<9;c++){
      let inp = document.createElement("input");
      inp.style.width="32px";inp.style.height="32px";inp.style.textAlign="center";
      inp.maxLength=1;
      rowDiv.appendChild(inp);
    }
    box.appendChild(rowDiv);
  }
  document.getElementById("msgSudo").innerText = "";
}
document.getElementById("nextSudo").onclick = genSudoku;
document.getElementById("checkSudo").onclick = function(){
  const t = langPack[lang];
  document.getElementById("msgSudo").className="msg-correct";
  document.getElementById("msgSudo").innerText = t.correct + " +8";
  setScore(score+8);
}

// ========== 人机对战（你 vs Bot）逻辑 ==========
let botRaceRunning = false;
let botPlayerProgress = 0;
let botBotProgress = 0;
let botRaceTotal = 5;
let botCurrentQuestion = null;

document.getElementById("startBotRace").onclick = function(){
  if(botRaceRunning) return;
  botRaceRunning = true;
  botPlayerProgress = 0;
  botBotProgress = 0;
  document.getElementById("progPlayer").style.width = "0%";
  document.getElementById("progBot").style.width = "0%";
  document.getElementById("multiBotMsg").innerText = "";
  document.getElementById("multiBotResult").innerText = "";
  nextBotRaceQuestion();
}
function nextBotRaceQuestion(){
  const qType = document.getElementById("multiQType").value;
  const t = langPack[lang];
  if(qType === "24"){
    const arr = [];
    for(let i=0;i<4;i++) arr.push(Math.floor(Math.random()*9)+1);
    botCurrentQuestion = {type:"24", nums:arr, answer:24};
    document.getElementById("multiQuestion").innerText = arr.join(" , ");
  }else if(qType === "calc"){
    const ops = ["+","-","*"];
    const a = Math.floor(Math.random()*50)+1;
    const b = Math.floor(Math.random()*20)+1;
    const op = ops[Math.floor(Math.random()*ops.length)];
    let ans;
    if(op ==="+") ans=a+b;
    else if(op ==="-") ans = a-b;
    else ans = a*b;
    botCurrentQuestion = {type:"calc", q:`${a} ${op} ${b}`, answer:ans};
    document.getElementById("multiQuestion").innerText = botCurrentQuestion.q;
  }else if(qType === "word"){
    const list = t.wordList;
    const w = list[Math.floor(Math.random()*list.length)];
    botCurrentQuestion = {type:"word", q:w.q, answer:w.a};
    document.getElementById("multiQuestion").innerText = w.q;
  }
}
document.getElementById("multiSubmit").onclick = function(){
  if(!botRaceRunning) return;
  const t = langPack[lang];
  const userAns = document.getElementById("multiAnsInput").value.trim();
  let correct = false;
  if(botCurrentQuestion.type === "24"){
    try{
      const v = Function('"use strict";return ('+userAns+')')();
      if(Math.abs(v-24)<0.001) correct=true;
    }catch(e){}
  }else{
    if(Number(userAns) === botCurrentQuestion.answer) correct = true;
  }
  if(correct){
    botPlayerProgress +=1;
    document.getElementById("progPlayer").style.width = (botPlayerProgress / botRaceTotal *100)+"%";
    document.getElementById("multiBotMsg").className="msg-correct";
    document.getElementById("multiBotMsg").innerText = t.correct;
  }else{
    document.getElementById("multiBotMsg").className="msg-wrong";
    document.getElementById("multiBotMsg").innerText = t.wrong;
  }
  // Bot自动答题
  const botDiff = document.getElementById("botDiff").value;
  let botChance = 0.4;
  if(botDiff ==="easy") botChance=0.3;
  if(botDiff ==="mid") botChance=0.6;
  if(botDiff ==="hard") botChance=0.85;
  if(Math.random() < botChance){
    botBotProgress +=1;
    document.getElementById("progBot").style.width = (botBotProgress / botRaceTotal *100)+"%";
  }
  document.getElementById("multiAnsInput").value="";

  // 判断比赛结束
  if(botPlayerProgress >= botRaceTotal || botBotProgress >= botRaceTotal){
    botRaceRunning = false;
    let winnerText;
    if(botPlayerProgress > botBotProgress){
      winnerText = t.raceFinish + " " + t.rank1 + "：你！+10分";
      setScore(score+10);
    }else if(botBotProgress > botPlayerProgress){
      winnerText = t.raceFinish + " " + t.rank1 + "：Bot";
    }else{
      winnerText = t.raceFinish + " 平局";
    }
    document.getElementById("multiBotResult").innerText = winnerText;
  }else{
    setTimeout(nextBotRaceQuestion, 800);
  }
}

// ========== Bot vs Bot 对战逻辑 ==========
let bbRaceRunning = false;
let bbBotAProg = 0;
let bbBotBProg = 0;
const bbTotal = 5;

document.getElementById("startBBRace").onclick = function(){
  if(bbRaceRunning) return;
  bbRaceRunning = true;
  bbBotAProg = 0;
  bbBotBProg = 0;
  document.getElementById("progBotA").style.width="0%";
  document.getElementById("progBotB").style.width="0%";
  document.getElementById("bbMsg").innerText="";
  document.getElementById("bbResult").innerText="";
  runBotBattleRound();
}
function runBotBattleRound(){
  const t = langPack[lang];
  const qType = document.getElementById("bbQType").value;
  let qText = "";
  if(qType === "24"){
    const arr = [];
    for(let i=0;i<4;i++) arr.push(Math.floor(Math.random()*9)+1);
    qText = arr.join(" , ");
  }else if(qType === "calc"){
    const ops = ["+","-","*"];
    const a = Math.floor(Math.random()*50)+1;
    const b = Math.floor(Math.random()*20)+1;
    const op = ops[Math.floor(Math.random()*ops.length)];
    qText = `${a} ${op} ${b} = ?`;
  }else if(qType === "word"){
    const list = t.wordList;
    const w = list[Math.floor(Math.random()*list.length)];
    qText = w.q;
  }
  document.getElementById("bbQuestion").innerText = qText;

  // BotA BotB随机答对
  if(Math.random()>0.4) bbBotAProg++;
  if(Math.random()>0.4) bbBotBProg++;
  document.getElementById("progBotA").style.width = (bbBotAProg/bbTotal*100)+"%";
  document.getElementById("progBotB").style.width = (bbBotBProg/bbTotal*100)+"%";

  if(bbBotAProg >= bbTotal || bbBotBProg >= bbTotal){
    bbRaceRunning = false;
    let resText;
    if(bbBotAProg > bbBotBProg){
      resText = t.raceFinish + " " + t.rank1 + " Bot A";
    }else if(bbBotBProg > bbBotAProg){
      resText = t.raceFinish + " " + t.rank1 + " Bot B";
    }else{
      resText = t.raceFinish + " 平局";
    }
    document.getElementById("bbResult").innerText = resText;
    return;
  }
  setTimeout(runBotBattleRound, 1000);
}

//初始化
pageHistory.push("pageHome");
historyIndex = 0;
updateLangUI();
checkDevilUnlock();
</script>
</body>
</html>
