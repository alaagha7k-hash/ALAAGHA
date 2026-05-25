<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>آغاتي — نقودك في جيبك</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;900&display=swap" rel="stylesheet">

<style>
  :root {
    --gold: #CFAF4A;
    --gold-light: #E8C96A;
    --gold-dark: #A88A30;
    --black: #000000;
    --dark: #0A0A0A;
    --dark2: #111111;
    --dark3: #1A1A1A;
    --white: #FFFFFF;
    --gray: #888888;
    --error: #FF4444;
    --success: #44BB77;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Tajawal', sans-serif;
    background: var(--black);
    color: var(--white);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── Background ── */
  .bg {
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 80% 50% at 50% -20%, rgba(207,175,74,0.15) 0%, transparent 60%),
      radial-gradient(ellipse 60% 40% at 80% 80%, rgba(207,175,74,0.08) 0%, transparent 50%),
      var(--black);
    z-index: 0;
  }

  .bg::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23CFAF4A' fill-opacity='0.03'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
    z-index: 0;
    pointer-events: none;
  }

  /* ── Pages ── */
  .page {
    position: relative;
    z-index: 1;
    min-height: 100vh;
    display: none;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 24px 20px;
  }
  .page.active { display: flex; }

  /* ── Logo ── */
  .logo-wrap {
    text-align: center;
    margin-bottom: 40px;
    animation: fadeDown 0.8s ease both;
  }

  .logo-circle {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--gold), var(--gold-dark));
    margin: 0 auto 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 32px;
    box-shadow: 0 0 40px rgba(207,175,74,0.4);
  }

  .logo-title {
    font-size: 32px;
    font-weight: 900;
    letter-spacing: 3px;
    background: linear-gradient(135deg, var(--gold-light), var(--gold));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .logo-sub {
    font-size: 14px;
    color: var(--gray);
    margin-top: 6px;
    font-weight: 300;
  }

  /* ── Card ── */
  .card {
    width: 100%;
    max-width: 400px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(207,175,74,0.2);
    border-radius: 24px;
    padding: 32px 24px;
    backdrop-filter: blur(20px);
    animation: fadeUp 0.8s ease 0.2s both;
  }

  .card-title {
    font-size: 22px;
    font-weight: 700;
    text-align: center;
    margin-bottom: 28px;
    color: var(--white);
  }

  /* ── Inputs ── */
  .field {
    margin-bottom: 16px;
  }

  .field label {
    display: block;
    font-size: 13px;
    color: var(--gray);
    margin-bottom: 8px;
    font-weight: 500;
  }

  .field input {
    width: 100%;
    padding: 14px 16px;
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 12px;
    color: var(--white);
    font-family: 'Tajawal', sans-serif;
    font-size: 15px;
    outline: none;
    transition: border-color 0.3s, box-shadow 0.3s;
    direction: ltr;
    text-align: right;
  }

  .field input:focus {
    border-color: var(--gold);
    box-shadow: 0 0 0 3px rgba(207,175,74,0.15);
  }

  .field input.error {
    border-color: var(--error);
  }

  .field-error {
    font-size: 12px;
    color: var(--error);
    margin-top: 6px;
    display: none;
  }

  .field-error.show { display: block; }

  /* ── Button ── */
  .btn {
    width: 100%;
    padding: 16px;
    border: none;
    border-radius: 12px;
    font-family: 'Tajawal', sans-serif;
    font-size: 17px;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.3s;
    margin-top: 8px;
  }

  .btn-gold {
    background: linear-gradient(135deg, var(--gold-light), var(--gold));
    color: var(--black);
  }

  .btn-gold:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(207,175,74,0.4); }
  .btn-gold:active { transform: translateY(0); }
  .btn-gold:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }

  .btn-ghost {
    background: transparent;
    color: var(--gold);
    border: 1px solid rgba(207,175,74,0.3);
    margin-top: 12px;
  }

  .btn-ghost:hover { background: rgba(207,175,74,0.1); }

  /* ── Spinner ── */
  .spinner {
    width: 20px; height: 20px;
    border: 2px solid rgba(0,0,0,0.3);
    border-top-color: var(--black);
    border-radius: 50%;
    animation: spin 0.7s linear infinite;
    display: inline-block;
    vertical-align: middle;
  }

  /* ── Toast ── */
  .toast {
    position: fixed;
    bottom: 32px;
    left: 50%;
    transform: translateX(-50%) translateY(100px);
    background: var(--dark2);
    border: 1px solid rgba(207,175,74,0.3);
    border-radius: 12px;
    padding: 14px 24px;
    font-size: 14px;
    z-index: 999;
    transition: transform 0.4s ease;
    white-space: nowrap;
    max-width: 90vw;
    text-align: center;
  }
  .toast.show { transform: translateX(-50%) translateY(0); }
  .toast.error { border-color: var(--error); color: var(--error); }
  .toast.success { border-color: var(--success); color: var(--success); }

  /* ── Divider ── */
  .divider {
    text-align: center;
    color: var(--gray);
    font-size: 13px;
    margin: 20px 0;
    position: relative;
  }
  .divider::before, .divider::after {
    content: '';
    position: absolute;
    top: 50%;
    width: 35%;
    height: 1px;
    background: rgba(255,255,255,0.1);
  }
  .divider::before { right: 0; }
  .divider::after { left: 0; }

  /* ── Home Page ── */
  .home-header {
    width: 100%;
    max-width: 500px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 32px;
    animation: fadeDown 0.6s ease both;
  }

  .home-greeting {
    font-size: 13px;
    color: var(--gray);
  }

  .home-name {
    font-size: 20px;
    font-weight: 700;
    color: var(--gold);
  }

  .logout-btn {
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(255,255,255,0.1);
    color: var(--gray);
    padding: 8px 16px;
    border-radius: 10px;
    cursor: pointer;
    font-family: 'Tajawal', sans-serif;
    font-size: 13px;
    transition: all 0.3s;
  }
  .logout-btn:hover { border-color: var(--error); color: var(--error); }

  .home-card {
    width: 100%;
    max-width: 500px;
    background: linear-gradient(135deg, rgba(207,175,74,0.15), rgba(207,175,74,0.05));
    border: 1px solid rgba(207,175,74,0.3);
    border-radius: 24px;
    padding: 32px;
    text-align: center;
    animation: fadeUp 0.6s ease 0.2s both;
  }

  .home-icon {
    font-size: 48px;
    margin-bottom: 16px;
  }

  .home-title {
    font-size: 24px;
    font-weight: 700;
    color: var(--gold);
    margin-bottom: 8px;
  }

  .home-desc {
    color: var(--gray);
    font-size: 14px;
    line-height: 1.6;
  }

  .home-email {
    margin-top: 16px;
    font-size: 13px;
    color: rgba(255,255,255,0.4);
    direction: ltr;
  }

  /* ── Forgot password link ── */
  .forgot-link {
    text-align: left;
    margin-top: 4px;
  }
  .forgot-link a {
    color: var(--gold);
    font-size: 13px;
    text-decoration: none;
    cursor: pointer;
  }

  /* ── Animations ── */
  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
