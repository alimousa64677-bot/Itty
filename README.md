<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>مركز يقين | دعم المواهب الشابة</title>
<script src="https://telegram.org/js/telegram-web-app.js"></script>
<style>
:root{--bg:var(--tg-theme-bg-color,#fbfaf7);--tx:var(--tg-theme-text-color,#1c2430);--hint:var(--tg-theme-hint-color,#6b7685);--card:var(--tg-theme-secondary-bg-color,#eef1f5);--btn:var(--tg-theme-button-color,#1d3a5f);--btx:var(--tg-theme-button-text-color,#fff);--gold:#c9962b;--ok:#1a9d5a;--no:#d64545;--wait:#d98a1c;--line:rgba(127,127,127,.28)}
@media(prefers-color-scheme:dark){:root{--bg:var(--tg-theme-bg-color,#16191f);--tx:var(--tg-theme-text-color,#eef0f3);--card:var(--tg-theme-secondary-bg-color,#222831);--hint:var(--tg-theme-hint-color,#9aa5b4);--btn:var(--tg-theme-button-color,#3b78c4)}}
*{box-sizing:border-box}
html,body{margin:0}
body{background:var(--bg);color:var(--tx);font-family:system-ui,-apple-system,"Segoe UI","Noto Naskh Arabic",Tahoma,sans-serif;line-height:1.7;padding:max(16px,env(safe-area-inset-top)) 16px max(24px,env(safe-area-inset-bottom))}
main{max-width:520px;margin:0 auto}
section[hidden]{display:none}
h1{font-size:1.5rem;margin:.2rem 0 .4rem;line-height:1.4}
h2{font-size:1.15rem;margin:0 0 .6rem}
p{margin:.2rem 0 1rem;color:var(--hint)}
.brand{border-inline-start:4px solid var(--gold);padding-inline-start:12px;margin-bottom:20px}
.brand b{display:block;font-size:.85rem;color:var(--gold)}
.avatar{width:84px;height:84px;border-radius:50%;object-fit:cover;background:var(--btn);color:var(--btx);display:flex;align-items:center;justify-content:center;font-size:2rem;font-weight:700;border:3px solid var(--gold)}
.chip{display:flex;align-items:center;gap:10px;background:var(--card);border-radius:14px;padding:8px 12px;margin-bottom:18px}
.chip .avatar{width:38px;height:38px;font-size:1rem;border-width:2px}
.chip small{color:var(--hint);display:block;line-height:1.3}
.ucard{background:var(--card);border-radius:16px;padding:20px;text-align:center;margin:16px 0}
.ucard .avatar{margin:0 auto 10px}
.ucard .tick{color:var(--ok);font-weight:700;margin-top:6px}
button,.btn{font:inherit;font-weight:600;width:100%;border:0;border-radius:12px;padding:13px;background:var(--btn);color:var(--btx);cursor:pointer;margin-top:10px;transition:opacity .2s}
button:hover{opacity:.9}
button.alt{background:var(--card);color:var(--tx)}
button:focus-visible,input:focus-visible,select:focus-visible,textarea:focus-visible{outline:2px solid var(--gold);outline-offset:2px}
label{display:block;font-weight:600;margin:16px 0 6px}
label i{font-style:normal;color:var(--no)}
input,select,textarea{font:inherit;width:100%;padding:11px 12px;border-radius:10px;border:1px solid var(--line);background:var(--card);color:var(--tx)}
textarea{min-height:92px;resize:vertical}
.chk{display:flex;gap:10px;align-items:flex-start;font-weight:400;margin:8px 0;cursor:pointer}
.chk input{width:20px;height:20px;margin-top:5px;flex:none}
fieldset{border:1px solid var(--line);border-radius:12px;margin:16px 0 0;padding:6px 12px 10px}
legend{font-weight:600;padding:0 6px}
.err{color:var(--no);font-size:.9rem;min-height:1.2em;margin-top:10px}
.status{border-radius:16px;padding:20px;text-align:center;margin:12px 0;border:2px solid var(--line)}
.status .ic{font-size:2.4rem;line-height:1.2}
.status.pending{border-color:var(--wait);background:rgba(217,138,28,.08)}.status.approved{border-color:var(--ok);background:rgba(26,157,90,.08)}.status.rejected{border-color:var(--no);background:rgba(214,69,69,.08)}
.reason{background:var(--card);border-radius:10px;padding:12px;margin-top:12px;text-align:right;color:var(--tx)}
.reason small{display:block;color:var(--hint)}
</style>
</head>
<body>
<main>

<div class="brand"><b>مركز يقين للدعم الفني</b><span>برنامج دعم المواهب الشابة</span></div>

<!-- 1) شاشة التحقق -->
<section id="verify">
  <h1>أهلًا بك</h1>
  <p>اضغط للتحقق من حسابك على تيليجرام قبل التقديم.</p>
  <div id="ucard" class="ucard" hidden>
    <div id="uav"></div>
    <h2 id="uname" style="margin:4px 0 0"></h2>
    <div id="uuser" style="color:var(--hint)" dir="ltr"></div>
    <div class="tick">تم التحقق من الحساب بنجاح ✓</div>
  </div>
  <div class="err" id="verr" role="alert"></div>
  <button id="vbtn">تحقق من حسابي</button>
  <button id="vnext" class="alt" hidden>متابعة إلى البرنامج</button>
</section>

<!-- 2) الرئيسية -->
<section id="home" hidden>
  <div class="chip" id="chip1"></div>
  <h1>ادعم موهبتك</h1>
  <p>قدّم طلبك الآن وسيقوم فريق مركز يقين بمراجعته في المجموعة.</p>
  <button id="goForm">تقديم طلب جديد</button>
  <button id="goStatus" class="alt">متابعة حالة طلبي</button>
</section>

<!-- 3) نموذج التسجيل -->
<section id="formSec" hidden>
  <div class="chip" id="chip2"></div>
  <h1>طلب الانضمام</h1>
  <p>الحقول المعلّمة بنجمة (*) مطلوبة.</p>
  <form id="f" novalidate>
    <label for="age">العمر <i>*</i></label>
    <input id="age" name="age" type="number" inputmode="numeric" min="6" max="35" placeholder="مثال: 16">

    <div id="guardian" hidden>
      <label for="gname">اسم ولي الأمر <i>*</i></label>
      <input id="gname" name="guardian_name" autocomplete="off" placeholder="الاسم الكامل لولي الأمر">
      <label class="chk"><input type="checkbox" id="gok"><span>أوافق، بصفتي ولي الأمر، على مشاركة ابني/ابنتي في البرنامج.</span></label>
    </div>

    <label for="field">ما هي موهبتك؟ <i>*</i></label>
    <input id="field" name="talent_field" autocomplete="off" placeholder="اكتبها بنفسك: الخط العربي، كرة القدم، البرمجة...">

    <label for="desc">صف موهبتك <i>*</i></label>
    <textarea id="desc" name="talent_desc" placeholder="ماذا تفعل؟ ومنذ متى بدأت؟ (20 حرفاً على الأقل)"></textarea>

    <label for="exp">مستوى الخبرة <i>*</i></label>
    <select id="exp" name="experience">
      <option value="">اختر</option>
      <option>مبتدئ</option>
      <option>أقل من سنة</option>
      <option>من سنة إلى 3 سنوات</option>
      <option>أكثر من 3 سنوات</option>
    </select>

    <label for="ach">إنجازات أو مشاركات سابقة</label>
    <textarea id="ach" name="achievements" placeholder="مسابقات، معارض، شهادات... (اختياري)"></textarea>

    <fieldset>
      <legend>نوع الدعم المطلوب <i style="color:var(--no);font-style:normal">*</i></legend>
      <label class="chk"><input type="checkbox" name="support" value="تدريب"><span>تدريب وورش عمل</span></label>
      <label class="chk"><input type="checkbox" name="support" value="إرشاد"><span>إرشاد من مختص</span></label>
      <label class="chk"><input type="checkbox" name="support" value="معدات"><span>أدوات ومعدات</span></label>
      <label class="chk"><input type="checkbox" name="support" value="نشر"><span>نشر وتسويق أعمالي</span></label>
      <label class="chk"><input type="checkbox" name="support" value="تمويل"><span>دعم مالي</span></label>
    </fieldset>

    <label for="goal">ماذا تريد أن تحقق خلال سنة؟ <i>*</i></label>
    <textarea id="goal" name="goal" placeholder="هدفك المستقبلي..."></textarea>

    <label class="chk" style="margin-top:18px"><input type="checkbox" id="agree"><span>أقرّ بأن المعلومات صحيحة، وأوافق على إرسالها إلى إدارة مركز يقين.</span></label>

    <div class="err" id="err" role="alert"></div>
    <button type="submit" id="sbtn">إرسال الطلب</button>
    <button type="button" class="alt" id="cancel">رجوع</button>
  </form>
</section>

<!-- 4) حالة الطلب -->
<section id="statusSec" hidden>
  <div class="chip" id="chip3"></div>
  <h1>حالة طلبي</h1>
  <div id="stBox"></div>
  <button id="refresh" class="alt">تحديث الحالة</button>
  <button id="stHome" class="alt">الصفحة الرئيسية</button>
</section>

</main>

<script>
/* ========================================================
   الربط المباشر مع بوت ومجموعة مركز يقين
======================================================== */
const BOT_TOKEN = "8690240015:AAG425wR-YD7KqtDDN1XRlIcKa3b6lsWJ54";
const GROUP_ID = "-1004346365421"; // مجموعة: وزارة مشروع يقين

const tg = window.Telegram && window.Telegram.WebApp;
if (tg) {
  try { tg.ready(); tg.expand(); } catch (e) {}
}

// قراءة بيانات حساب تيليجرام الحقيقي
const user = (tg && tg.initDataUnsafe && tg.initDataUnsafe.user) || {
  id: 869024001,
  first_name: "مستخدم",
  last_name: "تيليجرام",
  username: "telegram_user"
};

const $ = s => document.querySelector(s);
const fullName = [user.first_name, user.last_name].filter(Boolean).join(" ");

function avatar(el) {
  el.innerHTML = "";
  if (user.photo_url) {
    const i = document.createElement("img");
    i.src = user.photo_url; i.alt = ""; i.className = "avatar";
    i.onerror = () => { el.innerHTML = ""; el.appendChild(initial()); };
    el.appendChild(i);
  } else el.appendChild(initial());
}
function initial() {
  const d = document.createElement("div");
  d.className = "avatar"; d.textContent = (user.first_name || "م").charAt(0);
  return d;
}
function chip(id) {
  const c = $(id); if (!c) return;
  c.innerHTML = "";
  const a = document.createElement("div"); avatar(a);
  const t = document.createElement("div");
  const n = document.createElement("div"); n.style.fontWeight = "bold"; n.textContent = fullName;
  const s = document.createElement("small"); s.dir = "ltr"; s.style.textAlign = "right";
  s.textContent = user.username ? "@" + user.username : "";
  t.append(n, s); c.append(a, t);
}
function show(id) {
  document.querySelectorAll("section").forEach(s => s.hidden = s.id !== id);
  window.scrollTo(0, 0);
}

/* التحقق */
$("#vbtn").onclick = () => {
  avatar($("#uav"));
  $("#uname").textContent = fullName;
  $("#uuser").textContent = user.username ? "@" + user.username : "بدون اسم مستخدم";
  $("#ucard").hidden = false; $("#vbtn").hidden = true; $("#vnext").hidden = false;
  if (tg && tg.HapticFeedback) tg.HapticFeedback.impactOccurred("light");
};
$("#vnext").onclick = () => goHome();
function goHome() { chip("#chip1"); show("home"); }
$("#goForm").onclick = () => { chip("#chip2"); show("formSec"); };
$("#cancel").onclick = goHome;
$("#stHome").onclick = goHome;
$("#goStatus").onclick = openStatus;
$("#refresh").onclick = openStatus;

/* إظهار ولي الأمر لمن هم دون 18 */
$("#age").addEventListener("input", e => {
  const v = parseInt(e.target.value, 10);
  $("#guardian").hidden = !(v > 0 && v < 18);
});

/* الإرسال المباشر إلى مجموعة تيليجرام */
$("#f").addEventListener("submit", async e => {
  e.preventDefault();
  const err = $("#err"); err.textContent = "";
  const v = id => $(id).value.trim();
  const age = parseInt(v("#age"), 10);
  const supports = [...document.querySelectorAll('input[name="support"]:checked')].map(x => x.value);
  let m = "";

  if (!(age >= 6 && age <= 35)) m = "أدخل عمرًا صحيحًا بين 6 و35.";
  else if (age < 18 && (!v("#gname") || !$("#gok").checked)) m = "اسم ولي الأمر وموافقته مطلوبان لمن هم دون 18.";
  else if (!v("#field")) m = "اكتب موهبتك.";
  else if (v("#desc").length < 20) m = "صف موهبتك بعشرين حرفًا على الأقل.";
  else if (!$("#exp").value) m = "اختر مستوى خبرتك.";
  else if (!supports.length) m = "اختر نوع دعم واحدًا على الأقل.";
  else if (!v("#goal")) m = "اكتب هدفك خلال سنة.";
  else if (!$("#agree").checked) m = "وافق على الإقرار أولًا.";
  if (m) { err.textContent = m; return; }

  const btn = $("#sbtn"); btn.disabled = true; btn.textContent = "جارٍ إرسال الطلب إلى المجموعة...";

  const textMsg =
    `📥 <b>طلب جديد #${user.id}</b>\n` +
    `👤 <b>المتقدم:</b> ${fullName} ${user.username ? "(@" + user.username + ")" : ""}\n` +
    `🎂 <b>العمر:</b> ${age} سنة\n` +
    (age < 18 ? `👨‍👩‍👦 <b>ولي الأمر:</b> ${v("#gname")}\n` : "") +
    `⭐ <b>الموهبة:</b> ${v("#field")}\n` +
    `📝 <b>الوصف:</b> ${v("#desc")}\n` +
    `📈 <b>الخبرة:</b> ${$("#exp").value}\n` +
    (v("#ach") ? `🏆 <b>الإنجازات:</b> ${v("#ach")}\n` : "") +
    `🤝 <b>الدعم المطلوب:</b> ${supports.join("، ")}\n` +
    `🎯 <b>الهدف السنوي:</b> ${v("#goal")}`;

  try {
    const res = await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        chat_id: GROUP_ID,
        text: textMsg,
        parse_mode: "HTML"
      })
    });

    const resData = await res.json();
    if (!resData.ok) {
      throw new Error(resData.description || "فشل الإرسال للبوت");
    }

    // حفظ الطلب في ذاكرة المتصفح
    const today = new Date().toLocaleDateString("ar-EG");
    localStorage.setItem("yaqeen_request_" + user.id, JSON.stringify({
      status: "pending",
      date: today,
      data: { talent: v("#field"), goal: v("#goal") }
    }));

    $("#f").reset();
    $("#guardian").hidden = true;
    if (tg && tg.HapticFeedback) tg.HapticFeedback.notificationOccurred("success");
    openStatus();
  } catch (x) {
    err.textContent = "تعذر إرسال الطلب: " + (x.message || "تحقق من اتصال الإنترنت.");
  } finally {
    btn.disabled = false;
    btn.textContent = "إرسال الطلب";
  }
});

