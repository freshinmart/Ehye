<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kantong UMKM</title>
    <script src="https://cdn.jsdelivr.net/npm/quagga@0.12.1/dist/quagga.min.js"></script>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --success: #27ae60;
            --warning: #f39c12;
            --danger: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --gray: #95a5a6;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
        }
        
        .app-container {
            max-width: 480px;
            margin: 0 auto;
            background-color: white;
            min-height: 100vh;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            position: relative;
        }
        
        /* Header Styles */
        .app-header {
            background-color: var(--primary);
            color: white;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .app-header h1 {
            font-size: 1.2rem;
        }
        
        .user-profile {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .avatar {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            background-color: var(--secondary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }
        
        /* Navigation Styles */
        .app-nav {
            display: flex;
            justify-content: space-around;
            background-color: white;
            border-top: 1px solid #eee;
            position: sticky;
            bottom: 0;
            z-index: 100;
        }
        
        .nav-item {
            flex: 1;
            text-align: center;
            padding: 10px 5px;
            color: var(--gray);
            text-decoration: none;
            font-size: 0.8rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
        }
        
        .nav-item.active {
            color: var(--secondary);
        }
        
        .nav-item i {
            font-size: 1.2rem;
        }
        
        /* Page Container */
        .page {
            display: none;
            padding: 15px;
            min-height: calc(100vh - 120px);
            overflow-y: auto;
        }
        
        .page.active {
            display: block;
        }
        
        /* Card Styles */
        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            padding: 15px;
            margin-bottom: 15px;
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .card-title {
            font-weight: bold;
            font-size: 1.1rem;
        }
        
        /* Button Styles */
        .btn {
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            font-weight: bold;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
            transition: all 0.3s;
        }
        
        .btn-primary {
            background-color: var(--secondary);
            color: white;
        }
        
        .btn-success {
            background-color: var(--success);
            color: white;
        }
        
        .btn-warning {
            background-color: var(--warning);
            color: white;
        }
        
        .btn-danger {
            background-color: var(--danger);
            color: white;
        }
        
        .btn-block {
            display: block;
            width: 100%;
        }
        
        .btn-sm {
            padding: 5px 10px;
            font-size: 0.8rem;
        }
        
        /* Stats Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .stat-card {
            background-color: white;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            margin: 5px 0;
        }
        
        .stat-label {
            font-size: 0.8rem;
            color: var(--gray);
        }
        
        /* Product Grid */
        .product-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
        }
        
        .product-card {
            border: 1px solid #eee;
            border-radius: 8px;
            padding: 10px;
            text-align: center;
        }
        
        .product-image {
            width: 100%;
            height: 100px;
            background-color: #f9f9f9;
            border-radius: 5px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
        }
        
        .product-name {
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .product-price {
            color: var(--success);
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        /* Cart Styles */
        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #eee;
        }
        
        .cart-item-info {
            flex: 1;
        }
        
        .cart-item-name {
            font-weight: bold;
        }
        
        .cart-item-price {
            color: var(--gray);
            font-size: 0.9rem;
        }
        
        .cart-item-actions {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .quantity-control {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .quantity-btn {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            border: 1px solid #ddd;
            background-color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }
        
        .cart-total {
            display: flex;
            justify-content: space-between;
            padding: 15px 0;
            font-weight: bold;
            font-size: 1.2rem;
            border-top: 1px solid #eee;
            margin-top: 10px;
        }
        
        /* Form Styles */
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        
        .form-control {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        
        /* Table Styles */
        .table {
            width: 100%;
            border-collapse: collapse;
        }
        
        .table th, .table td {
            padding: 10px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }
        
        .table th {
            font-weight: bold;
            background-color: #f9f9f9;
        }
        
        /* QR Code Display */
        .qrcode-container {
            text-align: center;
            padding: 20px;
        }
        
        .qrcode {
            width: 200px;
            height: 200px;
            margin: 0 auto 20px;
            background-color: #f9f9f9;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid #ddd;
        }
        
        .countdown {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--warning);
            margin: 10px 0;
        }
        
        /* Status Badge */
        .badge {
            display: inline-block;
            padding: 3px 8px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: bold;
        }
        
        .badge-success {
            background-color: #d4edda;
            color: #155724;
        }
        
        .badge-warning {
            background-color: #fff3cd;
            color: #856404;
        }
        
        .badge-danger {
            background-color: #f8d7da;
            color: #721c24;
        }
        
        /* Notification */
        .notification {
            padding: 10px 15px;
            border-radius: 5px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .notification-warning {
            background-color: #fff3cd;
            color: #856404;
            border-left: 4px solid var(--warning);
        }
        
        /* Floating Cart Button */
        .floating-cart {
            position: fixed;
            bottom: 80px;
            right: 20px;
            width: 60px;
            height: 60px;
            background-color: var(--secondary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            cursor: pointer;
            z-index: 99;
        }
        
        .cart-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background-color: var(--danger);
            color: white;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.7rem;
        }
        
        /* Barcode Scanner */
        .barcode-scanner {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.8);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        
        .scanner-container {
            width: 90%;
            max-width: 400px;
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            text-align: center;
        }
        
        .scanner-placeholder {
            width: 100%;
            height: 250px;
            background-color: #f0f0f0;
            border: 2px dashed #ccc;
            margin-bottom: 20px;
            border-radius: 5px;
            overflow: hidden;
            position: relative;
        }
        
        #scanner-viewport {
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
            align-items: center;
            justify-content: center;
            background-color: rgba(0,0,0,0.5);
            color: white;
            font-size: 1.2rem;
        }
        
        .manual-barcode-input {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }
        
        /* Utility Classes */
        .text-center {
            text-align: center;
        }
        
        .text-right {
            text-align: right;
        }
        
        .mb-10 {
            margin-bottom: 10px;
        }
        
        .mb-15 {
            margin-bottom: 15px;
        }
        
        .mt-10 {
            margin-top: 10px;
        }
        
        .mt-15 {
            margin-top: 15px;
        }
        
        .hidden {
            display: none !important;
        }
        
        /* Modal Styles */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        
        .modal-content {
            width: 90%;
            max-width: 400px;
            max-height: 90vh;
            overflow-y: auto;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <header class="app-header">
            <h1 id="page-title">Kantong UMKM</h1>
            <div class="user-profile">
                <div class="avatar">KS</div>
            </div>
        </header>
        
        <!-- Main Content -->
        <main>
            <!-- Dashboard Page -->
            <section id="dashboard-page" class="page active">
                <div class="notification notification-warning">
                    <span>⚠️ Aktivasi QRIS: Maksimal H+2 registrasi</span>
                </div>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-label">Penjualan Hari Ini</div>
                        <div class="stat-value">Rp 350.000</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Transaksi</div>
                        <div class="stat-value">12</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Produk Terjual</div>
                        <div class="stat-value">24</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Saldo</div>
                        <div class="stat-value">Rp 4.000.000</div>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Pintasan Cepat</div>
                    </div>
                    <div class="stats-grid">
                        <button class="stat-card quick-action" data-page="pos-page">
                            <div>🛒</div>
                            <div>POS</div>
                        </button>
                        <button class="stat-card quick-action" data-page="history-page">
                            <div>📊</div>
                            <div>Riwayat</div>
                        </button>
                        <button class="stat-card quick-action" data-page="products-page">
                            <div>📦</div>
                            <div>Produk</div>
                        </button>
                        <button class="stat-card quick-action" data-page="ppob-page">
                            <div>⚡</div>
                            <div>PPOB</div>
                        </button>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Transaksi Terbaru</div>
                    </div>
                    <div class="transaction-list">
                        <div class="cart-item">
                            <div class="cart-item-info">
                                <div class="cart-item-name">Transaksi #001</div>
                                <div class="cart-item-price">Rp 75.000 • 10:30</div>
                            </div>
                            <span class="badge badge-success">Selesai</span>
                        </div>
                        <div class="cart-item">
                            <div class="cart-item-info">
                                <div class="cart-item-name">Transaksi #002</div>
                                <div class="cart-item-price">Rp 120.000 • 11:15</div>
                            </div>
                            <span class="badge badge-success">Selesai</span>
                        </div>
                    </div>
                </div>
            </section>
            
            <!-- POS Page -->
            <section id="pos-page" class="page">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Daftar Produk</div>
                        <button id="scan-barcode" class="btn btn-primary btn-sm">📷 Scan Barcode</button>
                    </div>
                    <div class="product-grid">
                        <!-- Products will be populated by JavaScript -->
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Keranjang</div>
                    </div>
                    <div class="cart-items">
                        <!-- Cart items will be populated by JavaScript -->
                    </div>
                    <div class="cart-total">
                        <span>Total:</span>
                        <span id="cart-total">Rp 0</span>
                    </div>
                    <button id="checkout-btn" class="btn btn-primary btn-block">Bayar</button>
                </div>
            </section>
            
            <!-- Payment Page -->
            <section id="payment-page" class="page">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Pembayaran</div>
                    </div>
                    <div class="cart-items">
                        <!-- Cart items will be populated by JavaScript -->
                    </div>
                    <div class="cart-total">
                        <span>Total:</span>
                        <span id="payment-total">Rp 0</span>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label">Metode Pembayaran</label>
                        <select id="payment-method" class="form-control">
                            <option value="cash">Tunai</option>
                            <option value="qris">QRIS</option>
                        </select>
                    </div>
                    
                    <div id="cash-payment" class="payment-section">
                        <div class="form-group">
                            <label class="form-label">Jumlah Uang Diterima</label>
                            <input type="number" id="cash-received" class="form-control" placeholder="Masukkan jumlah uang">
                        </div>
                        <div class="form-group">
                            <label class="form-label">Kembalian</label>
                            <input type="text" id="cash-change" class="form-control" readonly value="Rp 0">
                        </div>
                    </div>
                    
                    <div id="qris-payment" class="payment-section hidden">
                        <div class="qrcode-container">
                            <div class="qrcode">
                                [QR Code akan muncul di sini]
                            </div>
                            <div class="countdown" id="qris-countdown">02:00</div>
                            <p>Scan QR code di atas untuk pembayaran</p>
                            <button id="refresh-qr" class="btn btn-warning mt-10">Refresh QR</button>
                        </div>
                    </div>
                    
                    <button id="process-payment" class="btn btn-success btn-block mt-15">Proses Pembayaran</button>
                </div>
            </section>
            
            <!-- Receipt Page -->
            <section id="receipt-page" class="page">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Nota Pembayaran</div>
                    </div>
                    <div class="text-center mb-15">
                        <h2>Kantong UMKM</h2>
                        <p>Terima kasih atas pembelian Anda</p>
                    </div>
                    
                    <div id="receipt-details">
                        <!-- Receipt details will be populated by JavaScript -->
                    </div>
                    
                    <div class="text-center mt-15">
                        <button id="print-receipt" class="btn btn-primary">Cetak Nota</button>
                        <button id="new-transaction" class="btn btn-success">Transaksi Baru</button>
                    </div>
                </div>
            </section>
            
            <!-- Products Page -->
            <section id="products-page" class="page">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Daftar Produk</div>
                        <button id="add-product" class="btn btn-primary">Tambah</button>
                    </div>
                    <div class="product-list">
                        <!-- Product list will be populated by JavaScript -->
                    </div>
                </div>
            </section>
            
            <!-- History Page -->
            <section id="history-page" class="page">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Riwayat Transaksi</div>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Filter Periode</label>
                        <select id="period-filter" class="form-control">
                            <option value="daily">Harian</option>
                            <option value="weekly">Mingguan</option>
                            <option value="monthly">Bulanan</option>
                            <option value="yearly">Tahunan</option>
                        </select>
                    </div>
                    <table class="table">
                        <thead>
                            <tr>
                                <th>Tanggal</th>
                                <th>No. Invoice</th>
                                <th>Total</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody id="history-table">
                            <!-- History data will be populated by JavaScript -->
                        </tbody>
                    </table>
                </div>
            </section>
            
            <!-- Balance Page -->
            <section id="balance-page" class="page">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Saldo & Settlement</div>
                    </div>
                    <div class="stat-card text-center">
                        <div class="stat-label">Jumlah Saldo</div>
                        <div class="stat-value">Rp 4.000.000</div>
                    </div>
                    
                    <div class="card-header mt-15">
                        <div class="card-title">Riwayat Settlement</div>
                    </div>
                    <table class="table">
                        <thead>
                            <tr>
                                <th>Tanggal</th>
                                <th>Keterangan</th>
                                <th>Jumlah</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody id="settlement-table">
                            <!-- Settlement data will be populated by JavaScript -->
                        </tbody>
                    </table>
                </div>
            </section>
            
            <!-- PPOB Page -->
            <section id="ppob-page" class="page">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Layanan PPOB</div>
                    </div>
                    <div class="product-grid">
                        <div class="product-card ppob-service" data-service="pulsa">
                            <div class="product-image">📱</div>
                            <div class="product-name">Pulsa/Data</div>
                        </div>
                        <div class="product-card ppob-service" data-service="electricity">
                            <div class="product-image">⚡</div>
                            <div class="product-name">Token Listrik</div>
                        </div>
                        <div class="product-card ppob-service" data-service="ewallet">
                            <div class="product-image">💳</div>
                            <div class="product-name">Top-up E-Wallet</div>
                        </div>
                        <div class="product-card ppob-service" data-service="voucher">
                            <div class="product-image">🎮</div>
                            <div class="product-name">Voucher Game</div>
                        </div>
                    </div>
                </div>
                
                <div id="ppob-form" class="card hidden">
                    <div class="card-header">
                        <div class="card-title" id="ppob-service-title">Pembelian Pulsa</div>
                    </div>
                    <div class="form-group">
                        <label class="form-label" id="ppob-input-label">Nomor HP</label>
                        <input type="text" id="ppob-input" class="form-control" placeholder="Masukkan nomor">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Nominal</label>
                        <select id="ppob-amount" class="form-control">
                            <option value="5000">Rp 5.000</option>
                            <option value="10000">Rp 10.000</option>
                            <option value="20000">Rp 20.000</option>
                            <option value="50000">Rp 50.000</option>
                            <option value="100000">Rp 100.000</option>
                        </select>
                    </div>
                    <button id="process-ppob" class="btn btn-success btn-block">Proses</button>
                </div>
            </section>
            
            <!-- Settings Page -->
            <section id="settings-page" class="page">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">Pengaturan</div>
                    </div>
                    <div class="form-group">
                        <label class="form-label">Biaya Admin</label>
                        <input type="number" class="form-control" value="0">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Akun Bank</label>
                        <select class="form-control">
                            <option>BCA - 1234567890</option>
                            <option>Mandiri - 0987654321</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">PIN Baru</label>
                        <input type="password" class="form-control" placeholder="Masukkan PIN baru">
                    </div>
                    <button class="btn btn-primary btn-block">Simpan Pengaturan</button>
                </div>
                
                <div class="card mt-15">
                    <div class="card-header">
                        <div class="card-title">Bantuan</div>
                    </div>
                    <button id="contact-cs" class="btn btn-success btn-block">Hubungi Customer Service</button>
                </div>
            </section>
            
            <!-- Barcode Scanner Modal -->
            <div id="barcode-scanner" class="barcode-scanner hidden">
                <div class="scanner-container">
                    <h3 class="mb-15">Scan Barcode</h3>
                    <div class="scanner-placeholder">
                        <div id="scanner-viewport"></div>
                        <div id="scanner-overlay" class="scanner-overlay hidden">
                            Mengaktifkan kamera...
                        </div>
                    </div>
                    <p class="mb-15">Arahkan kamera ke barcode produk</p>
                    
                    <div class="manual-barcode-input">
                        <input type="text" id="manual-barcode" class="form-control" placeholder="Masukkan kode barcode manual">
                        <button id="add-by-barcode" class="btn btn-primary">Tambah</button>
                    </div>
                    
                    <button id="close-scanner" class="btn btn-danger btn-block mt-15">Tutup Scanner</button>
                </div>
            </div>
        </main>
        
        <!-- Floating Cart Button -->
        <div id="floating-cart" class="floating-cart hidden">
            🛒
            <div id="cart-badge" class="cart-badge">0</div>
        </div>
        
        <!-- Navigation -->
        <nav class="app-nav">
            <a href="#" class="nav-item active" data-page="dashboard-page">
                <span>🏠</span>
                <span>Dashboard</span>
            </a>
            <a href="#" class="nav-item" data-page="pos-page">
                <span>🛒</span>
                <span>POS</span>
            </a>
            <a href="#" class="nav-item" data-page="history-page">
                <span>📊</span>
                <span>Riwayat</span>
            </a>
            <a href="#" class="nav-item" data-page="products-page">
                <span>📦</span>
                <span>Produk</span>
            </a>
            <a href="#" class="nav-item" data-page="settings-page">
                <span>⚙️</span>
                <span>Pengaturan</span>
            </a>
        </nav>
    </div>

    <!-- Add/Edit Product Modal - DIPINDAHKAN KE BAWAH DAN DITAMBAHKAN CLASS HIDDEN -->
    <div id="product-modal" class="modal hidden">
        <div class="modal-content">
            <div class="card">
                <div class="card-header">
                    <div class="card-title" id="modal-title">Tambah Produk</div>
                    <button id="close-modal" class="btn btn-danger">✕</button>
                </div>
                <div class="form-group">
                    <label class="form-label">Nama Produk</label>
                    <input type="text" id="product-name" class="form-control" placeholder="Masukkan nama produk">
                </div>
                <div class="form-group">
                    <label class="form-label">Harga</label>
                    <input type="number" id="product-price" class="form-control" placeholder="Masukkan harga">
                </div>
                <div class="form-group">
                    <label class="form-label">Kode Barcode</label>
                    <input type="text" id="product-barcode" class="form-control" placeholder="Masukkan kode barcode">
                </div>
                <div class="form-group">
                    <label class="form-label">Kategori</label>
                    <input type="text" id="product-category" class="form-control" placeholder="Masukkan kategori">
                </div>
                <button id="save-product" class="btn btn-success btn-block">Simpan</button>
            </div>
        </div>
    </div>

    <script>
        // Sample data
        const sampleProducts = [
            { id: 1, name: "Kopi Hitam", price: 15000, category: "Minuman", barcode: "1234567890123" },
            { id: 2, name: "Roti Bakar", price: 12000, category: "Makanan", barcode: "1234567890124" },
            { id: 3, name: "Teh Manis", price: 8000, category: "Minuman", barcode: "1234567890125" },
            { id: 4, name: "Mie Goreng", price: 18000, category: "Makanan", barcode: "1234567890126" },
            { id: 5, name: "Jus Jeruk", price: 12000, category: "Minuman", barcode: "1234567890127" },
            { id: 6, name: "Pisang Goreng", price: 10000, category: "Makanan", barcode: "1234567890128" }
        ];
        
        const sampleHistory = [
            { id: 1, date: "2023-10-25 10:30", invoice: "INV-001", total: 75000, status: "Selesai" },
            { id: 2, date: "2023-10-25 11:15", invoice: "INV-002", total: 120000, status: "Selesai" },
            { id: 3, date: "2023-10-24 14:20", invoice: "INV-003", total: 45000, status: "Selesai" },
            { id: 4, date: "2023-10-24 16:45", invoice: "INV-004", total: 90000, status: "Selesai" }
        ];
        
        const sampleSettlement = [
            { id: 1, date: "2023-10-25", description: "Settlement QRIS", amount: 195000, status: "Sukses" },
            { id: 2, date: "2023-10-24", description: "Settlement QRIS", amount: 135000, status: "Sukses" },
            { id: 3, date: "2023-10-23", description: "Settlement QRIS", amount: 210000, status: "Sukses" }
        ];
        
        // Application state
        let currentCart = [];
        let currentTransaction = null;
        let editingProductId = null;
        let scannerActive = false;
        
        // DOM Elements
        const pages = document.querySelectorAll('.page');
        const navItems = document.querySelectorAll('.nav-item');
        const pageTitle = document.getElementById('page-title');
        const productGrid = document.querySelector('.product-grid');
        const cartItems = document.querySelector('.cart-items');
        const cartTotal = document.getElementById('cart-total');
        const paymentTotal = document.getElementById('payment-total');
        const checkoutBtn = document.getElementById('checkout-btn');
        const paymentMethod = document.getElementById('payment-method');
        const cashPayment = document.getElementById('cash-payment');
        const qrisPayment = document.getElementById('qris-payment');
        const cashReceived = document.getElementById('cash-received');
        const cashChange = document.getElementById('cash-change');
        const processPayment = document.getElementById('process-payment');
        const receiptDetails = document.getElementById('receipt-details');
        const productList = document.querySelector('.product-list');
        const addProductBtn = document.getElementById('add-product');
        const productModal = document.getElementById('product-modal');
        const closeModalBtn = document.getElementById('close-modal');
        const saveProductBtn = document.getElementById('save-product');
        const modalTitle = document.getElementById('modal-title');
        const productNameInput = document.getElementById('product-name');
        const productPriceInput = document.getElementById('product-price');
        const productBarcodeInput = document.getElementById('product-barcode');
        const productCategoryInput = document.getElementById('product-category');
        const historyTable = document.getElementById('history-table');
        const settlementTable = document.getElementById('settlement-table');
        const periodFilter = document.getElementById('period-filter');
        const ppobForm = document.getElementById('ppob-form');
        const ppobServiceTitle = document.getElementById('ppob-service-title');
        const ppobInputLabel = document.getElementById('ppob-input-label');
        const ppobInput = document.getElementById('ppob-input');
        const ppobAmount = document.getElementById('ppob-amount');
        const processPpobBtn = document.getElementById('process-ppob');
        const contactCsBtn = document.getElementById('contact-cs');
        const quickActions = document.querySelectorAll('.quick-action');
        const printReceiptBtn = document.getElementById('print-receipt');
        const newTransactionBtn = document.getElementById('new-transaction');
        const refreshQrBtn = document.getElementById('refresh-qr');
        const qrisCountdown = document.getElementById('qris-countdown');
        const floatingCart = document.getElementById('floating-cart');
        const cartBadge = document.getElementById('cart-badge');
        const scanBarcodeBtn = document.getElementById('scan-barcode');
        const barcodeScanner = document.getElementById('barcode-scanner');
        const closeScannerBtn = document.getElementById('close-scanner');
        const manualBarcodeInput = document.getElementById('manual-barcode');
        const addByBarcodeBtn = document.getElementById('add-by-barcode');
        const scannerViewport = document.getElementById('scanner-viewport');
        const scannerOverlay = document.getElementById('scanner-overlay');
        
        // Initialize the application
        function initApp() {
            renderProducts();
            renderProductList();
            renderHistory();
            renderSettlement();
            setupEventListeners();
            updateFloatingCart();
            
            // Pastikan modal tersembunyi saat aplikasi dimulai
            productModal.classList.add('hidden');
        }
        
        // Set up event listeners
        function setupEventListeners() {
            // Navigation
            navItems.forEach(item => {
                item.addEventListener('click', (e) => {
                    e.preventDefault();
                    const targetPage = item.getAttribute('data-page');
                    navigateToPage(targetPage);
                    
                    // Update active nav item
                    navItems.forEach(nav => nav.classList.remove('active'));
                    item.classList.add('active');
                    
                    // Show/hide floating cart
                    if (targetPage === 'pos-page') {
                        floatingCart.classList.remove('hidden');
                    } else {
                        floatingCart.classList.add('hidden');
                    }
                });
            });
            
            // Quick actions
            quickActions.forEach(action => {
                action.addEventListener('click', () => {
                    const targetPage = action.getAttribute('data-page');
                    navigateToPage(targetPage);
                    
                    // Update active nav item
                    navItems.forEach(nav => nav.classList.remove('active'));
                    document.querySelector(`.nav-item[data-page="${targetPage}"]`).classList.add('active');
                    
                    // Show/hide floating cart
                    if (targetPage === 'pos-page') {
                        floatingCart.classList.remove('hidden');
                    } else {
                        floatingCart.classList.add('hidden');
                    }
                });
            });
            
            // Checkout
            checkoutBtn.addEventListener('click', () => {
                if (currentCart.length === 0) {
                    alert('Keranjang kosong! Tambahkan produk terlebih dahulu.');
                    return;
                }
                
                navigateToPage('payment-page');
                renderPaymentCart();
                updatePaymentTotal();
            });
            
            // Payment method change
            paymentMethod.addEventListener('change', () => {
                const method = paymentMethod.value;
                
                if (method === 'cash') {
                    cashPayment.classList.remove('hidden');
                    qrisPayment.classList.add('hidden');
                } else {
                    cashPayment.classList.add('hidden');
                    qrisPayment.classList.remove('hidden');
                    startQRISCountdown();
                }
            });
            
            // Cash received input
            cashReceived.addEventListener('input', () => {
                const total = getCartTotal();
                const received = parseInt(cashReceived.value) || 0;
                const change = received - total;
                
                if (change >= 0) {
                    cashChange.value = `Rp ${change.toLocaleString()}`;
                } else {
                    cashChange.value = 'Uang kurang';
                }
            });
            
            // Process payment
            processPayment.addEventListener('click', () => {
                const method = paymentMethod.value;
                
                if (method === 'cash') {
                    const received = parseInt(cashReceived.value) || 0;
                    const total = getCartTotal();
                    
                    if (received < total) {
                        alert('Jumlah uang yang diterima kurang!');
                        return;
                    }
                    
                    processCashPayment();
                } else {
                    processQRISPayment();
                }
            });
            
            // Add product button
            addProductBtn.addEventListener('click', () => {
                openProductModal();
            });
            
            // Close modal
            closeModalBtn.addEventListener('click', () => {
                closeProductModal();
            });
            
            // Save product
            saveProductBtn.addEventListener('click', () => {
                saveProduct();
            });
            
            // Period filter change
            periodFilter.addEventListener('change', () => {
                renderHistory();
            });
            
            // PPOB services
            document.querySelectorAll('.ppob-service').forEach(service => {
                service.addEventListener('click', () => {
                    const serviceType = service.getAttribute('data-service');
                    openPPOBForm(serviceType);
                });
            });
            
            // Process PPOB
            processPpobBtn.addEventListener('click', () => {
                processPPOB();
            });
            
            // Contact CS
            contactCsBtn.addEventListener('click', () => {
                alert('Hubungi Customer Service Kantong UMKM di: 0800-123-4567');
            });
            
            // Print receipt
            printReceiptBtn.addEventListener('click', () => {
                window.print();
            });
            
            // New transaction
            newTransactionBtn.addEventListener('click', () => {
                currentCart = [];
                navigateToPage('pos-page');
                renderProducts();
                renderCart();
                updateFloatingCart();
                
                // Update active nav item
                navItems.forEach(nav => nav.classList.remove('active'));
                document.querySelector('.nav-item[data-page="pos-page"]').classList.add('active');
            });
            
            // Refresh QR
            refreshQrBtn.addEventListener('click', () => {
                startQRISCountdown();
            });
            
            // Floating cart click
            floatingCart.addEventListener('click', () => {
                // Scroll to cart section
                document.querySelector('#pos-page .card:last-child').scrollIntoView({ behavior: 'smooth' });
            });
            
            // Scan barcode button
            scanBarcodeBtn.addEventListener('click', () => {
                openBarcodeScanner();
            });
            
            // Close scanner
            closeScannerBtn.addEventListener('click', () => {
                closeBarcodeScanner();
            });
            
            // Add by barcode
            addByBarcodeBtn.addEventListener('click', () => {
                const barcode = manualBarcodeInput.value.trim();
                if (barcode) {
                    addProductByBarcode(barcode);
                    manualBarcodeInput.value = '';
                } else {
                    alert('Masukkan kode barcode terlebih dahulu!');
                }
            });
            
            // Manual barcode input enter key
            manualBarcodeInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    const barcode = manualBarcodeInput.value.trim();
                    if (barcode) {
                        addProductByBarcode(barcode);
                        manualBarcodeInput.value = '';
                    }
                }
            });
        }
        
        // Navigation function
        function navigateToPage(pageId) {
            pages.forEach(page => {
                page.classList.remove('active');
            });
            
            document.getElementById(pageId).classList.add('active');
            
            // Update page title
            const pageTitles = {
                'dashboard-page': 'Kantong UMKM',
                'pos-page': 'POS - Kantong UMKM',
                'payment-page': 'Pembayaran - Kantong UMKM',
                'receipt-page': 'Nota - Kantong UMKM',
                'products-page': 'Produk - Kantong UMKM',
                'history-page': 'Riwayat - Kantong UMKM',
                'balance-page': 'Saldo - Kantong UMKM',
                'ppob-page': 'PPOB - Kantong UMKM',
                'settings-page': 'Pengaturan - Kantong UMKM'
            };
            
            pageTitle.textContent = pageTitles[pageId] || 'Kantong UMKM';
            
            // Show/hide floating cart
            if (pageId === 'pos-page') {
                floatingCart.classList.remove('hidden');
            } else {
                floatingCart.classList.add('hidden');
            }
        }
        
        // Render products in POS page
        function renderProducts() {
            productGrid.innerHTML = '';
            
            sampleProducts.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'product-card';
                productCard.innerHTML = `
                    <div class="product-image">${product.category === 'Minuman' ? '🥤' : '🍕'}</div>
                    <div class="product-name">${product.name}</div>
                    <div class="product-price">Rp ${product.price.toLocaleString()}</div>
                    <button class="btn btn-primary add-to-cart" data-id="${product.id}">Tambah</button>
                `;
                
                productGrid.appendChild(productCard);
            });
            
            // Add event listeners to add-to-cart buttons
            document.querySelectorAll('.add-to-cart').forEach(button => {
                button.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.getAttribute('data-id'));
                    addToCart(productId);
                });
            });
        }
        
        // Add product to cart
        function addToCart(productId) {
            const product = sampleProducts.find(p => p.id === productId);
            
            if (!product) return;
            
            const existingItem = currentCart.find(item => item.id === productId);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                currentCart.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    quantity: 1
                });
            }
            
            renderCart();
            updateFloatingCart();
        }
        
        // Render cart
        function renderCart() {
            cartItems.innerHTML = '';
            
            if (currentCart.length === 0) {
                cartItems.innerHTML = '<p class="text-center">Keranjang kosong</p>';
                cartTotal.textContent = 'Rp 0';
                return;
            }
            
            currentCart.forEach(item => {
                const cartItem = document.createElement('div');
                cartItem.className = 'cart-item';
                cartItem.innerHTML = `
                    <div class="cart-item-info">
                        <div class="cart-item-name">${item.name}</div>
                        <div class="cart-item-price">Rp ${item.price.toLocaleString()} x ${item.quantity}</div>
                    </div>
                    <div class="cart-item-actions">
                        <div class="quantity-control">
                            <button class="quantity-btn decrease-quantity" data-id="${item.id}">-</button>
                            <span>${item.quantity}</span>
                            <button class="quantity-btn increase-quantity" data-id="${item.id}">+</button>
                        </div>
                        <button class="btn btn-danger remove-item" data-id="${item.id}">Hapus</button>
                    </div>
                `;
                
                cartItems.appendChild(cartItem);
            });
            
            // Add event listeners to quantity buttons
            document.querySelectorAll('.increase-quantity').forEach(button => {
                button.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.getAttribute('data-id'));
                    increaseQuantity(productId);
                });
            });
            
            document.querySelectorAll('.decrease-quantity').forEach(button => {
                button.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.getAttribute('data-id'));
                    decreaseQuantity(productId);
                });
            });
            
            document.querySelectorAll('.remove-item').forEach(button => {
                button.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.getAttribute('data-id'));
                    removeFromCart(productId);
                });
            });
            
            // Update total
            updateCartTotal();
        }
        
        // Render payment cart
        function renderPaymentCart() {
            const paymentCart = document.querySelector('#payment-page .cart-items');
            paymentCart.innerHTML = '';
            
            if (currentCart.length === 0) {
                paymentCart.innerHTML = '<p class="text-center">Keranjang kosong</p>';
                return;
            }
            
            currentCart.forEach(item => {
                const cartItem = document.createElement('div');
                cartItem.className = 'cart-item';
                cartItem.innerHTML = `
                    <div class="cart-item-info">
                        <div class="cart-item-name">${item.name}</div>
                        <div class="cart-item-price">Rp ${item.price.toLocaleString()} x ${item.quantity}</div>
                    </div>
                    <div class="cart-item-price">Rp ${(item.price * item.quantity).toLocaleString()}</div>
                `;
                
                paymentCart.appendChild(cartItem);
            });
        }
        
        // Increase quantity
        function increaseQuantity(productId) {
            const item = currentCart.find(item => item.id === productId);
            if (item) {
                item.quantity += 1;
                renderCart();
                updateFloatingCart();
            }
        }
        
        // Decrease quantity
        function decreaseQuantity(productId) {
            const item = currentCart.find(item => item.id === productId);
            if (item) {
                if (item.quantity > 1) {
                    item.quantity -= 1;
                } else {
                    removeFromCart(productId);
                    return;
                }
                renderCart();
                updateFloatingCart();
            }
        }
        
        // Remove from cart
        function removeFromCart(productId) {
            currentCart = currentCart.filter(item => item.id !== productId);
            renderCart();
            updateFloatingCart();
        }
        
        // Update cart total
        function updateCartTotal() {
            const total = getCartTotal();
            cartTotal.textContent = `Rp ${total.toLocaleString()}`;
        }
        
        // Update payment total
        function updatePaymentTotal() {
            const total = getCartTotal();
            paymentTotal.textContent = `Rp ${total.toLocaleString()}`;
        }
        
        // Get cart total
        function getCartTotal() {
            return currentCart.reduce((total, item) => total + (item.price * item.quantity), 0);
        }
        
        // Update floating cart badge
        function updateFloatingCart() {
            const totalItems = currentCart.reduce((total, item) => total + item.quantity, 0);
            cartBadge.textContent = totalItems;
        }
        
        // Process cash payment
        function processCashPayment() {
            const total = getCartTotal();
            const received = parseInt(cashReceived.value);
            const change = received - total;
            
            currentTransaction = {
                id: generateTransactionId(),
                date: new Date(),
                items: [...currentCart],
                total: total,
                method: 'cash',
                cashReceived: received,
                change: change,
                status: 'completed'
            };
            
            showReceipt();
        }
        
        // Process QRIS payment
        function processQRISPayment() {
            const total = getCartTotal();
            
            currentTransaction = {
                id: generateTransactionId(),
                date: new Date(),
                items: [...currentCart],
                total: total,
                method: 'qris',
                status: 'pending'
            };
            
            // Simulate QRIS payment success after 3 seconds
            setTimeout(() => {
                currentTransaction.status = 'completed';
                showReceipt();
            }, 3000);
            
            alert('Pembayaran QRIS sedang diproses...');
        }
        
        // Show receipt
        function showReceipt() {
            navigateToPage('receipt-page');
            
            const transaction = currentTransaction;
            let receiptHTML = `
                <div class="text-center mb-15">
                    <p><strong>No. Transaksi:</strong> ${transaction.id}</p>
                    <p><strong>Tanggal:</strong> ${formatDate(transaction.date)}</p>
                    <p><strong>Metode:</strong> ${transaction.method === 'cash' ? 'Tunai' : 'QRIS'}</p>
                </div>
                
                <table class="table">
                    <thead>
                        <tr>
                            <th>Produk</th>
                            <th>Qty</th>
                            <th>Harga</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            
            transaction.items.forEach(item => {
                receiptHTML += `
                    <tr>
                        <td>${item.name}</td>
                        <td>${item.quantity}</td>
                        <td>Rp ${(item.price * item.quantity).toLocaleString()}</td>
                    </tr>
                `;
            });
            
            receiptHTML += `
                    </tbody>
                    <tfoot>
                        <tr>
                            <td colspan="2"><strong>Total</strong></td>
                            <td><strong>Rp ${transaction.total.toLocaleString()}</strong></td>
                        </tr>
            `;
            
            if (transaction.method === 'cash') {
                receiptHTML += `
                        <tr>
                            <td colspan="2">Tunai Diterima</td>
                            <td>Rp ${transaction.cashReceived.toLocaleString()}</td>
                        </tr>
                        <tr>
                            <td colspan="2">Kembalian</td>
                            <td>Rp ${transaction.change.toLocaleString()}</td>
                        </tr>
                `;
            }
            
            receiptHTML += `
                    </tfoot>
                </table>
                
                <div class="text-center mt-15">
                    <p>Terima kasih telah berbelanja di Kantong UMKM</p>
                </div>
            `;
            
            receiptDetails.innerHTML = receiptHTML;
        }
        
        // Generate transaction ID
        function generateTransactionId() {
            const now = new Date();
            const dateStr = now.toISOString().slice(0,10).replace(/-/g, '');
            const timeStr = now.toTimeString().slice(0,8).replace(/:/g, '');
            return `TRX-${dateStr}-${timeStr}`;
        }
        
        // Format date
        function formatDate(date) {
            return new Date(date).toLocaleString('id-ID');
        }
        
        // Render product list in products page
        function renderProductList() {
            productList.innerHTML = '';
            
            sampleProducts.forEach(product => {
                const productItem = document.createElement('div');
                productItem.className = 'cart-item';
                productItem.innerHTML = `
                    <div class="cart-item-info">
                        <div class="cart-item-name">${product.name}</div>
                        <div class="cart-item-price">Rp ${product.price.toLocaleString()} • ${product.category}</div>
                        <div class="cart-item-price">Barcode: ${product.barcode}</div>
                    </div>
                    <div class="cart-item-actions">
                        <button class="btn btn-warning edit-product" data-id="${product.id}">Edit</button>
                        <button class="btn btn-danger delete-product" data-id="${product.id}">Hapus</button>
                    </div>
                `;
                
                productList.appendChild(productItem);
            });
            
            // Add event listeners to edit and delete buttons
            document.querySelectorAll('.edit-product').forEach(button => {
                button.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.getAttribute('data-id'));
                    editProduct(productId);
                });
            });
            
            document.querySelectorAll('.delete-product').forEach(button => {
                button.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.getAttribute('data-id'));
                    deleteProduct(productId);
                });
            });
        }
        
        // Open product modal
        function openProductModal(productId = null) {
            if (productId) {
                // Edit mode
                const product = sampleProducts.find(p => p.id === productId);
                if (product) {
                    modalTitle.textContent = 'Edit Produk';
                    productNameInput.value = product.name;
                    productPriceInput.value = product.price;
                    productBarcodeInput.value = product.barcode;
                    productCategoryInput.value = product.category;
                    editingProductId = productId;
                }
            } else {
                // Add mode
                modalTitle.textContent = 'Tambah Produk';
                productNameInput.value = '';
                productPriceInput.value = '';
                productBarcodeInput.value = '';
                productCategoryInput.value = '';
                editingProductId = null;
            }
            
            productModal.classList.remove('hidden');
        }
        
        // Close product modal
        function closeProductModal() {
            productModal.classList.add('hidden');
        }
        
        // Save product
        function saveProduct() {
            const name = productNameInput.value.trim();
            const price = parseInt(productPriceInput.value);
            const barcode = productBarcodeInput.value.trim();
            const category = productCategoryInput.value.trim();
            
            if (!name || !price || !barcode || !category) {
                alert('Harap isi semua field!');
                return;
            }
            
            if (editingProductId) {
                // Update existing product
                const productIndex = sampleProducts.findIndex(p => p.id === editingProductId);
                if (productIndex !== -1) {
                    sampleProducts[productIndex].name = name;
                    sampleProducts[productIndex].price = price;
                    sampleProducts[productIndex].barcode = barcode;
                    sampleProducts[productIndex].category = category;
                }
            } else {
                // Add new product
                const newId = sampleProducts.length > 0 ? Math.max(...sampleProducts.map(p => p.id)) + 1 : 1;
                sampleProducts.push({
                    id: newId,
                    name: name,
                    price: price,
                    barcode: barcode,
                    category: category
                });
            }
            
            closeProductModal();
            renderProductList();
            renderProducts();
        }
        
        // Edit product
        function editProduct(productId) {
            openProductModal(productId);
        }
        
        // Delete product
        function deleteProduct(productId) {
            if (confirm('Apakah Anda yakin ingin menghapus produk ini?')) {
                const productIndex = sampleProducts.findIndex(p => p.id === productId);
                if (productIndex !== -1) {
                    sampleProducts.splice(productIndex, 1);
                    renderProductList();
                    renderProducts();
                }
            }
        }
        
        // Render history
        function renderHistory() {
            historyTable.innerHTML = '';
            
            sampleHistory.forEach(transaction => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${transaction.date}</td>
                    <td>${transaction.invoice}</td>
                    <td>Rp ${transaction.total.toLocaleString()}</td>
                    <td><span class="badge badge-success">${transaction.status}</span></td>
                `;
                
                historyTable.appendChild(row);
            });
        }
        
        // Render settlement
        function renderSettlement() {
            settlementTable.innerHTML = '';
            
            sampleSettlement.forEach(settlement => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${settlement.date}</td>
                    <td>${settlement.description}</td>
                    <td>Rp ${settlement.amount.toLocaleString()}</td>
                    <td><span class="badge badge-success">${settlement.status}</span></td>
                `;
                
                settlementTable.appendChild(row);
            });
        }
        
        // Open PPOB form
        function openPPOBForm(serviceType) {
            ppobForm.classList.remove('hidden');
            
            const serviceConfig = {
                pulsa: { title: 'Pembelian Pulsa/Data', label: 'Nomor HP', placeholder: 'Masukkan nomor HP' },
                electricity: { title: 'Pembelian Token Listrik', label: 'ID Pelanggan', placeholder: 'Masukkan ID pelanggan' },
                ewallet: { title: 'Top-up E-Wallet', label: 'Nomor E-Wallet', placeholder: 'Masukkan nomor e-wallet' },
                voucher: { title: 'Pembelian Voucher Game', label: 'ID Game', placeholder: 'Masukkan ID game' }
            };
            
            const config = serviceConfig[serviceType] || serviceConfig.pulsa;
            
            ppobServiceTitle.textContent = config.title;
            ppobInputLabel.textContent = config.label;
            ppobInput.placeholder = config.placeholder;
        }
        
        // Process PPOB
        function processPPOB() {
            const input = ppobInput.value.trim();
            const amount = parseInt(ppobAmount.value);
            
            if (!input) {
                alert('Harap isi field yang diperlukan!');
                return;
            }
            
            // Simulate PPOB processing
            alert(`Transaksi PPOB sebesar Rp ${amount.toLocaleString()} sedang diproses...`);
            
            // Reset form
            ppobInput.value = '';
            ppobForm.classList.add('hidden');
        }
        
        // Start QRIS countdown
        function startQRISCountdown() {
            let timeLeft = 120; // 2 minutes in seconds
            
            const countdownInterval = setInterval(() => {
                const minutes = Math.floor(timeLeft / 60);
                const seconds = timeLeft % 60;
                
                qrisCountdown.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                
                timeLeft--;
                
                if (timeLeft < 0) {
                    clearInterval(countdownInterval);
                    qrisCountdown.textContent = '00:00';
                    alert('QR Code telah kadaluarsa. Silakan refresh untuk mendapatkan QR baru.');
                }
            }, 1000);
        }
        
        // Open barcode scanner
        function openBarcodeScanner() {
            barcodeScanner.classList.remove('hidden');
            manualBarcodeInput.value = '';
            startBarcodeScanner();
        }
        
        // Close barcode scanner
        function closeBarcodeScanner() {
            barcodeScanner.classList.add('hidden');
            stopBarcodeScanner();
        }
        
        // Start barcode scanner
        function startBarcodeScanner() {
            scannerActive = true;
            scannerOverlay.classList.remove('hidden');
            
            Quagga.init({
                inputStream: {
                    name: "Live",
                    type: "LiveStream",
                    target: scannerViewport,
                    constraints: {
                        width: 400,
                        height: 300,
                        facingMode: "environment" // Gunakan kamera belakang jika tersedia
                    }
                },
                decoder: {
                    readers: ["ean_reader", "ean_8_reader", "code_128_reader"]
                },
                locate: true
            }, function(err) {
                if (err) {
                    console.error(err);
                    scannerOverlay.textContent = "Gagal mengaktifkan kamera. Gunakan input manual.";
                    return;
                }
                scannerOverlay.classList.add('hidden');
                Quagga.start();
            });
            
            // Deteksi barcode
            Quagga.onDetected(function(result) {
                if (scannerActive) {
                    const code = result.codeResult.code;
                    addProductByBarcode(code);
                    stopBarcodeScanner();
                    closeBarcodeScanner();
                }
            });
        }
        
        // Stop barcode scanner
        function stopBarcodeScanner() {
            scannerActive = false;
            if (Quagga) {
                Quagga.stop();
            }
        }
        
        // Add product by barcode
        function addProductByBarcode(barcode) {
            const product = sampleProducts.find(p => p.barcode === barcode);
            
            if (product) {
                addToCart(product.id);
                alert(`Produk "${product.name}" berhasil ditambahkan ke keranjang!`);
            } else {
                alert('Produk dengan barcode tersebut tidak ditemukan!');
            }
        }
        
        // Initialize the app when DOM is loaded
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