</style>
</head>
<body>

<div class="bg"></div>

<!-- ── SPLASH ── -->
<div class="page active" id="splash">
  <div class="logo-wrap">
    <div class="logo-circle">👑</div>
    <div class="logo-title">AAGHaTi</div>
    <div class="logo-sub">نقودك في جيبك</div>
  </div>
  <div style="margin-top:20px">
    <div class="spinner" style="border-top-color:var(--gold); border-color:rgba(207,175,74,0.2)"></div>
  </div>
</div>

<!-- ── LOGIN ── -->
<div class="page" id="login">
  <div class="logo-wrap">
    <div class="logo-circle">👑</div>
    <div class="logo-title">AAGHaTi</div>
    <div class="logo-sub">نقودك في جيبك</div>
  </div>

  <div class="card">
    <div class="card-title">تسجيل الدخول</div>

    <div class="field">
      <label>البريد الإلكتروني</label>
      <input type="email" id="login-email" placeholder="example@email.com">
      <div class="field-error" id="login-email-err">بريد إلكتروني غير صحيح</div>
    </div>

    <div class="field">
      <label>كلمة المرور</label>
      <input type="password" id="login-pass" placeholder="••••••••">
      <div class="field-error" id="login-pass-err">كلمة المرور 6 أحرف على الأقل</div>
    </div>

    <div class="forgot-link">
      <a onclick="showForgot()">نسيت كلمة المرور؟</a>
    </div>

    <button class="btn btn-gold" id="login-btn" onclick="doLogin()">دخول</button>
    <button class="btn btn-ghost" onclick="showPage('register')">ليس لديك حساب؟ سجّل الآن</button>
  </div>
