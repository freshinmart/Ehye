<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KasPOS - Scanner Barcode Lengkap</title>
    <!-- Library untuk scanner barcode -->
    <script src="https://cdn.jsdelivr.net/npm/quagga@0.12.1/dist/quagga.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            display: flex;
            min-height: 100vh;
        }
        
        /* Sidebar Styles */
        .sidebar {
            width: 280px;
            background: linear-gradient(135deg, #2c3e50, #34495e);
            color: white;
            padding: 0;
            height: 100vh;
            position: fixed;
            overflow-y: auto;
            box-shadow: 2px 0 10px rgba(0,0,0,0.1);
            z-index: 1000;
        }
        
        .sidebar-header {
            padding: 25px 20px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            background-color: rgba(0,0,0,0.1);
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .logo-icon {
            font-size: 24px;
            background-color: #3498db;
            width: 40px;
            height: 40px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .logo-text {
            font-size: 20px;
            font-weight: 700;
        }
        
        .trial-info {
            margin-top: 10px;
            font-size: 13px;
            color: #ecf0f1;
            background-color: rgba(52, 152, 219, 0.2);
            padding: 8px 12px;
            border-radius: 6px;
            border-left: 3px solid #3498db;
        }
        
        .menu {
            padding: 15px 0;
        }
        
        .menu-section {
            margin-bottom: 10px;
        }
        
        .menu-title {
            font-size: 12px;
            text-transform: uppercase;
            color: #bdc3c7;
            padding: 10px 20px;
            letter-spacing: 1px;
        }
        
        .menu-item {
            padding: 12px 20px;
            display: flex;
            align-items: center;
            gap: 12px;
            cursor: pointer;
            transition: all 0.3s;
            border-left: 3px solid transparent;
        }
        
        .menu-item:hover {
            background-color: rgba(255,255,255,0.05);
            border-left-color: #3498db;
        }
        
        .menu-item.active {
            background-color: rgba(52, 152, 219, 0.2);
            border-left-color: #3498db;
        }
        
        .menu-item i {
            font-size: 18px;
            width: 24px;
            text-align: center;
        }
        
        .menu-item-text {
            flex: 1;
        }
        
        .badge {
            background-color: #e74c3c;
            color: white;
            font-size: 11px;
            padding: 2px 8px;
            border-radius: 10px;
        }
        
        .menu-divider {
            height: 1px;
            background-color: rgba(255,255,255,0.1);
            margin: 15px 20px;
        }
        
        .upgrade-section {
            margin: 20px;
            padding: 15px;
            background: linear-gradient(135deg, #3498db, #2980b9);
            border-radius: 8px;
            text-align: center;
        }
        
        .upgrade-title {
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 8px;
        }
        
        .upgrade-desc {
            font-size: 12px;
            margin-bottom: 12px;
            opacity: 0.9;
        }
        
        .btn-upgrade {
            background-color: white;
            color: #3498db;
            border: none;
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 12px;
            width: 100%;
        }
        
        .btn-upgrade:hover {
            background-color: #f8f9fa;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        /* Main Content Styles */
        .main-content {
            flex: 1;
            margin-left: 280px;
            padding: 20px;
            transition: margin-left 0.3s;
        }
        
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #ddd;
        }
        
        .trial-notice {
            background-color: #fff8e1;
            border-left: 4px solid #ffc107;
            padding: 12px 15px;
            margin-bottom: 20px;
            border-radius: 4px;
            font-size: 14px;
        }
        
        .content-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .page-title {
            font-size: 22px;
            font-weight: 600;
            color: #2c3e50;
        }
        
        .btn {
            padding: 8px 16px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.3s;
        }
        
        .btn-primary {
            background-color: #3498db;
            color: white;
        }
        
        .btn-secondary {
            background-color: #95a5a6;
            color: white;
        }
        
        .btn-success {
            background-color: #2ecc71;
            color: white;
        }
        
        .btn-danger {
            background-color: #e74c3c;
            color: white;
        }
        
        .btn-warning {
            background-color: #f39c12;
            color: white;
        }
        
        /* Halaman Scanner */
        .scanner-container {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            padding: 25px;
            margin-top: 20px;
            text-align: center;
        }
        
        .scanner-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .scanner-title {
            font-size: 20px;
            font-weight: 600;
            color: #2c3e50;
        }
        
        .scanner-preview-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin: 0 auto;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        }
        
        .scanner-preview {
            width: 100%;
            height: 400px;
            background-color: #2c3e50;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 18px;
            position: relative;
        }
        
        #interactive {
            width: 100%;
            height: 100%;
        }
        
        .scanner-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: linear-gradient(to bottom, 
                rgba(0,0,0,0.3) 0%, 
                rgba(0,0,0,0) 30%, 
                rgba(0,0,0,0) 70%, 
                rgba(0,0,0,0.3) 100%);
        }
        
        .scanner-frame {
            width: 80%;
            height: 200px;
            border: 2px solid #3498db;
            position: relative;
            box-shadow: 0 0 0 1000px rgba(0, 0, 0, 0.4);
        }
        
        .scanner-frame::before, .scanner-frame::after {
            content: '';
            position: absolute;
            width: 30px;
            height: 30px;
            border: 3px solid #3498db;
        }
        
        .scanner-frame::before {
            top: -3px;
            left: -3px;
            border-right: none;
            border-bottom: none;
        }
        
        .scanner-frame::after {
            bottom: -3px;
            right: -3px;
            border-left: none;
            border-top: none;
        }
        
        .scanner-corner-top-left::before {
            content: '';
            position: absolute;
            top: 10px;
            left: 10px;
            width: 20px;
            height: 20px;
            border-top: 3px solid #3498db;
            border-left: 3px solid #3498db;
        }
        
        .scanner-corner-top-right::before {
            content: '';
            position: absolute;
            top: 10px;
            right: 10px;
            width: 20px;
            height: 20px;
            border-top: 3px solid #3498db;
            border-right: 3px solid #3498db;
        }
        
        .scanner-corner-bottom-left::before {
            content: '';
            position: absolute;
            bottom: 10px;
            left: 10px;
            width: 20px;
            height: 20px;
            border-bottom: 3px solid #3498db;
            border-left: 3px solid #3498db;
        }
        
        .scanner-corner-bottom-right::before {
            content: '';
            position: absolute;
            bottom: 10px;
            right: 10px;
            width: 20px;
            height: 20px;
            border-bottom: 3px solid #3498db;
            border-right: 3px solid #3498db;
        }
        
        .scanner-guide {
            color: white;
            text-align: center;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.7);
            margin-top: 20px;
            font-size: 16px;
        }
        
        .scanner-controls {
            margin-top: 20px;
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        .btn-scan {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s;
        }
        
        .btn-scan:hover {
            background-color: #2980b9;
            transform: translateY(-2px);
        }
        
        .scanner-status {
            margin-top: 15px;
            padding: 10px;
            border-radius: 4px;
            font-size: 14px;
        }
        
        .scanner-status.success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .scanner-status.error {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .scanner-status.info {
            background-color: #d1ecf1;
            color: #0c5460;
            border: 1px solid #bee5eb;
        }
        
        .scanner-status.warning {
            background-color: #fff3cd;
            color: #856404;
            border: 1px solid #ffeaa7;
        }
        
        .scanner-result {
            margin-top: 15px;
            padding: 15px;
            background-color: #f8f9fa;
            border-radius: 8px;
            text-align: center;
            display: none;
        }
        
        .barcode-value {
            font-family: monospace;
            font-size: 1.4rem;
            font-weight: bold;
            color: #2ecc71;
            margin: 10px 0;
            padding: 10px;
            background-color: white;
            border-radius: 4px;
            border: 1px solid #ddd;
        }
        
        .scanner-options {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        
        .option-group {
            display: flex;
            gap: 10px;
            align-items: center;
        }
        
        .option-label {
            font-size: 14px;
            color: #555;
        }
        
        .option-select {
            padding: 8px 12px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: white;
            cursor: pointer;
        }
        
        .scanner-stats {
            display: flex;
            justify-content: space-around;
            margin-top: 20px;
            padding: 15px;
            background-color: #f8f9fa;
            border-radius: 8px;
        }
        
        .stat-item {
            text-align: center;
        }
        
        .stat-value {
            font-size: 24px;
            font-weight: bold;
            color: #3498db;
        }
        
        .stat-label {
            font-size: 14px;
            color: #7f8c8d;
        }
        
        .scanner-history {
            margin-top: 30px;
        }
        
        .history-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 15px;
            color: #2c3e50;
        }
        
        .history-list {
            max-height: 200px;
            overflow-y: auto;
            border: 1px solid #eee;
            border-radius: 8px;
            padding: 10px;
        }
        
        .history-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 12px;
            border-bottom: 1px solid #eee;
        }
        
        .history-item:last-child {
            border-bottom: none;
        }
        
        .history-barcode {
            font-family: monospace;
            font-weight: bold;
        }
        
        .history-time {
            color: #7f8c8d;
            font-size: 12px;
        }
        
        .recent-products {
            margin-top: 30px;
        }
        
        .cart-button {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #2ecc71;
            color: white;
            padding: 12px 20px;
            border-radius: 50px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            z-index: 100;
        }
        
        /* Scanner Modal */
        .scanner-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.8);
            z-index: 2000;
            align-items: center;
            justify-content: center;
        }
        
        .scanner-modal-content {
            background-color: white;
            padding: 25px;
            border-radius: 8px;
            width: 90%;
            max-width: 800px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            position: relative;
        }
        
        .scanner-modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .scanner-modal-title {
            font-size: 20px;
            font-weight: 600;
        }
        
        .close-modal {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #7f8c8d;
        }
        
        /* Scanner Animation */
        @keyframes scan-line {
            0% {
                top: 10%;
            }
            50% {
                top: 90%;
            }
            100% {
                top: 10%;
            }
        }
        
        .scan-line {
            position: absolute;
            left: 10%;
            width: 80%;
            height: 3px;
            background: linear-gradient(to right, transparent, #3498db, transparent);
            animation: scan-line 2s linear infinite;
            box-shadow: 0 0 10px rgba(52, 152, 219, 0.7);
        }
        
        /* Responsive Styles */
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                height: auto;
                position: relative;
            }
            
            .main-content {
                margin-left: 0;
            }
            
            .scanner-preview {
                height: 300px;
            }
            
            .scanner-controls {
                flex-direction: column;
                align-items: center;
            }
            
            .scanner-stats {
                flex-direction: column;
                gap: 15px;
            }
        }
        
        /* Page Styles */
        .page {
            display: none;
        }
        
        .page.active {
            display: block;
        }
        
        /* Scanner Canvas */
        #scannerCanvas {
            display: none;
        }
        
        /* Scanner Flash Effect */
        .flash-effect {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: white;
            opacity: 0;
            z-index: 10;
            pointer-events: none;
        }
        
        .flash {
            animation: flash 0.5s ease-out;
        }
        
        @keyframes flash {
            0% { opacity: 0.7; }
            100% { opacity: 0; }
        }
        
        /* Scanner Sound */
        .scanner-sound {
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Sidebar Navigasi -->
        <div class="sidebar">
            <div class="sidebar-header">
                <div class="logo">
                    <div class="logo-icon">K</div>
                    <div class="logo-text">KasPOS</div>
                </div>
                <div class="trial-info">
                    Saat ini anda trial, anda dapat hingga maksimal 10 produk
                </div>
            </div>
            
            <div class="menu">
                <div class="menu-section">
                    <div class="menu-title">Menu Utama</div>
                    <div class="menu-item active" data-page="products">
                        <i>🛍️</i>
                        <div class="menu-item-text">Tampilan Produk</div>
                    </div>
                    <div class="menu-item" data-page="add-product">
                        <i>➕</i>
                        <div class="menu-item-text">Tambah Produk</div>
                    </div>
                    <div class="menu-item" data-page="scanner">
                        <i>📷</i>
                        <div class="menu-item-text">Scanner Produk</div>
                    </div>
                    <div class="menu-item" data-page="cart">
                        <i>🛒</i>
                        <div class="menu-item-text">Keranjang Belanja</div>
                        <div class="badge" id="cartCount">0</div>
                    </div>
                </div>
                
                <div class="menu-divider"></div>
                
                <div class="menu-section">
                    <div class="menu-title">Transaksi</div>
                    <div class="menu-item" data-page="transactions">
                        <i>📋</i>
                        <div class="menu-item-text">Riwayat Transaksi</div>
                    </div>
                    <div class="menu-item" data-page="reports">
                        <i>📊</i>
                        <div class="menu-item-text">Laporan Transaksi</div>
                    </div>
                </div>
                
                <div class="menu-divider"></div>
                
                <div class="menu-section">
                    <div class="menu-title">Pengaturan</div>
                    <div class="menu-item" data-page="categories">
                        <i>📂</i>
                        <div class="menu-item-text">Kelola Kategori</div>
                    </div>
                    <div class="menu-item" data-page="settings">
                        <i>⚙️</i>
                        <div class="menu-item-text">Pengaturan</div>
                    </div>
                    <div class="menu-item" data-page="backup">
                        <i>💾</i>
                        <div class="menu-item-text">Backup Restore</div>
                    </div>
                </div>
                
                <div class="menu-divider"></div>
                
                <div class="menu-section">
                    <div class="menu-title">Lainnya</div>
                    <div class="menu-item" data-page="upgrade">
                        <i>🚀</i>
                        <div class="menu-item-text">Upgrade</div>
                        <div class="badge">PRO</div>
                    </div>
                    <div class="menu-item" data-page="feedback">
                        <i>📩</i>
                        <div class="menu-item-text">Kirim Masukan</div>
                    </div>
                    <div class="menu-item" data-page="rating">
                        <i>⭐</i>
                        <div class="menu-item-text">Beri Nilai Aplikasi</div>
                    </div>
                    <div class="menu-item" data-page="changelog">
                        <i>📝</i>
                        <div class="menu-item-text">Catatan Perubahan</div>
                    </div>
                </div>
                
                <div class="upgrade-section">
                    <div class="upgrade-title">Upgrade ke Versi Pro</div>
                    <div class="upgrade-desc">Dapatkan fitur lengkap tanpa batasan</div>
                    <button class="btn-upgrade" data-page="upgrade">UPGRADE SEKARANG</button>
                </div>
            </div>
        </div>
        
        <!-- Main Content -->
        <div class="main-content">
            <!-- Halaman Scanner -->
            <div class="page active" id="scanner-page">
                <div class="header">
                    <h2>Dashboard</h2>
                    <div class="user-info">
                        <span>Admin</span>
                    </div>
                </div>
                
                <div class="content-header">
                    <div class="page-title">Scanner Barcode Lengkap</div>
                </div>
                
                <div class="scanner-container">
                    <div class="scanner-header">
                        <div class="scanner-title">Pemindai Barcode & QR Code</div>
                        <button class="btn btn-primary" id="scannerHelpBtn">Bantuan</button>
                    </div>
                    
                    <div class="scanner-preview-container">
                        <div class="scanner-preview" id="scannerPreview">
                            <div id="interactive" class="viewport"></div>
                            <div class="scanner-overlay">
                                <div class="scanner-frame">
                                    <div class="scan-line"></div>
                                    <div class="scanner-corner-top-left"></div>
                                    <div class="scanner-corner-top-right"></div>
                                    <div class="scanner-corner-bottom-left"></div>
                                    <div class="scanner-corner-bottom-right"></div>
                                </div>
                                <div class="scanner-guide">Arahkan kode batang ke dalam area pemindaian</div>
                            </div>
                            <div class="flash-effect" id="flashEffect"></div>
                        </div>
                    </div>
                    
                    <div class="scanner-options">
                        <div class="option-group">
                            <label class="option-label">Kamera:</label>
                            <select class="option-select" id="cameraSelect">
                                <option value="environment">Kamera Belakang</option>
                                <option value="user">Kamera Depan</option>
                            </select>
                        </div>
                        
                        <div class="option-group">
                            <label class="option-label">Format:</label>
                            <select class="option-select" id="formatSelect">
                                <option value="all">Semua Format</option>
                                <option value="ean_13">EAN-13</option>
                                <option value="ean_8">EAN-8</option>
                                <option value="code_128">Code 128</option>
                                <option value="code_39">Code 39</option>
                                <option value="upc_a">UPC-A</option>
                                <option value="upc_e">UPC-E</option>
                            </select>
                        </div>
                        
                        <div class="option-group">
                            <label class="option-label">Flash:</label>
                            <button class="btn-scan btn-warning" id="toggleFlashBtn">
                                <i>⚡</i> Flash
                            </button>
                        </div>
                    </div>
                    
                    <div class="scanner-controls">
                        <button class="btn-scan" id="startCameraBtn">
                            <i>📷</i> Mulai Kamera
                        </button>
                        <button class="btn-scan btn-danger" id="stopCameraBtn" style="display: none;">
                            <i>⏹️</i> Hentikan Kamera
                        </button>
                        <button class="btn-scan btn-warning" id="switchCameraBtn" style="display: none;">
                            <i>🔄</i> Ganti Kamera
                        </button>
                        <button class="btn-scan btn-success" id="captureImageBtn" style="display: none;">
                            <i>📸</i> Ambil Gambar
                        </button>
                        <button class="btn-scan btn-secondary" id="manualInputBtn">
                            <i>⌨️</i> Input Manual
                        </button>
                    </div>
                    
                    <div id="scannerStatus" class="scanner-status info">
                        Klik "Mulai Kamera" untuk memulai pemindaian barcode
                    </div>
                    
                    <div class="scanner-result" id="scannerResult">
                        <h3>Barcode Berhasil Di-scan!</h3>
                        <p>Kode Batang:</p>
                        <div class="barcode-value" id="scannerBarcodeValue"></div>
                        <div id="scannerProductInfo"></div>
                        <div class="scanner-controls">
                            <button class="btn-scan btn-success" id="addToCartBtn">
                                <i>🛒</i> Tambah ke Keranjang
                            </button>
                            <button class="btn-scan btn-secondary" id="scanAgainBtn">
                                <i>🔁</i> Scan Lagi
                            </button>
                        </div>
                    </div>
                    
                    <div class="scanner-stats">
                        <div class="stat-item">
                            <div class="stat-value" id="scansToday">0</div>
                            <div class="stat-label">Scan Hari Ini</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value" id="successRate">0%</div>
                            <div class="stat-label">Tingkat Keberhasilan</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value" id="avgScanTime">0s</div>
                            <div class="stat-label">Rata-rata Waktu Scan</div>
                        </div>
                    </div>
                    
                    <div class="scanner-history">
                        <div class="history-title">Riwayat Scan Terbaru</div>
                        <div class="history-list" id="scannerHistory">
                            <div class="empty-state">
                                <i>📋</i>
                                <h4>Belum ada riwayat scan</h4>
                                <p>Scan barcode akan muncul di sini</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="recent-products">
                        <h3>Produk dengan Barcode</h3>
                        <div id="recentProductsList">
                            <div class="empty-state">
                                <i>📦</i>
                                <h4>Tidak ada produk dengan barcode</h4>
                                <p>Tambahkan produk dengan kode barcode untuk memudahkan scanning</p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="cart-button" id="scannerCartButton">
                    <i>🛒</i> Buka Keranjang (<span id="scannerCartCount">0</span>)
                </div>
                
                <!-- Canvas untuk pemrosesan gambar scanner -->
                <canvas id="scannerCanvas" style="display: none;"></canvas>
                
                <!-- Audio untuk suara scan berhasil -->
                <audio id="scanSuccessSound" class="scanner-sound">
                    <source src="https://assets.mixkit.co/sfx/preview/mixkit-correct-answer-tone-2870.mp3" type="audio/mpeg">
                </audio>
                
                <!-- Audio untuk suara scan gagal -->
                <audio id="scanErrorSound" class="scanner-sound">
                    <source src="https://assets.mixkit.co/sfx/preview/mixkit-wrong-answer-fail-notification-946.mp3" type="audio/mpeg">
                </audio>
            </div>
            
            <!-- Halaman lainnya -->
            <div class="page" id="products-page">
                <div class="content-header">
                    <div class="page-title">Daftar Produk</div>
                </div>
                <div class="empty-state">
                    <i>🛍️</i>
                    <h3>Halaman Daftar Produk</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="add-product-page">
                <div class="content-header">
                    <div class="page-title">Tambah Produk</div>
                </div>
                <div class="empty-state">
                    <i>➕</i>
                    <h3>Halaman Tambah Produk</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="cart-page">
                <div class="content-header">
                    <div class="page-title">Keranjang Belanja</div>
                </div>
                <div class="empty-state">
                    <i>🛒</i>
                    <h3>Halaman Keranjang Belanja</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="transactions-page">
                <div class="content-header">
                    <div class="page-title">Riwayat Transaksi</div>
                </div>
                <div class="empty-state">
                    <i>📋</i>
                    <h3>Halaman Riwayat Transaksi</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="reports-page">
                <div class="content-header">
                    <div class="page-title">Laporan Transaksi</div>
                </div>
                <div class="empty-state">
                    <i>📊</i>
                    <h3>Halaman Laporan Transaksi</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="categories-page">
                <div class="content-header">
                    <div class="page-title">Kelola Kategori</div>
                </div>
                <div class="empty-state">
                    <i>📂</i>
                    <h3>Halaman Kelola Kategori</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="settings-page">
                <div class="content-header">
                    <div class="page-title">Pengaturan</div>
                </div>
                <div class="empty-state">
                    <i>⚙️</i>
                    <h3>Halaman Pengaturan</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="backup-page">
                <div class="content-header">
                    <div class="page-title">Backup & Restore</div>
                </div>
                <div class="empty-state">
                    <i>💾</i>
                    <h3>Halaman Backup & Restore</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="upgrade-page">
                <div class="content-header">
                    <div class="page-title">Upgrade ke Versi Pro</div>
                </div>
                <div class="empty-state">
                    <i>🚀</i>
                    <h3>Halaman Upgrade</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="feedback-page">
                <div class="content-header">
                    <div class="page-title">Kirim Masukan</div>
                </div>
                <div class="empty-state">
                    <i>📩</i>
                    <h3>Halaman Kirim Masukan</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="rating-page">
                <div class="content-header">
                    <div class="page-title">Beri Nilai Aplikasi</div>
                </div>
                <div class="empty-state">
                    <i>⭐</i>
                    <h3>Halaman Beri Nilai Aplikasi</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
            
            <div class="page" id="changelog-page">
                <div class="content-header">
                    <div class="page-title">Catatan Perubahan</div>
                </div>
                <div class="empty-state">
                    <i>📝</i>
                    <h3>Halaman Catatan Perubahan</h3>
                    <p>Fitur ini akan segera tersedia</p>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Modal Bantuan Scanner -->
    <div class="scanner-modal" id="scannerHelpModal">
        <div class="scanner-modal-content">
            <div class="scanner-modal-header">
                <div class="scanner-modal-title">Bantuan Scanner Barcode</div>
                <button class="close-modal" id="closeHelpModal">&times;</button>
            </div>
            <div>
                <h3>Cara Menggunakan Scanner:</h3>
                <ol>
                    <li>Klik tombol "Mulai Kamera" untuk mengaktifkan kamera</li>
                    <li>Arahkan kamera ke barcode produk</li>
                    <li>Pastikan barcode berada dalam area pemindaian</li>
                    <li>Tunggu hingga barcode terdeteksi secara otomatis</li>
                    <li>Produk akan otomatis ditambahkan ke keranjang jika ditemukan</li>
                </ol>
                
                <h3>Tips untuk Hasil Terbaik:</h3>
                <ul>
                    <li>Pastikan pencahayaan cukup</li>
                    <li>Jaga jarak kamera dengan barcode (10-20 cm)</li>
                    <li>Hindari silau dan bayangan pada barcode</li>
                    <li>Gunakan flash jika kondisi gelap</li>
                    <li>Pastikan barcode tidak rusak atau terlipat</li>
                </ul>
                
                <h3>Format Barcode yang Didukung:</h3>
                <ul>
                    <li>EAN-13 (Standard retail barcode)</li>
                    <li>EAN-8</li>
                    <li>UPC-A</li>
                    <li>UPC-E</li>
                    <li>Code 128</li>
                    <li>Code 39</li>
                </ul>
            </div>
            
            <div class="form-actions">
                <button class="btn btn-secondary" id="closeHelpBtn">Tutup</button>
            </div>
        </div>
    </div>
    
    <!-- Modal Input Manual -->
    <div class="scanner-modal" id="manualInputModal">
        <div class="scanner-modal-content">
            <div class="scanner-modal-header">
                <div class="scanner-modal-title">Input Barcode Manual</div>
                <button class="close-modal" id="closeManualModal">&times;</button>
            </div>
            <div class="form-group">
                <label class="form-label" for="manualBarcode">Masukkan Kode Barcode</label>
                <input type="text" class="form-control" id="manualBarcode" placeholder="Contoh: 8992702020019" maxlength="20">
                <div class="form-hint">
                    Masukkan 13 digit kode barcode produk
                </div>
            </div>
            
            <div class="keyboard">
                <div class="keyboard-row">
                    <div class="key">1</div>
                    <div class="key">2</div>
                    <div class="key">3</div>
                    <div class="key">4</div>
                    <div class="key">5</div>
                    <div class="key">6</div>
                    <div class="key">7</div>
                    <div class="key">8</div>
                    <div class="key">9</div>
                    <div class="key">0</div>
                </div>
                <div class="keyboard-row">
                    <div class="key key-wide" id="clearManualBtn">Hapus</div>
                    <div class="key key-space" id="submitManualBtn">Submit</div>
                </div>
            </div>
            
            <div class="form-actions">
                <button class="btn btn-secondary" id="cancelManualBtn">Batal</button>
                <button class="btn btn-success" id="saveManualBtn">Simpan</button>
            </div>
        </div>
    </div>

    <script>
        // Data aplikasi
        let products = JSON.parse(localStorage.getItem('kaspos_products')) || [];
        let categories = JSON.parse(localStorage.getItem('kaspos_categories')) || [];
        let cart = JSON.parse(localStorage.getItem('kaspos_cart')) || [];
        let scannerHistory = JSON.parse(localStorage.getItem('kaspos_scanner_history')) || [];
        let scannerStats = JSON.parse(localStorage.getItem('kaspos_scanner_stats')) || {
            scansToday: 0,
            totalScans: 0,
            successfulScans: 0,
            totalScanTime: 0,
            lastScanDate: null
        };
        
        let currentPage = 'scanner';
        let isScanning = false;
        let currentFacingMode = 'environment';
        let quaggaScannerInstance = null;
        let flashEnabled = false;
        let stream = null;
        let currentScanStartTime = null;
        
        // DOM Elements
        const pages = document.querySelectorAll('.page');
        const menuItems = document.querySelectorAll('.menu-item');
        const startCameraBtn = document.getElementById('startCameraBtn');
        const stopCameraBtn = document.getElementById('stopCameraBtn');
        const switchCameraBtn = document.getElementById('switchCameraBtn');
        const captureImageBtn = document.getElementById('captureImageBtn');
        const toggleFlashBtn = document.getElementById('toggleFlashBtn');
        const manualInputBtn = document.getElementById('manualInputBtn');
        const scannerStatus = document.getElementById('scannerStatus');
        const scannerResult = document.getElementById('scannerResult');
        const scannerBarcodeValue = document.getElementById('scannerBarcodeValue');
        const scannerProductInfo = document.getElementById('scannerProductInfo');
        const addToCartBtn = document.getElementById('addToCartBtn');
        const scanAgainBtn = document.getElementById('scanAgainBtn');
        const scannerHelpBtn = document.getElementById('scannerHelpBtn');
        const scannerHelpModal = document.getElementById('scannerHelpModal');
        const closeHelpModal = document.getElementById('closeHelpModal');
        const closeHelpBtn = document.getElementById('closeHelpBtn');
        const manualInputModal = document.getElementById('manualInputModal');
        const closeManualModal = document.getElementById('closeManualModal');
        const cancelManualBtn = document.getElementById('cancelManualBtn');
        const saveManualBtn = document.getElementById('saveManualBtn');
        const manualBarcode = document.getElementById('manualBarcode');
        const clearManualBtn = document.getElementById('clearManualBtn');
        const submitManualBtn = document.getElementById('submitManualBtn');
        const cameraSelect = document.getElementById('cameraSelect');
        const formatSelect = document.getElementById('formatSelect');
        const flashEffect = document.getElementById('flashEffect');
        const scanSuccessSound = document.getElementById('scanSuccessSound');
        const scanErrorSound = document.getElementById('scanErrorSound');
        const scannerCartButton = document.getElementById('scannerCartButton');
        const scansTodayElement = document.getElementById('scansToday');
        const successRateElement = document.getElementById('successRate');
        const avgScanTimeElement = document.getElementById('avgScanTime');
        const scannerHistoryElement = document.getElementById('scannerHistory');
        const recentProductsList = document.getElementById('recentProductsList');
        
        // Inisialisasi aplikasi
        function initApp() {
            // Load data dari localStorage
            updateCart();
            updateScannerStats();
            renderScannerHistory();
            renderRecentProducts();
            setupEventListeners();
            
            // Tambahkan beberapa produk contoh jika belum ada
            if (products.length === 0) {
                addSampleProducts();
            }
            
            // Update stats hari ini jika tanggal berubah
            updateScansToday();
        }
        
        // Tambahkan produk contoh
        function addSampleProducts() {
            const sampleProducts = [
                {
                    id: '1',
                    title: 'Aqua',
                    description: '600ml',
                    category: 'minuman',
                    barcode: '8886008101059', // Barcode Aqua
                    price: 5000,
                    cost: 3000,
                    useImage: false,
                    useShapeColor: false,
                    image: '',
                    deleteImage: false,
                    stock: 10,
                    createdAt: new Date().toISOString()
                },
                {
                    id: '2',
                    title: 'Indomie Goreng',
                    description: '75g',
                    category: 'makanan',
                    barcode: '8992702020019', // Barcode Indomie
                    price: 3000,
                    cost: 2000,
                    useImage: false,
                    useShapeColor: false,
                    image: '',
                    deleteImage: false,
                    stock: 20,
                    createdAt: new Date().toISOString()
                },
                {
                    id: '3',
                    title: 'Pocari Sweat',
                    description: '500ml',
                    category: 'minuman',
                    barcode: '8999999035150', // Barcode Pocari Sweat
                    price: 8000,
                    cost: 5000,
                    useImage: false,
                    useShapeColor: false,
                    image: '',
                    deleteImage: false,
                    stock: 15,
                    createdAt: new Date().toISOString()
                },
                {
                    id: '4',
                    title: 'Roti Aoka',
                    description: '120g',
                    category: 'makanan',
                    barcode: '8997005530011', // Contoh barcode
                    price: 12000,
                    cost: 8000,
                    useImage: false,
                    useShapeColor: false,
                    image: '',
                    deleteImage: false,
                    stock: 8,
                    createdAt: new Date().toISOString()
                }
            ];
            
            products = [...products, ...sampleProducts];
            localStorage.setItem('kaspos_products', JSON.stringify(products));
            renderRecentProducts();
        }
        
        // Setup event listeners
        function setupEventListeners() {
            // Navigasi menu
            menuItems.forEach(item => {
                item.addEventListener('click', function() {
                    const pageId = this.getAttribute('data-page');
                    navigateToPage(pageId);
                });
            });
            
            // Scanner controls
            startCameraBtn.addEventListener('click', startCamera);
            stopCameraBtn.addEventListener('click', stopCamera);
            switchCameraBtn.addEventListener('click', switchCamera);
            captureImageBtn.addEventListener('click', captureImage);
            toggleFlashBtn.addEventListener('click', toggleFlash);
            manualInputBtn.addEventListener('click', openManualInput);
            addToCartBtn.addEventListener('click', addScannedToCart);
            scanAgainBtn.addEventListener('click', scanAgain);
            scannerHelpBtn.addEventListener('click', () => scannerHelpModal.style.display = 'flex');
            closeHelpModal.addEventListener('click', () => scannerHelpModal.style.display = 'none');
            closeHelpBtn.addEventListener('click', () => scannerHelpModal.style.display = 'none');
            
            // Manual input modal
            closeManualModal.addEventListener('click', () => manualInputModal.style.display = 'none');
            cancelManualBtn.addEventListener('click', () => manualInputModal.style.display = 'none');
            saveManualBtn.addEventListener('click', saveManualBarcode);
            clearManualBtn.addEventListener('click', () => manualBarcode.value = '');
            submitManualBtn.addEventListener('click', submitManualBarcode);
            
            // Keyboard untuk input manual
            const keyboardKeys = document.querySelectorAll('.key');
            keyboardKeys.forEach(key => {
                if (!key.id) { // Skip keys with IDs (clear, submit)
                    key.addEventListener('click', function() {
                        manualBarcode.value += this.textContent;
                    });
                }
            });
            
            // Options
            cameraSelect.addEventListener('change', function() {
                currentFacingMode = this.value;
                if (isScanning) {
                    stopCamera();
                    setTimeout(startCamera, 500);
                }
            });
            
            formatSelect.addEventListener('change', function() {
                if (isScanning) {
                    stopCamera();
                    setTimeout(startCamera, 500);
                }
            });
            
            // Cart button
            scannerCartButton.addEventListener('click', () => navigateToPage('cart'));
            
            // Event untuk membersihkan resource saat tab ditutup atau tidak aktif
            document.addEventListener('visibilitychange', function() {
                if (document.hidden && isScanning) {
                    stopCamera();
                }
            });

            window.addEventListener('beforeunload', function() {
                if (isScanning) {
                    stopCamera();
                }
            });
        }
        
        // Navigasi antar halaman
        function navigateToPage(pageId) {
            // Jika pindah dari halaman scanner, hentikan kamera
            if (currentPage === 'scanner' && pageId !== 'scanner') {
                stopCamera();
            }
            
            // Sembunyikan semua halaman
            pages.forEach(page => page.classList.remove('active'));
            
            // Tampilkan halaman yang dipilih
            document.getElementById(`${pageId}-page`).classList.add('active');
            
            // Update menu aktif
            menuItems.forEach(item => {
                if (item.getAttribute('data-page') === pageId) {
                    item.classList.add('active');
                } else {
                    item.classList.remove('active');
                }
            });
            
            // Update state halaman saat ini
            currentPage = pageId;
            
            // Load data halaman jika diperlukan
            if (pageId === 'scanner') {
                renderScannerHistory();
                renderRecentProducts();
            }
        }
        
        // Scanner functions
        function startCamera() {
            try {
                // Hentikan scanner sebelumnya jika ada
                stopCamera();

                // Update status
                scannerStatus.textContent = 'Menginisialisasi kamera...';
                scannerStatus.className = 'scanner-status info';

                // Konfigurasi Quagga
                const config = {
                    inputStream: {
                        name: "Live",
                        type: "LiveStream",
                        target: document.querySelector('#interactive'),
                        constraints: {
                            width: 800,
                            height: 600,
                            facingMode: currentFacingMode,
                            aspectRatio: { min: 1, max: 2 }
                        }
                    },
                    locator: {
                        patchSize: "medium",
                        halfSample: true
                    },
                    numOfWorkers: 4,
                    decoder: {
                        readers: getSelectedReaders()
                    },
                    locate: true
                };

                // Inisialisasi Quagga
                Quagga.init(config, function(err) {
                    if (err) {
                        console.error('Error initializing Quagga:', err);
                        scannerStatus.textContent = 'Tidak dapat mengakses kamera. Pastikan Anda memberikan izin akses kamera.';
                        scannerStatus.className = 'scanner-status error';
                        return;
                    }
                    
                    console.log('Quagga initialized successfully');
                    Quagga.start();
                    quaggaScannerInstance = Quagga;
                    
                    // Update UI
                    startCameraBtn.style.display = 'none';
                    stopCameraBtn.style.display = 'flex';
                    switchCameraBtn.style.display = 'flex';
                    captureImageBtn.style.display = 'flex';
                    isScanning = true;
                    currentScanStartTime = Date.now();

                    // Update status
                    scannerStatus.textContent = 'Kamera aktif - Arahkan kode batang ke area pemindaian';
                    scannerStatus.className = 'scanner-status info';
                });

                // Event ketika barcode terdeteksi
                Quagga.onDetected(function(result) {
                    const code = result.codeResult.code;
                    handleScannedCode(code);
                });
                
                // Event untuk proses scanning
                Quagga.onProcessed(function(result) {
                    if (result) {
                        drawDetectionOverlay(result);
                    }
                });
                
            } catch (err) {
                console.error('Error accessing camera:', err);
                scannerStatus.textContent = 'Tidak dapat mengakses kamera. Pastikan Anda memberikan izin akses kamera.';
                scannerStatus.className = 'scanner-status error';
            }
        }
        
        function stopCamera() {
            if (quaggaScannerInstance) {
                quaggaScannerInstance.stop();
                quaggaScannerInstance = null;
            }
            
            // Hapus video stream jika ada
            const container = document.getElementById('interactive');
            if (container) {
                container.innerHTML = ''; // Hapus video element
            }
            
            isScanning = false;
            scannerResult.style.display = 'none';
            flashEnabled = false;
            updateFlashButton();

            // Update status
            scannerStatus.textContent = 'Kamera dihentikan - Klik "Mulai Kamera" untuk memulai pemindaian';
            scannerStatus.className = 'scanner-status info';
            
            // Reset tombol
            startCameraBtn.style.display = 'flex';
            stopCameraBtn.style.display = 'none';
            switchCameraBtn.style.display = 'none';
            captureImageBtn.style.display = 'none';
        }
        
        function switchCamera() {
            // Switch between front and back camera
            currentFacingMode = currentFacingMode === 'environment' ? 'user' : 'environment';
            cameraSelect.value = currentFacingMode;
            stopCamera();
            setTimeout(startCamera, 500); // Restart camera with new facing mode
        }
        
        function captureImage() {
            // Trigger flash effect
            flashEffect.classList.add('flash');
            setTimeout(() => {
                flashEffect.classList.remove('flash');
            }, 500);
            
            // Simulate capture (in a real app, this would capture the current frame)
            scannerStatus.textContent = 'Gambar diambil - Menganalisis barcode...';
            scannerStatus.className = 'scanner-status warning';
            
            // Simulate analysis delay
            setTimeout(() => {
                scannerStatus.textContent = 'Tidak dapat menemukan barcode dalam gambar. Coba lagi dengan pencahayaan yang lebih baik.';
                scannerStatus.className = 'scanner-status error';
            }, 2000);
        }
        
        function toggleFlash() {
            flashEnabled = !flashEnabled;
            updateFlashButton();
            
            if (flashEnabled) {
                // In a real app, this would turn on the device flashlight
                scannerStatus.textContent = 'Flash diaktifkan';
            } else {
                scannerStatus.textContent = 'Flash dinonaktifkan';
            }
            
            // Show status for 2 seconds then revert
            setTimeout(() => {
                if (isScanning) {
                    scannerStatus.textContent = 'Kamera aktif - Arahkan kode batang ke area pemindaian';
                }
            }, 2000);
        }
        
        function updateFlashButton() {
            if (flashEnabled) {
                toggleFlashBtn.innerHTML = '<i>⚡</i> Flash ON';
                toggleFlashBtn.style.backgroundColor = '#f39c12';
            } else {
                toggleFlashBtn.innerHTML = '<i>⚡</i> Flash';
                toggleFlashBtn.style.backgroundColor = '';
            }
        }
        
        function getSelectedReaders() {
            const format = formatSelect.value;
            
            if (format === 'all') {
                return [
                    "ean_reader",
                    "ean_8_reader",
                    "code_128_reader",
                    "code_39_reader",
                    "upc_reader",
                    "upc_e_reader"
                ];
            } else {
                return [`${format}_reader`];
            }
        }
        
        function drawDetectionOverlay(result) {
            // This function would draw detection boxes on the video
            // For simplicity, we're skipping the detailed implementation
        }
        
        function handleScannedCode(code) {
            // Calculate scan time
            const scanTime = Date.now() - currentScanStartTime;
            
            // Update stats
            scannerStats.totalScans++;
            scannerStats.totalScanTime += scanTime;
            
            // Reset scan start time for next scan
            currentScanStartTime = Date.now();
            
            // Tampilkan hasil scan
            scannerBarcodeValue.textContent = code;
            scannerResult.style.display = 'block';
            
            // Find product by barcode
            const product = products.find(p => p.barcode === code);
            
            if (product) {
                // Product found
                scannerStats.successfulScans++;
                
                // Update product info
                scannerProductInfo.innerHTML = `
                    <div style="margin: 15px 0; padding: 10px; background: #e8f5e9; border-radius: 4px;">
                        <strong>${product.title}</strong><br>
                        ${product.description}<br>
                        <strong>Harga: Rp ${product.price.toLocaleString('id-ID')}</strong>
                    </div>
                `;
                
                // Update status
                scannerStatus.textContent = `Berhasil memindai: ${product.title}`;
                scannerStatus.className = 'scanner-status success';
                
                // Play success sound
                playSound('success');
                
                // Add to scan history
                addToScanHistory(code, product.title, true);
            } else {
                // Product not found
                scannerProductInfo.innerHTML = `
                    <div style="margin: 15px 0; padding: 10px; background: #ffebee; border-radius: 4px;">
                        <strong>Produk tidak ditemukan!</strong><br>
                        Kode barcode "${code}" tidak terdaftar dalam sistem.
                    </div>
                `;
                
                // Update status
                scannerStatus.textContent = `Kode "${code}" tidak ditemukan dalam database produk`;
                scannerStatus.className = 'scanner-status error';
                
                // Play error sound
                playSound('error');
                
                // Add to scan history
                addToScanHistory(code, 'Produk tidak ditemukan', false);
            }
            
            // Update scanner stats
            updateScannerStats();
            renderScannerHistory();
            
            // Save to localStorage
            localStorage.setItem('kaspos_scanner_stats', JSON.stringify(scannerStats));
            localStorage.setItem('kaspos_scanner_history', JSON.stringify(scannerHistory));
        }
        
        function playSound(type) {
            if (type === 'success') {
                scanSuccessSound.currentTime = 0;
                scanSuccessSound.play().catch(e => console.log('Audio play failed:', e));
            } else if (type === 'error') {
                scanErrorSound.currentTime = 0;
                scanErrorSound.play().catch(e => console.log('Audio play failed:', e));
            }
        }
        
        function addToScanHistory(barcode, productName, success) {
            const historyItem = {
                id: Date.now().toString(),
                barcode: barcode,
                productName: productName,
                success: success,
                timestamp: new Date().toISOString()
            };
            
            scannerHistory.unshift(historyItem);
            
            // Keep only last 20 items
            if (scannerHistory.length > 20) {
                scannerHistory = scannerHistory.slice(0, 20);
            }
            
            // Update scans today
            updateScansToday();
        }
        
        function updateScansToday() {
            const today = new Date().toDateString();
            
            // Reset scansToday if it's a new day
            if (scannerStats.lastScanDate !== today) {
                scannerStats.scansToday = 0;
                scannerStats.lastScanDate = today;
            }
            
            // Update scans today from history
            scannerStats.scansToday = scannerHistory.filter(item => {
                const itemDate = new Date(item.timestamp).toDateString();
                return itemDate === today;
            }).length;
            
            localStorage.setItem('kaspos_scanner_stats', JSON.stringify(scannerStats));
            updateScannerStats();
        }
        
        function updateScannerStats() {
            // Update scans today
            scansTodayElement.textContent = scannerStats.scansToday;
            
            // Calculate success rate
            const successRate = scannerStats.totalScans > 0 
                ? Math.round((scannerStats.successfulScans / scannerStats.totalScans) * 100) 
                : 0;
            successRateElement.textContent = `${successRate}%`;
            
            // Calculate average scan time
            const avgScanTime = scannerStats.totalScans > 0 
                ? (scannerStats.totalScanTime / scannerStats.totalScans / 1000).toFixed(1) 
                : 0;
            avgScanTimeElement.textContent = `${avgScanTime}s`;
        }
        
        function renderScannerHistory() {
            if (scannerHistory.length === 0) {
                scannerHistoryElement.innerHTML = `
                    <div class="empty-state">
                        <i>📋</i>
                        <h4>Belum ada riwayat scan</h4>
                        <p>Scan barcode akan muncul di sini</p>
                    </div>
                `;
            } else {
                scannerHistoryElement.innerHTML = `
                    ${scannerHistory.map(item => `
                        <div class="history-item">
                            <div>
                                <div class="history-barcode">${item.barcode}</div>
                                <div>${item.productName}</div>
                            </div>
                            <div>
                                <span style="color: ${item.success ? '#2ecc71' : '#e74c3c'}">
                                    ${item.success ? '✓' : '✗'}
                                </span>
                                <div class="history-time">${formatTime(new Date(item.timestamp))}</div>
                            </div>
                        </div>
                    `).join('')}
                `;
            }
        }
        
        function renderRecentProducts() {
            const productsWithBarcode = products.filter(p => p.barcode && p.barcode.length > 0);
            
            if (productsWithBarcode.length === 0) {
                recentProductsList.innerHTML = `
                    <div class="empty-state">
                        <i>📦</i>
                        <h4>Tidak ada produk dengan barcode</h4>
                        <p>Tambahkan produk dengan kode barcode untuk memudahkan scanning</p>
                    </div>
                `;
            } else {
                recentProductsList.innerHTML = `
                    <div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 15px;">
                        ${productsWithBarcode.slice(0, 6).map(product => `
                            <div class="product-card" style="cursor: default;">
                                <div class="product-name">${product.title}</div>
                                <div class="product-description">${product.description}</div>
                                <div class="product-price">Rp ${product.price.toLocaleString('id-ID')}</div>
                                <div class="product-barcode" style="font-size: 12px; color: #7f8c8d;">${product.barcode}</div>
                            </div>
                        `).join('')}
                    </div>
                `;
            }
        }
        
        function openManualInput() {
            manualInputModal.style.display = 'flex';
            manualBarcode.value = '';
            manualBarcode.focus();
        }
        
        function saveManualBarcode() {
            const barcode = manualBarcode.value.trim();
            
            if (barcode === '') {
                alert('Silakan masukkan kode barcode');
                return;
            }
            
            if (barcode.length < 8) {
                alert('Kode barcode harus minimal 8 digit');
                return;
            }
            
            handleScannedCode(barcode);
            manualInputModal.style.display = 'none';
        }
        
        function submitManualBarcode() {
            saveManualBarcode();
        }
        
        function addScannedToCart() {
            const barcode = scannerBarcodeValue.textContent;
            const product = products.find(p => p.barcode === barcode);
            
            if (product) {
                addToCart(product.id);
                scannerResult.style.display = 'none';
                
                // Show success message
                showNotification(`${product.title} berhasil ditambahkan ke keranjang`);
            }
        }
        
        function scanAgain() {
            scannerResult.style.display = 'none';
            currentScanStartTime = Date.now();
            
            // Reset status
            if (isScanning) {
                scannerStatus.textContent = 'Kamera aktif - Arahkan kode batang ke area pemindaian';
                scannerStatus.className = 'scanner-status info';
            }
        }
        
        // Keranjang belanja
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;
            
            const existingItem = cart.find(item => item.productId === productId);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({
                    productId: productId,
                    quantity: 1,
                    price: product.price,
                    name: product.title,
                    description: product.description
                });
            }
            
            updateCart();
        }
        
        function updateCart() {
            localStorage.setItem('kaspos_cart', JSON.stringify(cart));
            
            // Update cart count
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            document.getElementById('cartCount').textContent = totalItems;
            document.getElementById('scannerCartCount').textContent = totalItems;
        }
        
        // Utility functions
        function formatTime(date) {
            return date.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });
        }
        
        function showNotification(message) {
            // Create notification element
            const notification = document.createElement('div');
            notification.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                background-color: #2ecc71;
                color: white;
                padding: 12px 20px;
                border-radius: 4px;
                box-shadow: 0 2px 10px rgba(0,0,0,0.2);
                z-index: 3000;
                transition: opacity 0.3s;
            `;
            notification.textContent = message;
            
            document.body.appendChild(notification);
            
            // Remove notification after 3 seconds
            setTimeout(() => {
                notification.style.opacity = '0';
                setTimeout(() => {
                    document.body.removeChild(notification);
                }, 300);
            }, 3000);
        }
        
        // Inisialisasi aplikasi saat halaman dimuat
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