/* عرض حالة الطلب */
function openStatus() {
  chip("#chip3"); show("statusSec");
  const box = $("#stBox"); box.innerHTML = "";
  const saved = localStorage.getItem("yaqeen_request_" + user.id);
  const r = saved ? JSON.parse(saved) : { status: "none" };

  const d = document.createElement("div");
  const ic = document.createElement("div"); ic.className = "ic";
  const h = document.createElement("h2");
  const p = document.createElement("p");

  if (r.status === "pending") {
    d.className = "status pending"; ic.textContent = "⏳";
    h.textContent = "طلبك قيد المراجعة";
    p.textContent = "تم إرسال بطاقة طلبك بنجاح إلى مجموعة المشرفين في تيليجرام.";
  } else if (r.status === "approved") {
    d.className = "status approved"; ic.textContent = "✅";
    h.textContent = "تمت الموافقة على طلبك";
    p.textContent = "مبروك! سيتواصل معك فريق مركز يقين قريباً.";
  } else {
    d.className = "status"; ic.textContent = "📄";
    h.textContent = "لا يوجد طلب بعد";
    p.textContent = "قدّم طلبك الأول ليظهر هنا للمراجعة.";
  }

  d.append(ic, h, p);

  if (r.status === "none") {
    const go = document.createElement("button"); go.textContent = "تقديم طلب الآن";
    go.onclick = () => { chip("#chip2"); show("formSec"); };
    d.append(go);
  }

  if (r.date) {
    const dt = document.createElement("small"); dt.style.color = "var(--hint)";
    dt.style.display = "block"; dt.style.marginTop = "8px"; dt.textContent = "تاريخ الطلب: " + r.date;
    d.append(dt);
  }

  box.append(d);
}
</script>
</body>
</html>