</div>

<!-- ── REGISTER ── -->
<div class="page" id="register">
  <div class="logo-wrap" style="margin-bottom:24px">
    <div class="logo-title" style="font-size:24px">إنشاء حساب</div>
  </div>

  <div class="card">
    <div class="card-title">مرحباً بك في آغاتي</div>

    <div class="field">
      <label>الاسم الكامل</label>
      <input type="text" id="reg-name" placeholder="محمد العلي" style="text-align:right; direction:rtl">
      <div class="field-error" id="reg-name-err">أدخل اسمك</div>
    </div>

    <div class="field">
      <label>البريد الإلكتروني</label>
      <input type="email" id="reg-email" placeholder="example@email.com">
      <div class="field-error" id="reg-email-err">بريد إلكتروني غير صحيح</div>
    </div>

    <div class="field">
      <label>كلمة المرور</label>
      <input type="password" id="reg-pass" placeholder="••••••••">
      <div class="field-error" id="reg-pass-err">كلمة المرور 6 أحرف على الأقل</div>
    </div>

    <div class="field">
      <label>تأكيد كلمة المرور</label>
      <input type="password" id="reg-confirm" placeholder="••••••••">
      <div class="field-error" id="reg-confirm-err">كلمتا المرور غير متطابقتين</div>
    </div>

    <button class="btn btn-gold" id="reg-btn" onclick="doRegister()">إنشاء الحساب</button>
    <button class="btn btn-ghost" onclick="showPage('login')">لديك حساب؟ سجّل دخولك</button>
  </div>
</div>

<!-- ── HOME ── -->
<div class="page" id="home">
  <div class="home-header">
    <div>
      <div class="home-greeting">أهلاً وسهلاً،</div>
      <div class="home-name" id="home-name">—</div>
    </div>
    <button class="logout-btn" onclick="doLogout()">خروج</button>
  </div>

  <div class="home-card">
    <div class="home-icon">👑</div>
    <div class="home-title">AAGHaTi</div>
    <div class="home-desc">المنصة الملكية لإدارة أموالك بذكاء وأناقة</div>
    <div class="home-email" id="home-email"></div>
  </div>
</div>

<!-- ── TOAST ── -->
<div class="toast" id="toast"></div>

<!-- ── Firebase ── -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.14.0/firebase-app.js";
import {
  getAuth,
  signInWithEmailAndPassword,
  createUserWithEmailAndPassword,
  sendPasswordResetEmail,
  updateProfile,
  onAuthStateChanged,
  signOut
} from "https://www.gstatic.com/firebasejs/10.14.0/firebase-auth.js";
import {
  getFirestore,
  doc,
  setDoc,
  getDoc,
  serverTimestamp
} from "https://www.gstatic.com/firebasejs/10.14.0/firebase-firestore.js";

