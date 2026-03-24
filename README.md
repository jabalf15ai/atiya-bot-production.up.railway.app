# atiya-bot-production.up.railway.app
jabalf15ai/atiya-bot
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>عطية — مساعدك الذكي</title>
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;900&family=Cairo:wght@400;600;700;900&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0D0D0D; --bg2: #141414; --bg3: #1A1A1A;
  --gold: #D4A843; --gold2: #F0C96A; --gold3: #8B6914;
  --green: #25D366; --green2: #128C7E;
  --white: #F5F0E8; --gray: #888; --gray2: #555;
}
* { margin:0; padding:0; box-sizing:border-box; }
html, body { height:100%; }
body {
  font-family:'Tajawal',sans-serif;
  background:var(--bg); color:var(--white);
  height:100vh; display:flex; flex-direction:column; overflow:hidden;
}

/* HEADER */
.header {
  padding:12px 20px;
  background:rgba(13,13,13,0.98);
  border-bottom:1px solid rgba(212,168,67,0.15);
  display:flex; align-items:center; justify-content:space-between;
  flex-shrink:0;
}
.header-left { display:flex; align-items:center; gap:12px; }
.avatar-wrap { position:relative; width:48px; height:48px; }
.avatar-img {
  width:48px; height:48px; border-radius:50%; object-fit:cover;
  border:2px solid rgba(37,211,102,0.4);
  box-shadow:0 0 15px rgba(37,211,102,0.15);
}
.online-dot {
  position:absolute; bottom:1px; right:1px;
  width:12px; height:12px; background:var(--green);
  border-radius:50%; border:2px solid var(--bg);
  animation:pulseG 1.8s infinite;
}
@keyframes pulseG {
  0%,100%{box-shadow:0 0 0 0 rgba(37,211,102,0.4);}
  50%{box-shadow:0 0 0 5px rgba(37,211,102,0);}
}
.bot-name { font-size:17px; font-weight:900; color:#fff; font-family:'Cairo',sans-serif; }
.bot-status { font-size:12px; color:var(--green); margin-top:2px; }
.header-badge {
  padding:4px 12px; border-radius:20px; font-size:11px;
  background:rgba(212,168,67,0.08); border:1px solid rgba(212,168,67,0.2);
  color:var(--gold); font-weight:600;
}

/* QUICK BAR */
.quick-bar {
  padding:8px 20px;
  background:rgba(13,13,13,0.95);
  border-bottom:1px solid rgba(255,255,255,0.04);
  display:flex; gap:8px; overflow-x:auto; flex-shrink:0;
}
.quick-bar::-webkit-scrollbar { display:none; }
.qbtn {
  padding:6px 14px; border-radius:20px; font-size:12px;
  font-family:'Tajawal',sans-serif; cursor:pointer;
  white-space:nowrap; border:1px solid; flex-shrink:0;
  transition:all 0.2s;
  background:rgba(37,211,102,0.08); border-color:rgba(37,211,102,0.25); color:var(--green);
}
.qbtn:hover { transform:translateY(-1px); opacity:0.85; }
.qbtn.d { background:rgba(212,168,67,0.08); border-color:rgba(212,168,67,0.25); color:var(--gold); }

/* MESSAGES */
.messages {
  flex:1; overflow-y:auto; padding:18px 20px;
  display:flex; flex-direction:column; gap:14px;
  background:var(--bg);
}
.messages::-webkit-scrollbar { width:3px; }
.messages::-webkit-scrollbar-thumb { background:var(--gray2); border-radius:3px; }
.msg-date {
  text-align:center; font-size:11px; color:var(--gray2);
  padding:4px 14px; background:rgba(255,255,255,0.04);
  border-radius:10px; align-self:center;
}
.msg { display:flex; flex-direction:column; max-width:80%; animation:fadeUp 0.25s ease; }
@keyframes fadeUp { from{opacity:0;transform:translateY(8px);} to{opacity:1;transform:translateY(0);} }
.msg.user { align-self:flex-start; }
.msg.bot  { align-self:flex-end; }
.bubble {
  padding:11px 15px; font-size:14px; line-height:1.75;
  border-radius:16px; word-break:break-word;
}
.msg.user .bubble {
  background:rgba(255,255,255,0.06); border:1px solid rgba(255,255,255,0.07);
  border-bottom-right-radius:4px; color:var(--white);
}
.msg.bot .bubble {
  background:rgba(18,44,25,0.85); border:1px solid rgba(37,211,102,0.12);
  border-bottom-left-radius:4px; color:#dff5d8;
}
.bubble strong { color:var(--gold2); font-weight:700; }
.msg-meta { font-size:10px; color:var(--gray2); margin-top:4px; padding:0 4px; }
.msg.user .msg-meta { text-align:right; }
.msg.bot  .msg-meta { text-align:left; }

/* TYPING */
.typing {
  align-self:flex-end; display:flex; align-items:center; gap:5px;
  background:rgba(18,44,25,0.85); border:1px solid rgba(37,211,102,0.12);
  border-radius:16px; border-bottom-left-radius:4px; padding:13px 17px;
}
.dot { width:7px; height:7px; border-radius:50%; background:var(--green); opacity:0.5; animation:bounce 1.2s infinite; }
.dot:nth-child(2){animation-delay:0.2s;} .dot:nth-child(3){animation-delay:0.4s;}
@keyframes bounce { 0%,80%,100%{transform:translateY(0);opacity:0.4;} 40%{transform:translateY(-7px);opacity:1;} }

/* INPUT */
.input-area {
  padding:12px 20px;
  background:rgba(13,13,13,0.98);
  border-top:1px solid rgba(255,255,255,0.05);
  display:flex; align-items:flex-end; gap:10px; flex-shrink:0;
}
.msg-ta {
  flex:1; background:rgba(255,255,255,0.06);
  border:1px solid rgba(37,211,102,0.15); border-radius:22px;
  padding:12px 18px; color:var(--white);
  font-family:'Tajawal',sans-serif; font-size:14px;
  outline:none; resize:none; min-height:46px; max-height:130px;
  line-height:1.5; transition:border-color 0.2s;
}
.msg-ta:focus { border-color:var(--green); }
.msg-ta::placeholder { color:rgba(255,255,255,0.2); }
.btn-send {
  width:46px; height:46px; flex-shrink:0;
  background:var(--green); border:none; border-radius:50%;
  color:#fff; cursor:pointer; display:flex; align-items:center; justify-content:center;
  transition:all 0.2s; box-shadow:0 4px 15px rgba(37,211,102,0.25);
}
.btn-send:hover { background:#1ebc5b; transform:scale(1.06); }
.btn-send:disabled { opacity:0.35; cursor:not-allowed; transform:none; }

/* TOAST */
.toast {
  position:fixed; bottom:80px; left:50%; transform:translateX(-50%);
  background:var(--bg3); border:1px solid var(--gold);
  border-radius:10px; padding:10px 22px;
  font-size:13px; color:var(--gold); z-index:999;
  animation:toastIn 0.3s ease;
}
@keyframes toastIn {
  from{opacity:0;transform:translateX(-50%) translateY(16px);}
  to{opacity:1;transform:translateX(-50%) translateY(0);}
}

/* WELCOME */
.welcome { align-self:center; text-align:center; padding:24px 20px; max-width:340px; animation:fadeUp 0.5s ease; }
.wel-img {
  width:88px; height:88px; border-radius:50%; object-fit:cover;
  margin:0 auto 14px; display:block;
  border:3px solid rgba(37,211,102,0.4);
  box-shadow:0 0 35px rgba(37,211,102,0.18);
}
.welcome h2 { font-size:20px; font-weight:900; margin-bottom:8px; }
.welcome p { font-size:13px; color:var(--gray); line-height:1.7; }
.wel-hint {
  margin-top:14px; padding:10px 14px;
  background:rgba(212,168,67,0.07); border:1px solid rgba(212,168,67,0.15);
  border-radius:10px; font-size:12px; color:var(--gold); line-height:1.9;
}
</style>
</head>
<body>

<!-- HEADER -->
<div class="header">
  <div class="header-left">
    <div class="avatar-wrap">
      <img class="avatar-img"
        src="WhatsApp_Image_2026-03-12_at_4_35_05_AM.jpeg" alt="عطية"
        onerror="this.src='data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 width=%2248%22 height=%2248%22 viewBox=%220 0 48 48%22%3E%3Ccircle cx=%2224%22 cy=%2224%22 r=%2224%22 fill=%22%23128C7E%22/%3E%3Ctext x=%2224%22 y=%2231%22 text-anchor=%22middle%22 font-size=%2222%22%3E🤖%3C/text%3E%3C/svg%3E'">
      <div class="online-dot"></div>
    </div>
    <div>
      <div class="bot-name">عطية</div>
      <div class="bot-status">متصل · يبحث ويقارن لك</div>
    </div>
  </div>
  <div class="header-badge">JABALF15 ✦</div>
</div>

<!-- QUICK BAR -->
<div class="quick-bar">
  <button class="qbtn" onclick="qs('قارن لي اسعار تذاكر الطيران من المدينة المنورة للرياض بكره من جميع شركات الطيران')">✈️ تذاكر طيران</button>
  <button class="qbtn" onclick="qs('وين احسن عروض وتخفيضات الاسبوع هذا في السعودية؟')">🏷️ عروض وتخفيضات</button>
  <button class="qbtn" onclick="qs('قارن لي افضل مطاعم في المدينة المنورة مع الاسعار التقريبية')">🍽️ مطاعم</button>
  <button class="qbtn" onclick="qs('وش افضل الفعاليات والانشطة هذا الاسبوع في السعودية؟')">🎪 فعاليات</button>
  <button class="qbtn d" onclick="qs('قارن لي بين منتجين واعطني الافضل بالنسبة للسعر والجودة')">⚖️ مقارنة</button>
</div>

<!-- MESSAGES -->
<div class="messages" id="msgs">
  <div class="msg-date">اليوم</div>
  <div class="welcome">
    <img class="wel-img"
      src="WhatsApp_Image_2026-03-12_at_4_35_05_AM.jpeg" alt="عطية"
      onerror="this.src='data:image/svg+xml,%3Csvg xmlns=%22http://www.w3.org/2000/svg%22 width=%2288%22 height=%2288%22 viewBox=%220 0 88 88%22%3E%3Ccircle cx=%2244%22 cy=%2244%22 r=%2244%22 fill=%22%23128C7E%22/%3E%3Ctext x=%2244%22 y=%2257%22 text-anchor=%22middle%22 font-size=%2240%22%3E🤖%3C/text%3E%3C/svg%3E'">
    <h2>أهلاً! أنا عطية 👋</h2>
    <p>أبحث وأقارن أي شي تطلبه — تذاكر، عروض، مطاعم، فعاليات، أو أي مقارنة تبيها</p>
    <div class="wel-hint">
      ✈️ تذاكر طيران &nbsp;|&nbsp; 🏷️ عروض وتخفيضات<br>
      🍽️ مطاعم &nbsp;|&nbsp; 🎪 فعاليات<br>
      ⚖️ مقارنة أي منتج أو خدمة
    </div>
  </div>
</div>

<!-- INPUT -->
<div class="input-area">
  <textarea class="msg-ta" id="inp"
    placeholder="اسألني عن أي شي وأنا أبحث وأقارن لك!"
    onkeydown="handleKey(event)" oninput="rsz(this)" rows="1" disabled></textarea>
  <button class="btn-send" id="sendBtn" onclick="send()" disabled>
    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
      <line x1="22" y1="2" x2="11" y2="13"/>
      <polygon points="22 2 15 22 11 13 2 9 22 2"/>
    </svg>
  </button>
</div>

<script>
const IBAN  = 'SA46 8000 0198 6080 1021 0195';
const BANK  = 'الراجحي';
const OWNER = 'أنس مبيريك ساعد اللهيبي الحربي';
const FEE   = '5';

let apiKey = '', history = [], active = false;

const SYSTEM = `أنت "عطية"، مساعد ذكي شبابي سعودي متخصص في البحث والمقارنة.

تخصصاتك:
• تذاكر الطيران — قارن شركات الطيران والأسعار والمواعيد
• عروض وتخفيضات — أفضل الديلز في المتاجر والإلكترونيات وغيرها
• مطاعم — قارن الخيارات بالسعر والتقييم والنوع وأين تتواجد
• فعاليات وأنشطة — ما يحدث هذا الأسبوع أو القريب في السعودية
• مقارنة أي منتجين أو خدمتين — أيهما أفضل قيمة وليش
• أي طلب بحث أو مقارنة آخر

أسلوبك:
- عربي سعودي عصري خفيف
- مباشر ومفصّل بأسماء حقيقية وأرقام واقعية
- لا تقول "أستفسر للمسؤول" أبداً — أنت الخدمة الكاملة
- ردودك منظّمة وسهلة القراءة

في نهاية كل رد أضف:
"لو استفدت، رسوم الخدمة ${FEE} ريال — ${BANK}: ${IBAN} (${OWNER}) 🙏"`;

// يُستدعى من السيرفر أو الإعداد الخارجي
window.initBot = function(key) {
  apiKey = key || '';
  active = true;
  document.getElementById('sendBtn').disabled = false;
  document.getElementById('inp').disabled = false;
  document.getElementById('inp').placeholder = 'اسألني عن أي شي وأنا أبحث وأقارن لك!';
  addMsg('bot', 'أهلاً وسهلاً! 🎉\nجاهز أخدمك — اسأل عن تذاكر، عروض، مطاعم، فعاليات، أو أي مقارنة تبيها!');
};

async function send() {
  if (!active) return;
  const input = document.getElementById('inp');
  const text = input.value.trim();
  if (!text) return;
  input.value = ''; rsz(input);

  addMsg('user', text);
  history.push({ role:'user', content:text });
  document.getElementById('sendBtn').disabled = true;
  const typing = addTyping();

  try {
    const headers = {
      'Content-Type':'application/json',
      'anthropic-version':'2023-06-01',
      'anthropic-dangerous-direct-browser-access':'true'
    };
    if (apiKey) headers['x-api-key'] = apiKey;

    const endpoint = '/v1/messages';

    const res = await fetch(endpoint, {
      method:'POST', headers,
      body: JSON.stringify({
        model:'claude-sonnet-4-20250514',
        max_tokens:800,
        system:SYSTEM,
        messages:history
      })
    });
    const data = await res.json();
    typing.remove();

    if (data.content?.[0]?.text) {
      const reply = data.content[0].text;
      history.push({ role:'assistant', content:reply });
      addMsg('bot', reply);
    } else {
      addMsg('bot','عذراً، حاول مرة ثانية.');
    }
  } catch(e) {
    typing.remove();
    addMsg('bot','⚠️ خطأ في الاتصال.');
  }

  document.getElementById('sendBtn').disabled = false;
  document.getElementById('inp').focus();
}

function addMsg(role, text) {
  const c = document.getElementById('msgs');
  const time = new Date().toLocaleTimeString('ar',{hour:'2-digit',minute:'2-digit'});
  const div = document.createElement('div');
  div.className = `msg ${role}`;
  let html = esc(text)
    .replace(/\*\*(.*?)\*\*/g,'<strong>$1</strong>')
    .replace(/•/g,'<br>•')
    .replace(/\n/g,'<br>');
  html = html.replace(/(SA\d{2}[\d\s]{20,})/g,
    '<span style="color:var(--gold2);font-weight:700">$1</span>');
  div.innerHTML = `<div class="bubble">${html}</div>
    <div class="msg-meta">${time}${role==='bot'?' ✓✓':''}</div>`;
  c.appendChild(div); c.scrollTop = c.scrollHeight;
}

function addTyping() {
  const c = document.getElementById('msgs');
  const div = document.createElement('div');
  div.className = 'typing';
  div.innerHTML = '<div class="dot"></div><div class="dot"></div><div class="dot"></div>';
  c.appendChild(div); c.scrollTop = c.scrollHeight;
  return div;
}

function qs(text) {
  if (!active) return toast('البوت غير مشغّل بعد');
  document.getElementById('inp').value = text; send();
}
function handleKey(e) { if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();send();} }
function rsz(el) { el.style.height='auto'; el.style.height=Math.min(el.scrollHeight,130)+'px'; }
function esc(t) { return t.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }
function toast(msg) {
  document.querySelector('.toast')?.remove();
  const t=document.createElement('div'); t.className='toast'; t.textContent=msg;
  document.body.appendChild(t); setTimeout(()=>t.remove(),3000);
}
</script>
</body>
</html>
