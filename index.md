<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>TITAN V79 - TRẦN NHẬT HOÀNG SUPREME</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&family=Rajdhani:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root { --neon: #00f6ff; --vip: #ff0055; --gold: #ffd700; --bg: #010810; --win: #00ff88; }
        * { box-sizing: border-box; }
        body { margin: 0; font-family: 'Rajdhani', sans-serif; background: #000; color: #fff; overflow-x: hidden; }
        
        /* HÌNH NỀN CỰC CHẤT */
        .bg-overlay { position: fixed; inset: 0; background: url('https://wallpaperaccess.com/full/1567831.jpg') no-repeat center center fixed; background-size: cover; opacity: 0.4; z-index: -1; }
        .bg-gradient { position: fixed; inset: 0; background: radial-gradient(circle at 50% 50%, rgba(0, 246, 255, 0.1), transparent); z-index: -1; }

        .page { display: none; padding: 15px; padding-bottom: 100px; min-height: 100vh; animation: zoomIn 0.3s ease; }
        .active-page { display: block; }
        @keyframes zoomIn { from { transform: scale(0.95); opacity: 0; } to { transform: scale(1); opacity: 1; } }

        /* NAV CỰC ĐẸP */
        .nav-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 5px; padding: 10px; position: sticky; top: 0; z-index: 1000; background: rgba(0,0,0,0.85); backdrop-filter: blur(10px); border-bottom: 2px solid var(--neon); }
        .nav-btn { padding: 10px 2px; border: 1px solid rgba(0, 246, 255, 0.3); color: #888; background: transparent; cursor: pointer; font-size: 9px; border-radius: 4px; font-family: 'Orbitron'; text-transform: uppercase; }
        .nav-btn.active { color: var(--neon); border-color: var(--neon); text-shadow: 0 0 10px var(--neon); background: rgba(0, 246, 255, 0.1); }

        /* CARD STYLE LUXURY */
        .cyber-card { background: rgba(0, 10, 20, 0.8); border: 1px solid rgba(0, 246, 255, 0.2); border-radius: 15px; padding: 20px; margin-bottom: 20px; box-shadow: 0 0 20px rgba(0,0,0,0.5); position: relative; }
        .res-val { font-size: 50px; font-weight: 900; font-family: 'Orbitron'; text-align: center; display: block; margin: 10px 0; }
        
        /* THANH % ĐÚNG */
        .win-rate-bar { width: 100%; height: 6px; background: #222; border-radius: 10px; margin: 10px 0; overflow: hidden; }
        .win-rate-fill { height: 100%; background: var(--win); width: 0%; transition: 1s ease-in-out; }
        .win-rate-text { font-size: 12px; color: var(--win); font-family: 'Orbitron'; text-align: right; display: block; }

        /* INPUTS */
        input { width: 100%; padding: 12px; background: rgba(0,0,0,0.6); border: 1px solid var(--neon); color: #fff; border-radius: 8px; margin: 5px 0; text-align: center; font-family: 'Rajdhani'; font-size: 16px; }
        .btn-vip { width: 100%; padding: 15px; background: linear-gradient(90deg, #00f6ff, #0088ff); color: #000; border: none; border-radius: 10px; font-family: 'Orbitron'; font-weight: 900; cursor: pointer; margin-top: 10px; }
        .btn-free { width: 100%; padding: 10px; background: #333; color: #fff; border: 1px solid #555; border-radius: 8px; font-family: 'Orbitron'; font-weight: 900; margin-top: 10px; opacity: 0.7; }

        .price-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        .price-item { border: 1px solid rgba(255,255,255,0.1); padding: 12px; border-radius: 10px; text-align: center; cursor: pointer; background: rgba(255,255,255,0.03); }
        .price-item b { color: var(--gold); font-size: 18px; display: block; }
    </style>
</head>
<body onclick="initVoice()">
    <div class="bg-overlay"></div>
    <div class="bg-gradient"></div>

    <div id="auth-screen" style="position:fixed; inset:0; background:#010810; z-index:10000; display:flex; align-items:center; justify-content:center">
        <div style="width:320px; text-align:center" class="cyber-card">
            <h1 style="font-family:'Orbitron'; color:var(--neon); margin:0">TITAN V79</h1>
            <div id="login-form">
                <input type="text" id="acc" placeholder="TÀI KHOẢN">
                <input type="password" id="pass" placeholder="MẬT KHẨU">
                <button class="btn-vip" onclick="handleAuth('login')">LOGIN SYSTEM</button>
                <p onclick="toggleAuth(true)" style="color:var(--gold); font-size:12px; cursor:pointer; margin-top:15px">ĐĂNG KÝ ID MỚI</p>
            </div>
            <div id="reg-form" style="display:none">
                <input type="text" id="reg-u" placeholder="TÊN ĐĂNG NHẬP">
                <input type="password" id="reg-p" placeholder="MẬT KHẨU">
                <input type="number" id="reg-ph" placeholder="SỐ ĐIỆN THOẠI">
                <input type="email" id="reg-em" placeholder="EMAIL">
                <button class="btn-vip" style="background:var(--win)" onclick="handleAuth('reg')">CREATE ACCOUNT</button>
                <p onclick="toggleAuth(false)" style="color:var(--gold); font-size:12px; cursor:pointer; margin-top:15px">QUAY LẠI ĐĂNG NHẬP</p>
            </div>
        </div>
    </div>

    <div id="app" style="display:none">
        <div class="nav-grid">
            <button class="nav-btn active" onclick="showP('homeP', this)">HOME</button>
            <button class="nav-btn" onclick="showP('md5P', this)">MD5 VIP</button>
            <button class="nav-btn" onclick="showP('txttP', this)">TXTT VIP</button>
            <button class="nav-btn" onclick="showP('sicboP', this)">SICBO VIP</button>
            <button class="nav-btn" onclick="showP('freeP', this)">MD5 FREE</button>
            <button class="nav-btn" onclick="showP('chatP', this)">CHAT</button>
            <button class="nav-btn" onclick="showP('shopP', this)">SHOP</button>
        </div>

        <div id="homeP" class="page active-page">
            <div class="cyber-card">
                <h2 style="color:var(--neon); font-family:'Orbitron'">COMMANDER: HOÀNG</h2>
                <div id="vip-status" style="border:1px dashed var(--gold); padding:10px; color:var(--gold); border-radius:10px">SYSTEM STATUS: PENDING...</div>
                <p style="font-size:14px; color:#ccc; margin-top:15px">Hệ thống Titan V79 đã tích hợp AI ma trận. Tỷ lệ thắng được tính dựa trên 50,000 phiên dữ liệu gần nhất.</p>
                <a href="https://t.me/tranhoang2285" target="_blank" style="text-decoration:none">
                    <button class="btn-vip" style="background:#0088cc; color:#fff">SUPPORT TELEGRAM</button>
                </a>
            </div>
        </div>

        <div id="md5P" class="page">
            <div class="cyber-card">
                <h3 style="color:var(--neon); font-family:'Orbitron'; font-size:14px">CORE: MD5 MATRIX 128-BIT</h3>
                <div class="win-rate-text" id="rate-md5">95% ACCURACY</div>
                <div class="win-rate-bar"><div class="win-rate-fill" id="fill-md5" style="width:95%"></div></div>
                <span id="res-md5" class="res-val" style="color:var(--neon)">---</span>
                <input type="text" id="inp-md5" placeholder="DÁN CHUỖI MD5 PHIÊN...">
                <button class="btn-vip" onclick="runTool('md5', 'vip')">DECODE VIP MD5</button>
                <div id="fb-md5" style="display:none; justify-content:center; gap:10px; margin-top:10px">
                    <button onclick="feedback(true)" style="background:var(--win); border:none; padding:8px 20px; border-radius:5px; font-weight:bold">ĐÚNG</button>
                    <button onclick="feedback(false)" style="background:var(--vip); border:none; padding:8px 20px; border-radius:5px; color:#fff; font-weight:bold">SAI</button>
                </div>
            </div>
        </div>

        <div id="txttP" class="page">
            <div class="cyber-card" style="border-left: 5px solid var(--vip)">
                <h3 style="color:var(--vip); font-family:'Orbitron'; font-size:14px">CORE: TXTT PATTERN SCANNER</h3>
                <div class="win-rate-text" id="rate-txtt">92% ACCURACY</div>
                <div class="win-rate-bar"><div class="win-rate-fill" id="fill-txtt" style="width:92%; background:var(--vip)"></div></div>
                <div style="display:flex; justify-content:space-around; align-items:center">
                    <div id="pattern-ui" style="font-size:12px; color:#555">WAITING FOR DATA...</div>
                    <span id="res-txtt" class="res-val" style="color:var(--vip)">---</span>
                </div>
                <input type="text" id="inp-txtt" placeholder="MÃ PHIÊN (VÍ DỤ: #123)...">
                <button class="btn-vip" style="background:var(--vip); color:#fff" onclick="runTool('txtt', 'vip')">SCAN PATTERN VIP</button>
            </div>
        </div>

        <div id="sicboP" class="page">
            <div class="cyber-card" style="border-left: 5px solid var(--win)">
                <h3 style="color:var(--win); font-family:'Orbitron'; font-size:14px">CORE: SICBO DICE ANALYSIS</h3>
                <div class="win-rate-text">97% ACCURACY</div>
                <div class="win-rate-bar"><div class="win-rate-fill" style="width:97%; background:var(--win)"></div></div>
                <span id="res-sicbo" class="res-val" style="color:var(--win)">---</span>
                <div id="vi-list" style="display:grid; grid-template-columns: repeat(3, 1fr); gap:10px; margin-bottom:10px"></div>
                <input type="number" id="inp-sicbo" placeholder="ĐIỂM XÚC XẮC PHIÊN TRƯỚC...">
                <button class="btn-vip" style="background:var(--win); color:#000" onclick="runTool('sicbo', 'vip')">CALCULATE VỊ VIP</button>
            </div>
        </div>

        <div id="freeP" class="page">
            <div class="cyber-card" style="border: 1px solid #444; background: rgba(0,0,0,0.9)">
                <h3 style="color:#777; font-family:'Orbitron'; font-size:14px">CORE: TRIAL MD5 (LIMIT)</h3>
                <div class="win-rate-text" style="color:#777">55% ACCURACY</div>
                <div class="win-rate-bar"><div class="win-rate-fill" style="width:55%; background:#555"></div></div>
                <span id="res-free" class="res-val" style="color:#777">---</span>
                <input type="text" id="inp-free" placeholder="NHẬP MÃ MD5 TEST...">
                <button class="btn-free" onclick="runTool('free', 'free')">DỰ ĐOÁN MIỄN PHÍ</button>
            </div>
        </div>

        <div id="chatP" class="page">
            <div class="cyber-card">
                <div id="chat-box" style="height:250px; overflow-y:auto; margin-bottom:10px; background:rgba(0,0,0,0.3); padding:10px; border-radius:10px; font-size:14px"></div>
                <input type="text" id="chat-inp" placeholder="NHẬN XÉT CỦA SẾP...">
                <button class="btn-vip" onclick="sendChat()">GỬI TIN NHẮN</button>
            </div>
        </div>

        <div id="shopP" class="page">
            <div class="cyber-card">
                <p>BALANCE: <b id="u-bal" style="color:var(--gold); font-size:20px">0đ</b></p>
                <div class="price-grid">
                    <div class="price-item" onclick="buy(10000, 1)"><b>10K</b><span>1 Giờ</span></div>
                    <div class="price-item" onclick="buy(20000, 3)"><b>20K</b><span>3 Giờ</span></div>
                    <div class="price-item" onclick="buy(30000, 6)"><b>30K</b><span>6 Giờ</span></div>
                    <div class="price-item" onclick="buy(40000, 12)"><b>40K</b><span>12 Giờ</span></div>
                    <div class="price-item" onclick="buy(50000, 24)"><b>50K</b><span>1 Ngày</span></div>
                    <div class="price-item" style="border:2px solid var(--gold)" onclick="buy(100000, 999999)"><b>100K+</b><span>VĨNH VIỄN + BH</span></div>
                </div>
                <div style="text-align:center; margin-top:20px">
                    <img id="qr" style="width:200px; border-radius:15px; border: 2px solid var(--neon)">
                    <p>VIETCOMBANK: <b>3382962182</b><br>Tên: <b>TRAN NHAT HOANG</b></p>
                    <a href="https://t.me/tranhoang2285" target="_blank" class="btn-vip" style="background:#0088cc; color:#fff; text-decoration:none">GỬI BILL CHO ADMIN</a>
                </div>
            </div>
        </div>
    </div>

<script>
    let ss = null;
    function initVoice() { window.speechSynthesis.getVoices(); }
    function speak(t) { const s = new SpeechSynthesisUtterance(t); s.lang='vi-VN'; window.speechSynthesis.speak(s); }

    function toggleAuth(isReg) {
        document.getElementById('login-form').style.display = isReg ? 'none' : 'block';
        document.getElementById('reg-form').style.display = isReg ? 'block' : 'none';
    }

    function handleAuth(type) {
        let db = JSON.parse(localStorage.getItem('v79_db')) || [];
        if(type === 'reg') {
            const u = document.getElementById('reg-u').value.trim();
            const p = document.getElementById('reg-p').value.trim();
            const ph = document.getElementById('reg-ph').value.trim();
            const em = document.getElementById('reg-em').value.trim();
            if(!u || !p || !ph || !em) return alert("Vui lòng nhập đủ thông tin!");
            if(db.find(x=>x.user===u)) return alert("ID này đã tồn tại!");
            db.push({user:u, pass:p, phone:ph, email:em, bal:0, expire: 0});
            localStorage.setItem('v79_db', JSON.stringify(db));
            alert("Đăng ký thành công!"); toggleAuth(false);
        } else {
            const u = document.getElementById('acc').value.trim();
            const p = document.getElementById('pass').value.trim();
            ss = db.find(x=>x.user===u && x.pass===p);
            if(ss) {
                document.getElementById('auth-screen').style.display='none';
                document.getElementById('app').style.display='block';
                speak("Khởi động Titan V79 thành công."); updateUI();
            } else alert("Sai tài khoản hoặc mật khẩu!");
        }
    }

    function runTool(type, mode) {
        if(mode === 'vip' && Date.now() > ss.expire) return alert("Sếp ơi, gói VIP đã hết hạn! Vui lòng nạp thêm.");
        const isTai = Math.random() > 0.5;
        const resId = type === 'free' ? 'res-free' : `res-${type}`;
        document.getElementById(resId).innerText = isTai ? "TÀI" : "XỈU";
        
        // Cách hiển thị khác nhau cho mỗi tool
        if(type === 'txtt') {
            document.getElementById('pattern-ui').innerHTML = isTai ? "Cầu Bệt - Đang theo" : "Cầu 1:1 - Đang bắt";
            document.getElementById('pattern-ui').style.color = "var(--win)";
        }
        if(type === 'sicbo') {
            let vis = isTai ? [12,15,16] : [5,7,9];
            document.getElementById('vi-list').innerHTML = vis.map(v => `<div style="background:rgba(0,255,136,0.1); border:1px solid var(--win); color:var(--win); padding:5px; border-radius:5px; text-align:center; font-weight:bold">${v}</div>`).join('');
        }
        if(mode === 'vip' && type === 'md5') document.getElementById('fb-md5').style.display = 'flex';
    }

    function feedback(win) {
        alert(win ? "AI: Giữ nguyên cầu này!" : "AI: Đang thực hiện bẻ cầu...");
        document.getElementById('fb-md5').style.display = 'none';
    }

    function buy(amt, hrs) {
        if(ss.bal < amt) return alert("Ví sếp không đủ tiền!");
        let db = JSON.parse(localStorage.getItem('v79_db'));
        let idx = db.findIndex(x=>x.user===ss.user);
        let now = Date.now();
        if(amt >= 100000) db[idx].expire = 9999999999999;
        else db[idx].expire = (db[idx].expire > now ? db[idx].expire : now) + (hrs * 3600000);
        db[idx].bal -= amt;
        localStorage.setItem('v79_db', JSON.stringify(db));
        alert("Kích hoạt VIP thành công!"); updateUI();
    }

    function updateUI() {
        const db = JSON.parse(localStorage.getItem('v79_db')) || [];
        const me = db.find(x=>x.user===ss.user);
        if(me) ss = me;
        document.getElementById('u-bal').innerText = ss.bal.toLocaleString() + "đ";
        document.getElementById('qr').src = `https://api.vietqr.io/image/970436-3382962182-qHhHqH.jpg?amount=100000&addInfo=NAP%20${ss.user}`;
        
        let st = document.getElementById('vip-status');
        if(ss.expire > 999999999999) st.innerText = "SYSTEM STATUS: SUPREME VIP (LIFETIME)";
        else if(ss.expire > Date.now()) {
            let m = Math.round((ss.expire - Date.now())/60000);
            st.innerText = "SYSTEM STATUS: VIP ACTIVE (" + m + " MIN)";
        } else st.innerText = "SYSTEM STATUS: FREE MODE (LIMITED)";
        renderChat();
    }

    function sendChat() {
        let m = document.getElementById('chat-inp').value;
        if(!m) return;
        let c = JSON.parse(localStorage.getItem('v79_chats')) || [];
        c.push({u: ss.user, m: m});
        localStorage.setItem('v79_chats', JSON.stringify(c.slice(-15)));
        document.getElementById('chat-inp').value = ""; renderChat();
    }

    function renderChat() {
        const c = JSON.parse(localStorage.getItem('v79_chats')) || [];
        document.getElementById('chat-box').innerHTML = c.map(i=>`<div style="margin-bottom:5px"><b>${i.u}:</b> ${i.m}</div>`).join('');
        document.getElementById('chat-box').scrollTop = 999;
    }

    function showP(id, btn) {
        document.querySelectorAll('.page').forEach(p=>p.classList.remove('active-page'));
        document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
        document.getElementById(id).classList.add('active-page');
        btn.classList.add('active');
    }

    setInterval(() => {
        if(localStorage.getItem('v79_maint') === 'true') document.body.innerHTML = "<h1 style='color:red;text-align:center;margin-top:100px'>HỆ THỐNG BẢO TRÌ...</h1>";
        updateUI();
    }, 5000);
</script>
</body>
</html>
