<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gita Yunita - Keuangan Jajan</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
            padding: 30px;
            width: 100%;
            max-width: 500px;
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .app-title {
            text-align: center;
            margin-bottom: 30px;
        }

        .app-title h1 {
            font-size: 2.5em;
            background: linear-gradient(45deg, #ff6b6b, #ee5a24);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-weight: 800;
            letter-spacing: 2px;
            cursor: pointer;
            transition: transform 0.3s ease;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .app-title h1:hover {
            transform: scale(1.05);
        }

        .app-title .subtitle {
            color: #666;
            font-size: 0.9em;
            margin-top: 5px;
        }

        .balance-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 20px;
            padding: 25px;
            color: white;
            margin-bottom: 30px;
            text-align: center;
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
        }

        .balance-label {
            font-size: 0.9em;
            opacity: 0.9;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .balance-amount {
            font-size: 3em;
            font-weight: bold;
            margin: 10px 0;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 30px;
        }

        .menu-item {
            background: #f8f9fa;
            border: 2px solid #e9ecef;
            border-radius: 20px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .menu-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            border-color: #ff6b6b;
        }

        .menu-item:active {
            transform: scale(0.95);
        }

        .menu-emoji {
            font-size: 2.5em;
            margin-bottom: 10px;
            display: block;
        }

        .menu-name {
            font-weight: 600;
            color: #333;
            margin-bottom: 5px;
        }

        .menu-price {
            color: #ff6b6b;
            font-weight: bold;
            font-size: 1.2em;
        }

        .menu-item.telur-gulung {
            background: linear-gradient(135deg, #ffeaa7, #fdcb6e);
        }

        .menu-item.es-teh {
            background: linear-gradient(135deg, #a29bfe, #6c5ce7);
            color: white;
        }

        .menu-item.risol {
            background: linear-gradient(135deg, #ffb8b8, #ff6b6b);
            color: white;
        }

        .menu-item.cilok {
            background: linear-gradient(135deg, #81ecec, #00b894);
            color: white;
        }

        .menu-item.es-teh .menu-name,
        .menu-item.es-teh .menu-price,
        .menu-item.risol .menu-name,
        .menu-item.risol .menu-price,
        .menu-item.cilok .menu-name,
        .menu-item.cilok .menu-price {
            color: white;
        }

        .history-section {
            background: #f8f9fa;
            border-radius: 20px;
            padding: 20px;
        }

        .history-title {
            font-weight: 600;
            margin-bottom: 15px;
            color: #333;
            font-size: 1.1em;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .history-list {
            max-height: 200px;
            overflow-y: auto;
        }

        .history-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px;
            border-bottom: 1px solid #e9ecef;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateX(-20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .history-item:last-child {
            border-bottom: none;
        }

        .history-item-name {
            font-weight: 500;
            color: #333;
        }

        .history-item-price {
            color: #ff6b6b;
            font-weight: bold;
        }

        .history-item-time {
            font-size: 0.8em;
            color: #999;
        }

        .reset-btn {
            background: #ff6b6b;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 0.9em;
            transition: all 0.3s ease;
        }

        .reset-btn:hover {
            background: #ee5a24;
            transform: scale(1.05);
        }

        .empty-state {
            text-align: center;
            color: #999;
            padding: 20px;
            font-style: italic;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            padding: 15px 20px;
            border-radius: 10px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            animation: slideInRight 0.3s ease;
            z-index: 1000;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        @keyframes slideInRight {
            from { opacity: 0; transform: translateX(100px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .notification.success {
            border-left: 4px solid #00b894;
        }

        .notification.error {
            border-left: 4px solid #ff6b6b;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header Aplikasi yang bisa diklik -->
        <div class="app-title">
            <h1 onclick="showAppInfo()" title="Klik untuk info aplikasi">🌸 Gita Yunita 🌸</h1>
            <p class="subtitle">✨ Catatan Keuangan Jajan ✨</p>
        </div>

        <!-- Saldo -->
        <div class="balance-card">
            <div class="balance-label">💰 Total Pengeluaran</div>
            <div class="balance-amount" id="totalBalance">Rp 0</div>
            <div style="font-size: 0.8em; opacity: 0.8;">💖 Jajan hemat, hidup nikmat!</div>
        </div>

        <!-- Menu Jajan -->
        <div class="menu-grid">
            <div class="menu-item telur-gulung" onclick="addTransaction('Telur Gulung', 2000, this)">
                <span class="menu-emoji">🥚</span>
                <div class="menu-name">Telur Gulung</div>
                <div class="menu-price">Rp 2.000</div>
            </div>
            
            <div class="menu-item es-teh" onclick="addTransaction('Es Teh', 3000, this)">
                <span class="menu-emoji">🧊</span>
                <div class="menu-name">Es Teh</div>
                <div class="menu-price">Rp 3.000</div>
            </div>
            
            <div class="menu-item risol" onclick="addTransaction('Risol', 2000, this)">
                <span class="menu-emoji">🥟</span>
                <div class="menu-name">Risol</div>
                <div class="menu-price">Rp 2.000</div>
            </div>
            
            <div class="menu-item cilok" onclick="addTransaction('Cilok', 2000, this)">
                <span class="menu-emoji">🍡</span>
                <div class="menu-name">Cilok</div>
                <div class="menu-price">Rp 2.000</div>
            </div>
        </div>

        <!-- Riwayat Transaksi -->
        <div class="history-section">
            <div class="history-title">
                📋 Riwayat Jajan
                <button class="reset-btn" onclick="resetAll()">🔄 Reset</button>
            </div>
            <div class="history-list" id="historyList">
                <div class="empty-state">
                    🍽️ Belum ada transaksi nih...<br>
                    <small>Ayo jajan dulu! 😋</small>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Data transaksi
        let transactions = JSON.parse(localStorage.getItem('gitaYunitaTransactions')) || [];
        let totalBalance = transactions.reduce((sum, t) => sum + t.price, 0);

        // Inisialisasi tampilan
        updateDisplay();

        function addTransaction(name, price, element) {
            // Animasi klik pada menu item
            element.style.transform = 'scale(0.9)';
            setTimeout(() => {
                element.style.transform = '';
            }, 150);

            // Tambah transaksi
            const transaction = {
                id: Date.now(),
                name: name,
                price: price,
                time: new Date().toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' }),
                date: new Date().toLocaleDateString('id-ID', { day: 'numeric', month: 'short' })
            };
            
            transactions.unshift(transaction);
            totalBalance += price;
            
            // Simpan ke localStorage
            saveData();
            
            // Update tampilan
            updateDisplay();
            
            // Tampilkan notifikasi
            showNotification(`✅ ${name} ditambahkan! (+Rp ${price.toLocaleString('id-ID')})`, 'success');
        }

        function updateDisplay() {
            // Update saldo
            document.getElementById('totalBalance').textContent = 
                'Rp ' + totalBalance.toLocaleString('id-ID');
            
            // Update riwayat
            const historyList = document.getElementById('historyList');
            
            if (transactions.length === 0) {
                historyList.innerHTML = `
                    <div class="empty-state">
                        🍽️ Belum ada transaksi nih...<br>
                        <small>Ayo jajan dulu! 😋</small>
                    </div>
                `;
            } else {
                historyList.innerHTML = transactions.map(t => `
                    <div class="history-item">
                        <div>
                            <div class="history-item-name">${t.name}</div>
                            <div class="history-item-time">📅 ${t.date} ⏰ ${t.time}</div>
                        </div>
                        <div class="history-item-price">Rp ${t.price.toLocaleString('id-ID')}</div>
                    </div>
                `).join('');
            }
        }

        function resetAll() {
            if (transactions.length === 0) {
                showNotification('ℹ️ Belum ada transaksi untuk direset', 'error');
                return;
            }
            
            if (confirm('Yakin mau reset semua riwayat jajan? 🙈\nData tidak bisa dikembalikan lho...')) {
                transactions = [];
                totalBalance = 0;
                saveData();
                updateDisplay();
                showNotification('🔄 Semua riwayat berhasil direset!', 'success');
            }
        }

        function saveData() {
            localStorage.setItem('gitaYunitaTransactions', JSON.stringify(transactions));
        }

        function showNotification(message, type) {
            // Hapus notifikasi lama jika ada
            const oldNotification = document.querySelector('.notification');
            if (oldNotification) {
                oldNotification.remove();
            }
            
            // Buat notifikasi baru
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            notification.textContent = message;
            document.body.appendChild(notification);
            
            // Hapus notifikasi setelah 2 detik
            setTimeout(() => {
                notification.style.opacity = '0';
                notification.style.transform = 'translateX(100px)';
                notification.style.transition = 'all 0.3s ease';
                setTimeout(() => {
                    notification.remove();
                }, 300);
            }, 2000);
        }

        function showAppInfo() {
            const infoHTML = `
                <div style="text-align: center;">
                    <h2>🌸 Gita Yunita 🌸</h2>
                    <p style="margin: 10px 0;">Aplikasi Pencatat Keuangan Jajan</p>
                    <p style="font-size: 0.9em; color: #666;">
                        Versi 1.0<br>
                        Dibuat dengan ❤️<br>
                        🍽️ Catat jajanmu, atur keuanganmu!<br>
                        💖 Hemat pangkal kaya!
                    </p>
                    <p style="margin-top: 10px; font-size: 0.8em; color: #999;">
                        Total transaksi hari ini: <strong>${transactions.length}</strong><br>
                        Total pengeluaran: <strong>Rp ${totalBalance.toLocaleString('id-ID')}</strong>
                    </p>
                </div>
            `;
            
            alert(infoHTML.replace(/<[^>]*>/g, '')); // Tampilkan sebagai plain text di alert
        }

        // Keyboard shortcut
        document.addEventListener('keydown', function(e) {
            switch(e.key.toLowerCase()) {
                case '1':
                    document.querySelectorAll('.menu-item')[0].click();
                    break;
                case '2':
                    document.querySelectorAll('.menu-item')[1].click();
                    break;
                case '3':
                    document.querySelectorAll('.menu-item')[2].click();
                    break;
                case '4':
                    document.querySelectorAll('.menu-item')[3].click();
                    break;
                case 'r':
                    if (e.ctrlKey) {
                        e.preventDefault();
                        resetAll();
                    }
                    break;
            }
        });

        console.log('🌸 Aplikasi Gita Yunita siap digunakan!');
        console.log('💡 Tips: Tekan tombol 1-4 untuk quick add jajan');
        console.log('💰 Total pengeluaran: Rp ' + totalBalance.toLocaleString('id-ID'));
    </script>
</body>
</html>
