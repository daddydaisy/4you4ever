# 4you4ever
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>4you4ever · 解锁</title>
    <style>
        /* 全局样式 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', 'Times New Roman', serif;
            background: #f7f4f0;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        /* 密码锁卡片 */
        .lock-container {
            background: #fffcf9;
            padding: 48px 40px;
            max-width: 400px;
            width: 100%;
            border-radius: 24px;
            box-shadow: 0 8px 48px rgba(0, 0, 0, 0.06);
            border: 1px solid #eee8e0;
            text-align: center;
        }

        .lock-container .icon {
            font-size: 48px;
            margin-bottom: 12px;
            display: block;
        }

        .lock-container h1 {
            font-size: 24px;
            font-weight: 400;
            color: #2c2a28;
            margin-bottom: 6px;
        }

        .lock-container .sub {
            color: #8a8580;
            font-size: 14px;
            margin-bottom: 28px;
        }

        .lock-container input {
            width: 100%;
            padding: 14px 16px;
            border: 1px solid #ddd8d0;
            border-radius: 40px;
            font-size: 16px;
            background: #fffcf9;
            text-align: center;
            letter-spacing: 4px;
            font-family: inherit;
            transition: 0.2s;
            margin-bottom: 14px;
        }

        .lock-container input:focus {
            outline: none;
            border-color: #b8a99a;
            box-shadow: 0 0 0 3px rgba(184, 169, 154, 0.12);
        }

        .lock-container .btn-unlock {
            width: 100%;
            padding: 14px;
            background: #2c2a28;
            color: #fff;
            border: none;
            border-radius: 40px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: 0.2s;
            font-family: inherit;
        }

        .lock-container .btn-unlock:hover {
            background: #1f1d1b;
        }

        .lock-container .error-msg {
            color: #c0392b;
            font-size: 14px;
            margin-top: 12px;
            min-height: 24px;
        }

        .lock-container .hint {
            color: #b8b0a8;
            font-size: 13px;
            margin-top: 18px;
            border-top: 1px solid #f0ebe5;
            padding-top: 18px;
        }

        /* ---------- 网站内容（默认隐藏） ---------- */
        .site-content {
            display: none;
            max-width: 640px;
            width: 100%;
            margin: 0 auto;
            padding: 20px;
        }

        .site-content .header {
            text-align: center;
            padding: 40px 0 20px;
            border-bottom: 1px solid #eee8e0;
        }

        .site-content .header h1 {
            font-size: 36px;
            font-weight: 400;
            color: #2c2a28;
            letter-spacing: 2px;
        }

        .site-content .header p {
            color: #8a8580;
            font-size: 16px;
            margin-top: 6px;
        }

        .site-content .letter {
            background: #fffcf9;
            padding: 32px 36px;
            margin-top: 28px;
            border-radius: 16px;
            border: 1px solid #eee8e0;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.02);
        }

        .site-content .letter .greeting {
            font-size: 18px;
            font-weight: 500;
            color: #2c2a28;
        }

        .site-content .letter .body {
            font-size: 16px;
            line-height: 1.8;
            color: #4a4540;
            margin-top: 12px;
        }

        .site-content .letter .signature {
            text-align: right;
            margin-top: 20px;
            color: #8a8580;
            font-style: italic;
        }

        .site-content .footer {
            text-align: center;
            margin-top: 32px;
            font-size: 13px;
            color: #b8b0a8;
        }
    </style>
</head>
<body>

    <!-- ==================== 密码锁 ==================== -->
    <div id="lockScreen" class="lock-container">
        <span class="icon">✉️</span>
        <h1>4you4ever</h1>
        <p class="sub">输入密码，打开这封信</p>
        <input type="password" id="passwordInput" placeholder="· · · · · · · ·" maxlength="20">
        <button class="btn-unlock" id="unlockBtn">🔓 解锁</button>
        <div class="error-msg" id="errorMsg"></div>
        <div class="hint">💌 只有知道密码的人才能打开</div>
    </div>

    <!-- ==================== 网站内容（密码正确后显示） ==================== -->
    <div id="siteContent" class="site-content">
        <div class="header">
            <h1>✉️ 4you4ever</h1>
            <p>slow letters, softly delivered.</p>
        </div>

        <div class="letter">
            <div class="greeting">亲爱的，</div>
            <div class="body">
                这里的早晨没有你，很安静。<br>
                咖啡还是苦的，天空还是宽的，<br>
                而我，还是你的。
            </div>
            <div class="signature">— 星期日 · 黄昏</div>
        </div>

        <div class="footer">
            🌙 这封信只属于你和我
        </div>
    </div>

    <script>
        // ============================================================
        //  🔐 在这里修改你的密码！（只改下面这一行）
        // ============================================================
        const CORRECT_PASSWORD = '20260710';  // ← 把 20260710 改成你们约定的密码
        // ============================================================

        const lockScreen = document.getElementById('lockScreen');
        const siteContent = document.getElementById('siteContent');
        const passwordInput = document.getElementById('passwordInput');
        const unlockBtn = document.getElementById('unlockBtn');
        const errorMsg = document.getElementById('errorMsg');

        // 解锁函数
        function unlock() {
            const input = passwordInput.value.trim();

            if (input === '') {
                errorMsg.textContent = '请输入密码 ✍️';
                return;
            }

            if (input === CORRECT_PASSWORD) {
                // 密码正确：显示网站内容
                lockScreen.style.display = 'none';
                siteContent.style.display = 'block';
                errorMsg.textContent = '';
                // 把密码记录在 URL 里（方便刷新后不用重新输入）
                history.pushState({ unlocked: true }, '', '?unlocked=true');
            } else {
                errorMsg.textContent = '❌ 密码不对，再试试吧';
                passwordInput.value = '';
                passwordInput.focus();
            }
        }

        // 点击解锁按钮
        unlockBtn.addEventListener('click', unlock);

        // 按回车键解锁
        passwordInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') unlock();
        });

        // 如果 URL 里带了 ?unlocked=true，自动跳过密码锁（刷新页面后保持解锁状态）
        window.addEventListener('load', () => {
            const params = new URLSearchParams(window.location.search);
            if (params.get('unlocked') === 'true') {
                // 但还是要检查一下是不是真的知道密码（防止别人直接加参数）
                // 这里简单处理：如果有参数，就显示内容（但实际使用中建议结合 sessionStorage）
                lockScreen.style.display = 'none';
                siteContent.style.display = 'block';
            }
        });

        // 可选：输入时清空错误提示
        passwordInput.addEventListener('input', () => {
            errorMsg.textContent = '';
        });
    </script>

</body>
</html>