// ── Firebase Config ── نسخ من Firebase Console
const firebaseConfig = {
  apiKey: "AIzaSyC901AbRcfp8APr6Xld7ldsm_q8BQyA6yk",
  authDomain: "project-f074d8d3-d5aa-40ec-ae0.firebaseapp.com",
  projectId: "project-f074d8d3-d5aa-40ec-ae0",
  storageBucket: "project-f074d8d3-d5aa-40ec-ae0.firebasestorage.app",
  messagingSenderId: "120124606674",
  appId: "1:120124606674:android:4f74674a1d1aab60f1450b"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

// ── Auth State ──
onAuthStateChanged(auth, async (user) => {
  if (user) {
    // Load name from Firestore
    try {
      const snap = await getDoc(doc(db, 'users', user.uid));
      const name = snap.exists() ? snap.data().name : user.displayName || 'مستخدم';
      document.getElementById('home-name').textContent = name;
      document.getElementById('home-email').textContent = user.email;
    } catch(e) {
      document.getElementById('home-name').textContent = user.displayName || 'مستخدم';
    }
    showPage('home');
  } else {
    showPage('login');
  }
});

// ── Login ──
window.doLogin = async () => {
  const email = document.getElementById('login-email').value.trim();
  const pass = document.getElementById('login-pass').value;
  let valid = true;

  clearErrors(['login-email-err', 'login-pass-err']);

  if (!validateEmail(email)) {
    showError('login-email-err', 'login-email'); valid = false;
  }
  if (pass.length < 6) {
    showError('login-pass-err', 'login-pass'); valid = false;
  }
  if (!valid) return;

  setLoading('login-btn', true);
  try {
    await signInWithEmailAndPassword(auth, email, pass);
  } catch(e) {
    showToast(mapError(e.code), 'error');
  } finally {
    setLoading('login-btn', false);
  }
};

// ── Register ──
window.doRegister = async () => {
  const name = document.getElementById('reg-name').value.trim();
  const email = document.getElementById('reg-email').value.trim();
  const pass = document.getElementById('reg-pass').value;
  const confirm = document.getElementById('reg-confirm').value;
  let valid = true;

  clearErrors(['reg-name-err','reg-email-err','reg-pass-err','reg-confirm-err']);

  if (name.length < 2) { showError('reg-name-err','reg-name'); valid = false; }
  if (!validateEmail(email)) { showError('reg-email-err','reg-email'); valid = false; }
  if (pass.length < 6) { showError('reg-pass-err','reg-pass'); valid = false; }
  if (pass !== confirm) { showError('reg-confirm-err','reg-confirm'); valid = false; }
  if (!valid) return;

  setLoading('reg-btn', true);
  try {
    const cred = await createUserWithEmailAndPassword(auth, email, pass);
    await updateProfile(cred.user, { displayName: name });
    await setDoc(doc(db, 'users', cred.user.uid), {
      name, email, createdAt: serverTimestamp()
    });
    showToast('تم إنشاء الحساب بنجاح 🎉', 'success');
  } catch(e) {
    showToast(mapError(e.code), 'error');
  } finally {
    setLoading('reg-btn', false);
  }
};

// ── Forgot Password ──
window.showForgot = async () => {
  const email = document.getElementById('login-email').value.trim();
  if (!validateEmail(email)) {
    showToast('أدخل بريدك الإلكتروني أولاً', 'error');
    return;
  }
  try {
    await sendPasswordResetEmail(auth, email);
    showToast('تم إرسال رابط إعادة التعيين ✉️', 'success');
  } catch(e) {
    showToast(mapError(e.code), 'error');
  }
};

// ── Logout ──
window.doLogout = async () => {
  await signOut(auth);
};

// ── Helpers ──
window.showPage = (id) => {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
};

function validateEmail(e) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(e);
}

function showError(errId, inputId) {
  document.getElementById(errId).classList.add('show');
  document.getElementById(inputId).classList.add('error');
}

function clearErrors(ids) {
  ids.forEach(id => {
    document.getElementById(id).classList.remove('show');
  });
  document.querySelectorAll('input').forEach(i => i.classList.remove('error'));
}

