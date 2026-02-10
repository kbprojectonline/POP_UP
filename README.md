<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Dashboard - Premium Control</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary: #3b82f6;
            --bg-body: #f1f5f9;
            --card-bg: #ffffff;
            --text-main: #1e293b;
            --text-sub: #64748b;
            --silver: #94a3b8;
            --gold: #f59e0b;
            --diamond: #0ea5e9;
        }

        body { 
            font-family: 'Poppins', sans-serif; 
            background: var(--bg-body); 
            display: flex; flex-direction: column; align-items: center; 
            min-height: 100vh; margin: 0; padding: 20px;
            color: var(--text-main);
            transition: zoom 0.2s ease;
        }

        /* --- KARTU UTAMA (LEBAR 1000PX) --- */
        .dashboard-card { 
            background: var(--card-bg); 
            width: 95% !important; 
            max-width: 1000px !important; /* KHUSUS LEBAR */
            border-radius: 24px; 
            box-shadow: 0 20px 40px rgba(0,0,0,0.08); 
            padding: 35px; 
            position: relative;
            margin-top: 20px;
            margin-bottom: 20px;
        }

        /* HEADER */
        .header { text-align: center; margin-bottom: 30px; }
        .header h1 { margin: 0; font-size: 1.8rem; font-weight: 700; color: var(--text-main); }
        .header p { margin: 5px 0 0; color: var(--text-sub); font-size: 0.9rem; }

        /* MENU ZOOM (POJOK KANAN) */
        .menu-wrapper { position: absolute; top: 25px; right: 25px; z-index: 50; }
        .btn-menu {
            background: #f8fafc; border: 1px solid #e2e8f0; border-radius: 12px;
            width: 42px; height: 42px; display: flex; align-items: center; justify-content: center;
            cursor: pointer; font-size: 1.2rem; transition: 0.3s; color: var(--text-sub);
        }
        .btn-menu:hover { background: white; box-shadow: 0 5px 15px rgba(0,0,0,0.1); color: var(--primary); }
        
        .zoom-dropdown {
            display: none; position: absolute; top: 50px; right: 0;
            background: white; border: 1px solid #f1f5f9; border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15); padding: 15px; width: 180px;
            animation: slideDown 0.2s ease;
        }
        .zoom-dropdown.show { display: block; }
        .zoom-dropdown label { display: block; font-size: 0.75rem; font-weight: 700; color: var(--text-sub); margin-bottom: 8px; text-transform: uppercase; letter-spacing: 1px; }
        .zoom-dropdown select { width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #cbd5e1; font-family: inherit; font-size: 0.9rem; }

        /* LOGIN AREA */
        .login-box { text-align: center; padding: 40px 0; }
        .btn-google {
            background: #ffffff; color: #333; border: 1px solid #ddd;
            padding: 12px 25px; border-radius: 50px; font-weight: 600;
            cursor: pointer; display: inline-flex; align-items: center; gap: 10px;
            font-size: 1rem; box-shadow: 0 2px 5px rgba(0,0,0,0.1); transition: 0.3s;
        }
        .btn-google:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(0,0,0,0.15); }

        /* MASTER SWITCH (SAKLAR UTAMA) */
        .master-panel {
            background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
            padding: 20px 25px; border-radius: 16px;
            display: flex; justify-content: space-between; align-items: center;
            margin-bottom: 40px; border: 1px solid #cbd5e1; cursor: pointer;
        }
        .master-info h3 { margin: 0; font-size: 1rem; color: var(--text-sub); text-transform: uppercase; letter-spacing: 1px; }
        .master-status { font-size: 1.4rem; font-weight: 800; margin-top: 5px; }
        .status-on { color: #10b981; }
        .status-off { color: #ef4444; }

        /* ITEM ROWS (LIST HARGA) */
        .section-title {
            display: flex; align-items: center; gap: 15px; margin-top: 30px; margin-bottom: 15px;
        }
        .section-title span { font-weight: 700; font-size: 0.9rem; letter-spacing: 1px; text-transform: uppercase; }
        .line { flex: 1; height: 1px; background: #e2e8f0; }
        
        /* Warna Header Kategori */
        .head-silver { color: var(--silver); }
        .head-gold { color: var(--gold); }
        .head-diamond { color: var(--diamond); }

        .item-row {
            display: flex; justify-content: space-between; align-items: center;
            background: #fff; padding: 12px 20px; border-radius: 16px;
            border: 1px solid #f1f5f9; margin-bottom: 12px; transition: 0.2s;
        }
        .item-row:hover { border-color: #cbd5e1; box-shadow: 0 4px 12px rgba(0,0,0,0.03); transform: scale(1.005); }

        .item-left { display: flex; align-items: center; gap: 15px; }
        
        /* ICON BOX (KUNCI DI KIRI) */
        .icon-box {
            width: 48px; height: 48px; border-radius: 12px;
            display: flex; align-items: center; justify-content: center;
            flex-shrink: 0;
        }
        .icon-silver { background: #f1f5f9; color: var(--silver); }
        .icon-gold { background: #fffbeb; color: var(--gold); }
        .icon-diamond { background: #e0f2fe; color: var(--diamond); }
        
        .svg-key { width: 24px; height: 24px; fill: currentColor; }

        .item-details { display: flex; flex-direction: column; }
        .name { font-weight: 600; font-size: 1rem; color: var(--text-main); }
        .price { font-size: 0.85rem; color: var(--text-sub); margin-top: 2px; }

        /* SWITCH TOGGLE IOS STYLE */
        .switch { position: relative; display: inline-block; width: 52px; height: 30px; flex-shrink: 0; }
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider {
            position: absolute; cursor: pointer; top: 0; left: 0; right: 0; bottom: 0;
            background-color: #cbd5e1; transition: .4s; border-radius: 34px;
        }
        .slider:before {
            position: absolute; content: ""; height: 22px; width: 22px;
            left: 4px; bottom: 4px; background-color: white;
            transition: .4s; border-radius: 50%; box-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }
        input:checked + .slider { background-color: var(--primary); }
        input:checked + .slider:before { transform: translateX(22px); }

        /* BUTTON LOGOUT */
        .btn-logout {
            width: 100%; padding: 15px; background: #fee2e2; color: #ef4444; 
            border: none; border-radius: 12px; font-weight: 700; margin-top: 40px; 
            cursor: pointer; font-size: 1rem; transition: 0.2s;
        }
        .btn-logout:hover { background: #fecaca; }

        .hide { display: none !important; }
        @keyframes slideDown { from {opacity:0; transform:translateY(-10px);} to {opacity:1; transform:translateY(0);} }

    </style>
</head>
<body>

    <div class="dashboard-card">
        
        <div class="menu-wrapper">
            <button class="btn-menu" onclick="toggleMenu()">⚙️</button>
            <div id="zoom-box" class="zoom-dropdown">
                <label>Skala Tampilan</label>
                <select id="zoom-select" onchange="applyZoom(this.value)">
                    <option value="0.5">50% (Tiny)</option>
                    <option value="0.7">70%</option>
                    <option value="0.8">80%</option>
                    <option value="0.9">90%</option>
                    <option value="1.0" selected>100% (Normal)</option>
                    <option value="1.1">110%</option>
                    <option value="1.2">120%</option>
                    <option value="1.3">130%</option>
                    <option value="1.4">140%</option>
                    <option value="1.5">150% (Large)</option>
                    <option value="1.6">160%</option>
                    <option value="1.7">170%</option>
                    <option value="1.8">180%</option>
                    <option value="1.9">190% (Max)</option>
                </select>
            </div>
        </div>

        <div class="header">
            <h1>Admin Panel</h1>
            <p>Kelola Promo & Stok Kunci</p>
        </div>

        <div id="login-view" class="login-box">
            <div style="font-size: 4rem; margin-bottom: 10px;">🔒</div>
            <p style="margin-bottom: 20px;">Anda harus login sebagai Admin.</p>
            <button class="btn-google" onclick="doLogin()">
                <img src="https://www.gstatic.com/firebasejs/ui/2.0.0/images/auth/google.svg" width="20">
                Login dengan Google
            </button>
        </div>

        <div id="control-view" class="hide">
            
            <div class="master-panel" onclick="toggleMasterSwitch()">
                <div class="master-info">
                    <h3>Status Utama</h3>
                    <div id="master-status-text" class="master-status status-off">OFFLINE</div>
                </div>
                <div id="master-icon" style="font-size: 2rem;">🔴</div>
            </div>

            <div class="section-title head-silver">
                <span>Silver Package</span> <div class="line" style="background: currentColor; opacity: 0.3;"></div>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-silver">
                        <svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg>
                    </div>
                    <div class="item-details">
                        <span class="name">100 Kunci Silver</span>
                        <span class="price">Rp 2.950.000</span>
                    </div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_100" onchange="updateItem('promo_silver_100')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-silver"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">50 Kunci Silver</span><span class="price">Rp 1.480.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_50" onchange="updateItem('promo_silver_50')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-silver"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">20 Kunci Silver</span><span class="price">Rp 600.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_20" onchange="updateItem('promo_silver_20')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-silver"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">10 Kunci Silver</span><span class="price">Rp 310.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_10" onchange="updateItem('promo_silver_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-silver"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">5 Kunci Silver</span><span class="price">Rp 165.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_5" onchange="updateItem('promo_silver_5')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-silver"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">1 Kunci Silver</span><span class="price">Rp 35.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_silver_1" onchange="updateItem('promo_silver_1')"><span class="slider"></span></label>
            </div>


            <div class="section-title head-gold">
                <span>Gold Package</span> <div class="line" style="background: currentColor; opacity: 0.3;"></div>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-gold"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">70 Kunci Gold</span><span class="price">Rp 5.000.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_70" onchange="updateItem('promo_gold_70')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-gold"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">50 Kunci Gold</span><span class="price">Rp 3.700.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_50" onchange="updateItem('promo_gold_50')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-gold"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">10 Kunci Gold</span><span class="price">Rp 760.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_10" onchange="updateItem('promo_gold_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-gold"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">5 Kunci Gold</span><span class="price">Rp 410.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_5" onchange="updateItem('promo_gold_5')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-gold"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">1 Kunci Gold</span><span class="price">Rp 85.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_gold_1" onchange="updateItem('promo_gold_1')"><span class="slider"></span></label>
            </div>


            <div class="section-title head-diamond">
                <span>Diamond Package</span> <div class="line" style="background: currentColor; opacity: 0.3;"></div>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-diamond"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">25 Kunci Diamond</span><span class="price">Rp 5.300.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_25" onchange="updateItem('promo_diamond_25')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-diamond"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">15 Kunci Diamond</span><span class="price">Rp 3.250.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_15" onchange="updateItem('promo_diamond_15')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-diamond"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">10 Kunci Diamond</span><span class="price">Rp 2.200.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_10" onchange="updateItem('promo_diamond_10')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-diamond"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">5 Kunci Diamond</span><span class="price">Rp 1.150.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_5" onchange="updateItem('promo_diamond_5')"><span class="slider"></span></label>
            </div>

            <div class="item-row">
                <div class="item-left">
                    <div class="icon-box icon-diamond"><svg class="svg-key" viewBox="0 0 24 24"><path d="M7 14c-2.21 0-4-1.79-4-4S4.79 6 7 6s4 1.79 4 4c0 .73-.2 1.41-.55 2H11v1h2v2h2v1h2v-2.1c.71-.53 1.25-1.28 1.45-2.18l-1.95-.43c-.15.65-.74 1.11-1.4 1.11-.22 0-.43-.05-.62-.15l-.26-.14-.29.12C10.53 13.9 8.85 14 7 14zM7 8c-1.1 0-2 .9-2 2s.9 2 2 2 2-.9 2-2-.9-2-2-2z"/></svg></div>
                    <div class="item-details"><span class="name">1 Kunci Diamond</span><span class="price">Rp 250.000</span></div>
                </div>
                <label class="switch"><input type="checkbox" id="chk_promo_diamond_1" onchange="updateItem('promo_diamond_1')"><span class="slider"></span></label>
            </div>

            <button class="btn-logout" onclick="doLogout()">Keluar Aplikasi</button>
        </div>
    </div>

    <script>
        function toggleMenu() {
            document.getElementById('zoom-box').classList.toggle('show');
        }

        function applyZoom(val) {
            document.body.style.zoom = val;
            localStorage.setItem('admin_zoom_pref', val);
        }

        window.onload = function() {
            const saved = localStorage.getItem('admin_zoom_pref') || "1.0";
            document.body.style.zoom = saved;
            const select = document.getElementById('zoom-select');
            if(select) select.value = saved;
        }
    </script>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, signInWithPopup, GoogleAuthProvider, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";
        import { getDatabase, ref, onValue, set } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBublDvXwqKWK3lACZ_plD3ORMS1h2MvTM",
            authDomain: "kuis-belajar-fc843.firebaseapp.com",
            databaseURL: "https://kuis-belajar-fc843-default-rtdb.asia-southeast1.firebasedatabase.app",
            projectId: "kuis-belajar-fc843",
            storageBucket: "kuis-belajar-fc843.firebasestorage.app",
            messagingSenderId: "851984555383",
            appId: "1:851984555383:web:e47824f590620b73849572"
        };

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getDatabase(app);
        const provider = new GoogleAuthProvider();

        const ADMIN_UID = "G6N2sLEF6vX0e3X9ndbmft1oHVg2";
        let masterStatus = false;

        // UI Helpers
        window.doLogin = () => signInWithPopup(auth, provider).catch(e => alert(e.message));
        window.doLogout = () => signOut(auth).then(() => location.reload());

        // Master Switch UI
        function setMasterUI(isActive) {
            const txt = document.getElementById('master-status-text');
            const icon = document.getElementById('master-icon');
            if(isActive) {
                txt.innerText = "ONLINE (AKTIF)";
                txt.className = "master-status status-on";
                icon.innerText = "🟢";
            } else {
                txt.innerText = "OFFLINE (MATI)";
                txt.className = "master-status status-off";
                icon.innerText = "🔴";
            }
        }

        // Logic Toggle
        window.toggleMasterSwitch = () => {
            set(ref(db, 'config/promo_active'), !masterStatus);
        };

        window.updateItem = (itemId) => {
            const chk = document.getElementById('chk_' + itemId);
            if(chk) set(ref(db, `config/promo_items/${itemId}`), chk.checked);
        };

        // Auth Listener
        onAuthStateChanged(auth, (user) => {
            if (user && user.uid === ADMIN_UID) {
                document.getElementById('login-view').classList.add('hide');
                document.getElementById('control-view').classList.remove('hide');
                
                // Listen Master
                onValue(ref(db, 'config/promo_active'), (snap) => {
                    masterStatus = snap.val() === true;
                    setMasterUI(masterStatus);
                });

                // Listen Items
                onValue(ref(db, 'config/promo_items'), (snap) => {
                    const data = snap.val() || {};
                    const keys = [
                        'promo_silver_100', 'promo_silver_50', 'promo_silver_20', 'promo_silver_10', 'promo_silver_5', 'promo_silver_1',
                        'promo_gold_70', 'promo_gold_50', 'promo_gold_10', 'promo_gold_5', 'promo_gold_1',
                        'promo_diamond_25', 'promo_diamond_15', 'promo_diamond_10', 'promo_diamond_5', 'promo_diamond_1'
                    ];
                    keys.forEach(k => {
                        const el = document.getElementById('chk_' + k);
                        if(el) el.checked = data[k] === true;
                    });
                });

            } else if (user) {
                alert("Bukan Admin!");
                signOut(auth);
            }
        });
    </script>
</body>
</html>