function setLoading(btnId, loading) {
  const btn = document.getElementById(btnId);
  btn.disabled = loading;
  btn.innerHTML = loading
    ? '<span class="spinner"></span>'
    : btn.id === 'login-btn' ? 'دخول' : 'إنشاء الحساب';
}

let toastTimer;
window.showToast = (msg, type='') => {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = `toast show ${type}`;
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => t.classList.remove('show'), 3500);
};

function mapError(code) {
  const map = {
    'auth/email-already-in-use': 'البريد مستخدم مسبقاً',
    'auth/invalid-email': 'البريد الإلكتروني غير صحيح',
    'auth/weak-password': 'كلمة المرور ضعيفة',
    'auth/user-not-found': 'البريد أو كلمة المرور غير صحيحة',
    'auth/wrong-password': 'البريد أو كلمة المرور غير صحيحة',
    'auth/invalid-credential': 'البريد أو كلمة المرور غير صحيحة',
    'auth/too-many-requests': 'محاولات كثيرة، حاول لاحقاً',
    'auth/network-request-failed': 'تعذّر الاتصال بالإنترنت',
  };
  return map[code] || 'حدث خطأ، حاول مرة أخرى';
}

// Enter key support
document.addEventListener('keydown', e => {
  if (e.key === 'Enter') {
    const active = document.querySelector('.page.active');
    if (active.id === 'login') doLogin();
    if (active.id === 'register') doRegister();
  }
});
</script>
</body>
</html>

          curl -X POST \
            "https://api.render.com/v1/services/${{ secrets.RENDER_ADS_SERVICE_ID }}/deploys" \
            -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
            -H "Content-Type: application/json" \
            -d '{}'

      - name: ✅ Confirm Deploy
        run: echo "✅ Ads Website deployment triggered!"

  # ============================
  # 👑 نشر الموقع الإمبراطوري
  # ============================
  deploy-imperial:
    name: 👑 Deploy Imperial Website
    runs-on: ubuntu-latest
    if: |
      contains(github.event.head_commit.modified, 'aghati-imperial-website/')
    steps:
      - name: 🚀 Trigger Render Deploy
        run: |
          curl -X POST \
            "https://api.render.com/v1/services/${{ secrets.RENDER_IMPERIAL_SERVICE_ID }}/deploys" \
            -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
            -H "Content-Type: application/json" \
            -d '{}'

      - name: ✅ Confirm Deploy
        run: echo "✅ Imperial Website deployment triggered!"

  # ============================
  # 🎯 نشر موقع Skill
  # ============================
  deploy-skill:
    name: 🎯 Deploy Skill Website
    runs-on: ubuntu-latest
    if: |
      contains(github.event.head_commit.modified, 'aghati-skill-website/')
    steps:
      - name: 🚀 Trigger Render Deploy
        run: |
          curl -X POST \
            "https://api.render.com/v1/services/${{ secrets.RENDER_SKILL_SERVICE_ID }}/deploys" \
            -H "Authorization: Bearer ${{ secrets.RENDER_API_KEY }}" \
            -H "Content-Type: application/json" \
            -d '{}'

      - name: ✅ Confirm Deploy
        run: echo "✅ Skill Website deployment triggered!"

  # ============================
  # 📊 تقرير النشر
  # ============================
  notify:
    name: 📊 Deploy Report
    runs-on: ubuntu-latest
    needs: [deploy-main, deploy-ads, deploy-imperial, deploy-skill]
    if: always()
    steps:
      - name: 📊 Report
        run: |
          echo "================================"
          echo "🎨 ALAAGHA Deploy Report"
          echo "================================"
          echo "🔐 Main:     ${{ needs.deploy-main.result }}"
          echo "📢 Ads:      ${{ needs.deploy-ads.result }}"
          echo "👑 Imperial: ${{ needs.deploy-imperial.result }}"
          echo "🎯 Skill:    ${{ needs.deploy-skill.result }}"
          echo "================================"


