<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Akuntansi Warmindo (Clean UI)</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        /* === COLOR VARIABLES (CLEAN UI THEME) === */
        :root {
            --primary: #4f46e5;         /* Indigo / Modern Blue */
            --primary-hover: #4338ca;
            --bg-body: #f8fafc;         /* Very Light Gray/Blue */
            --bg-surface: #ffffff;      /* Pure White */
            --text-main: #0f172a;       /* Dark Slate */
            --text-muted: #64748b;      /* Slate Gray */
            --border-color: #e2e8f0;    /* Soft Border */
            --success: #10b981;
            --danger: #ef4444;
            --warning: #f59e0b;
            --radius-sm: 8px;
            --radius-md: 12px;
            --shadow-sm: 0 1px 2px 0 rgb(0 0 0 / 0.05);
            --shadow-card: 0 4px 6px -1px rgb(0 0 0 / 0.05), 0 2px 4px -2px rgb(0 0 0 / 0.05);
            --font-family: 'Inter', system-ui, -apple-system, sans-serif;
        }

        body { font-family: var(--font-family); margin: 0; background-color: var(--bg-body); color: var(--text-main); -webkit-font-smoothing: antialiased; }
        
        /* === STYLE HALAMAN LOGIN === */
        #login-screen { display: flex; justify-content: center; align-items: center; height: 100vh; background-color: var(--bg-body); }
        .login-box { background: var(--bg-surface); padding: 40px; border-radius: var(--radius-md); box-shadow: var(--shadow-card); width: 100%; max-width: 340px; border: 1px solid var(--border-color); text-align: center; }
        .login-box h2 { color: var(--text-main); margin-top: 0; margin-bottom: 24px; font-size: 24px; font-weight: 600;}
        .login-box input { margin-bottom: 16px; background-color: var(--bg-body); }
        .login-box button { width: 100%; padding: 12px; font-size: 15px; font-weight: 500; margin-top: 8px; }
        
        /* === APLIKASI UTAMA === */
        #app-wrapper { display: none; width: 100%; min-height: 100vh; }
        
        /* Sidebar Clean */
        .sidebar { width: 260px; background-color: var(--bg-surface); color: var(--text-main); height: 100vh; position: fixed; padding-top: 24px; z-index: 100; border-right: 1px solid var(--border-color); overflow-y: auto;}
        .sidebar h3 { text-align: center; margin-bottom: 32px; color: var(--primary); font-size: 20px; font-weight: 700; letter-spacing: -0.5px;}
        .sidebar a { display: block; color: var(--text-muted); padding: 12px 20px; margin: 4px 16px; text-decoration: none; border-radius: var(--radius-sm); font-weight: 500; cursor: pointer; transition: all 0.2s; font-size: 14px;}
        .sidebar a:hover { background-color: var(--bg-body); color: var(--text-main); }
        .sidebar a.active { background-color: #eef2ff; color: var(--primary); font-weight: 600; }
        .sidebar .logout-btn { color: var(--danger); margin-top: 24px; border-top: 1px solid var(--border-color); border-radius: 0; padding-top: 20px;}
        .sidebar .logout-btn:hover { background-color: transparent; color: #b91c1c; }
        
        .main-content { margin-left: 260px; padding: 32px 40px; width: calc(100% - 260px); box-sizing: border-box; }
        .section-view { display: none; animation: fadeIn 0.4s ease-out; }
        .section-view.active { display: block; }
        
        /* Typography & Layout */
        h2 { color: var(--text-main); margin-top: 0; font-size: 22px; font-weight: 600; margin-bottom: 24px; }
        h3 { color: var(--text-main); margin-top: 0; font-size: 16px; font-weight: 600; margin-bottom: 16px;}
        label { font-weight: 500; font-size: 13px; color: var(--text-muted); display: block; margin-top: 12px; margin-bottom: 6px; }
        
        /* Cards */
        .card { background-color: var(--bg-surface); padding: 24px 32px; margin-bottom: 24px; border-radius: var(--radius-md); box-shadow: var(--shadow-sm); border: 1px solid var(--border-color); }
        
        /* Inputs & Buttons */
        input[type="text"], input[type="number"], input[type="date"], input[type="password"], select, textarea { width: 100%; padding: 10px 14px; margin: 0 0 16px 0; border: 1px solid var(--border-color); border-radius: var(--radius-sm); box-sizing: border-box; font-family: var(--font-family); font-size: 14px; color: var(--text-main); transition: 0.2s; background: var(--bg-surface); outline: none;}
        input:focus, select:focus, textarea:focus { border-color: var(--primary); box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.15); }
        .search-bar { width: 100%; max-width: 320px; margin-bottom: 0; padding-left: 36px; background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="%2394a3b8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>'); background-repeat: no-repeat; background-position: 12px center; }
        
        button { background-color: var(--primary); color: white; padding: 10px 20px; border: none; border-radius: var(--radius-sm); cursor: pointer; font-size: 14px; font-weight: 500; transition: 0.2s; display: inline-flex; justify-content: center; align-items: center;}
        button:hover { background-color: var(--primary-hover); transform: translateY(-1px); box-shadow: var(--shadow-sm); }
        button.btn-danger { background-color: var(--danger); }
        button.btn-danger:hover { background-color: #dc2626; }
        button.btn-warning { background-color: var(--warning); color: #fff; }
        button.btn-warning:hover { background-color: #d97706; }
        button.btn-info { background-color: var(--bg-body); color: var(--text-main); border: 1px solid var(--border-color); }
        button.btn-info:hover { background-color: var(--border-color); }
        
        /* Minimalist Tables */
        table { width: 100%; border-collapse: collapse; margin: 10px 0; font-size: 14px; }
        th, td { padding: 14px 16px; text-align: left; border-bottom: 1px solid var(--border-color); }
        th { background-color: transparent; color: var(--text-muted); font-weight: 600; font-size: 12px; text-transform: uppercase; letter-spacing: 0.5px; border-bottom: 2px solid var(--border-color);}
        tr:last-child td { border-bottom: none; }
        tr:hover td { background-color: #f8fafc; }
        
        /* Layout Structure */
        .flex-container { display: flex; gap: 24px; flex-wrap: wrap; }
        .flex-child { flex: 1; min-width: 250px; }
        
        /* Modern Badges */
        .badge { padding: 4px 12px; border-radius: 9999px; font-size: 12px; font-weight: 600; display: inline-block;}
        .badge-masuk { background-color: #d1fae5; color: #065f46; }
        .badge-keluar { background-color: #fee2e2; color: #991b1b; }
        .badge-opname { background-color: #e0e7ff; color: #3730a3; }
        
        /* Clean Dashboard Stats */
        .stat-box { flex: 1; background: var(--bg-surface); padding: 24px; border-radius: var(--radius-md); box-shadow: var(--shadow-sm); border: 1px solid var(--border-color); }
        .stat-box h3 { color: var(--text-muted); margin: 0 0 8px 0; font-size: 14px; font-weight: 500; }
        .stat-box h1 { margin: 0; font-size: 32px; font-weight: 700; color: var(--text-main); }
        .border-blue { border-left: 4px solid var(--primary); }
        .border-red { border-left: 4px solid var(--danger); }
        .border-green { border-left: 4px solid var(--success); }

        /* Responsive Mobile Layout */
        @media (max-width: 768px) {
            #app-wrapper { flex-direction: column; }
            .sidebar { width: 100%; height: auto; position: relative; display: flex; flex-wrap: nowrap; overflow-x: auto; padding: 12px 0; border-right: none; border-bottom: 1px solid var(--border-color);}
            .sidebar h3 { display: none; } 
            .sidebar a { padding: 8px 16px; margin: 0 4px; font-size: 13px; white-space: nowrap; border-radius: 20px; background: var(--bg-body);}
            .sidebar a.active { background-color: var(--primary); color: white; }
            .sidebar .logout-btn { margin-top: 0; border-top: none; padding-top: 8px; color: var(--danger); }
            .main-content { margin-left: 0; width: 100%; padding: 20px; }
            .card { padding: 20px; }
        }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="login-screen">
        <div class="login-box">
            <h2 style="color: var(--primary);">Warmindo App</h2>
            <p style="color: var(--text-muted); font-size: 14px; margin-top: -15px; margin-bottom: 25px;">Silakan masuk ke akun Anda</p>
            <input type="text" id="loginUsername" placeholder="Username">
            <input type="password" id="loginPassword" placeholder="Password" onkeypress="if(event.key === 'Enter') prosesLogin()">
            <button onclick="prosesLogin()">Masuk Sistem</button>
            <p style="font-size: 12px; color: var(--text-muted); margin-top: 24px;">
                Akses demo: <b>admin</b> / <b>user</b>
            </p>
        </div>
    </div>

    <div id="app-wrapper">
        <div class="sidebar">
            <h3 id="app-title">🍜 Warmindo</h3>
            <a href="javascript:void(0)" onclick="showSection('dashboard')" id="nav-dashboard" class="active">Dashboard</a>
            <a href="javascript:void(0)" onclick="showSection('master-bahan')" id="nav-master-bahan">Data Master</a>
            <a href="javascript:void(0)" onclick="showSection('pembelian')" id="nav-pembelian">Barang Masuk</a>
            <a href="javascript:void(0)" onclick="showSection('pemakaian')" id="nav-pemakaian">Barang Keluar</a>
            <a href="javascript:void(0)" onclick="showSection('stok-opname')" id="nav-stok-opname">Stok Opname</a>
            <a href="javascript:void(0)" onclick="showSection('laporan')" id="nav-laporan">Laporan & Export</a>
            <a href="javascript:void(0)" onclick="showSection('riwayat')" id="nav-riwayat">Riwayat Data</a>
            
            <a href="javascript:void(0)" onclick="prosesLogout()" class="logout-btn">Log Out</a>
        </div>

        <div class="main-content">

            <div id="dashboard" class="section-view active">
                <h2>Ringkasan Sistem</h2>
                <div class="flex-container">
                    <div class="stat-box border-blue">
                        <h3>Total Varian Bahan Baku</h3>
                        <h1 id="dashTotalItem">0</h1>
                    </div>
                    <div class="stat-box border-red">
                        <h3>Peringatan Stok Kritis</h3>
                        <h1 id="dashStokKritis">0</h1>
                    </div>
                    <div class="stat-box border-green">
                        <h3>Total Transaksi Tercatat</h3>
                        <h1 id="dashTotalTransaksi">0</h1>
                    </div>
                </div>
                <div class="card" style="margin-top: 24px; background-color: #eef2ff; border: none;">
                    <h3 style="color: var(--primary);">Halo, <span id="display-user" style="text-transform:capitalize;"></span>! 👋</h3>
                    <p style="color: var(--text-muted); font-size: 14px; margin-bottom: 0;">Seluruh data diolah dan disimpan secara aman dan instan di dalam memori lokal browser Anda.</p>
                </div>
            </div>

            <div id="master-bahan" class="section-view">
                <h2>Kelola Data Master Bahan</h2>
                <div class="flex-container">
                    <div class="card flex-child">
                        <h3>Tambah/Edit Master Data</h3>
                        <label>Kode Bahan Baku:</label>
                        <input type="text" id="inputKode" placeholder="Contoh: BBK-001">
                        
                        <label>Nama Bahan Baku:</label>
                        <input type="text" id="inputNama" placeholder="Contoh: Tepung Terigu">
                        
                        <div class="flex-container" style="gap: 15px;">
                            <div class="flex-child">
                                <label>Satuan:</label>
                                <select id="inputSatuan">
                                    <option value="Kg">Kg</option>
                                    <option value="Pcs">Pcs</option>
                                    <option value="Ikat">Ikat</option>
                                    <option value="Liter">Liter</option>
                                    <option value="Dus">Dus</option>
                                    <option value="Bungkus">Bungkus</option>
                                </select>
                            </div>
                            <div class="flex-child">
                                <label>Kategori:</label>
                                <select id="inputKategori">
                                    <option value="Bahan Kering">Bahan Kering</option>
                                    <option value="Bahan Segar">Bahan Segar</option>
                                    <option value="Bumbu">Bumbu</option>
                                    <option value="Minuman">Minuman</option>
                                </select>
                            </div>
                        </div>

                        <label>Stok Awal (Opsional):</label>
                        <input type="number" id="inputStok" value="0">
                        
                        <label>Deskripsi Keterangan:</label>
                        <textarea id="inputDeskripsi" rows="2" placeholder="Catatan opsional..."></textarea>
                        
                        <div style="display: flex; gap: 10px; margin-top: 10px;">
                            <button onclick="simpanBahanBaku()" style="flex: 2;">Simpan Data</button>
                            <button class="btn-info" onclick="resetFormMaster()" style="flex: 1;">Reset</button>
                        </div>
                    </div>

                    <div class="card flex-child" style="flex: 1.5;">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                            <h3 style="margin: 0;">Daftar Bahan Baku</h3>
                            <input type="text" class="search-bar" id="searchMaster" placeholder="Cari data..." onkeyup="cariData('searchMaster', 'tabelMasterBahan')">
                        </div>
                        
                        <div style="overflow-x: auto;">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Kode</th>
                                        <th>Nama</th>
                                        <th>Kategori</th>
                                        <th>Satuan</th>
                                        <th>Stok</th>
                                        <th>Aksi</th>
                                    </tr>
                                </thead>
                                <tbody id="tabelMasterBahan"></tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <div id="pembelian" class="section-view">
                <h2>Pencatatan Barang Masuk</h2>
                <div class="card">
                    <div class="flex-container">
                        <div class="flex-child">
                            <label>Tanggal Transaksi:</label>
                            <input type="date" id="tglPembelian">
                            <label>Pilih Bahan Baku:</label>
                            <select id="selectBahanPembelian"></select>
                            <label>Jumlah (Qty) Masuk:</label>
                            <input type="number" id="jumlahPembelian" placeholder="0">
                        </div>
                        <div class="flex-child">
                            <label>No. Nota / Bukti (Bila ada):</label>
                            <input type="text" id="notaPembelian" placeholder="Contoh: INV-001">
                            <label>Supplier / Vendor:</label>
                            <input type="text" id="supplierPembelian" placeholder="Contoh: Pasar Induk / Agen">
                            <label>Total Harga Beli (Rp):</label>
                            <input type="number" id="hargaPembelian" placeholder="0">
                        </div>
                    </div>
                    <button onclick="simpanPembelian()" style="width: 100%; margin-top: 10px;">Simpan Barang Masuk</button>
                </div>
            </div>

            <div id="pemakaian" class="section-view">
                <h2>Pencatatan Barang Keluar</h2>
                <div class="card">
                    <div class="flex-container">
                        <div class="flex-child">
                            <label>Tanggal Pemakaian:</label>
                            <input type="date" id="tglPemakaian">
                            <label>Tujuan Pemakaian:</label>
                            <select id="unitPemakaian">
                                <option value="Dapur Utama">Dapur Utama (Dimasak)</option>
                                <option value="Stand Depan">Stand Minuman</option>
                                <option value="Buang/Rusak">Dibuang / Basi / Rusak</option>
                            </select>
                        </div>
                        <div class="flex-child">
                            <label>Pilih Bahan Baku:</label>
                            <select id="selectBahanPemakaian"></select>
                            <label>Jumlah (Qty) Keluar:</label>
                            <input type="number" id="jumlahPemakaian" placeholder="0">
                        </div>
                    </div>
                    <button class="btn-warning" style="width:100%; margin-top: 10px;" onclick="simpanPemakaian()">Catat Pengurangan Stok</button>
                </div>
            </div>

            <div id="stok-opname" class="section-view">
                <h2>Stok Opname Sistem vs Fisik</h2>
                <div class="card">
                    <p style="color: var(--text-muted); font-size: 14px; margin-bottom: 20px;">Ketik jumlah stok fisik aktual yang ada di rak/gudang pada kolom <b>Stok Fisik</b> lalu klik sesuaikan. Sistem akan mencatat selisihnya otomatis.</p>
                    <div style="overflow-x: auto;">
                        <table>
                            <thead>
                                <tr>
                                    <th>Kode</th>
                                    <th>Nama Bahan Baku</th>
                                    <th>Stok Sistem</th>
                                    <th style="width: 120px;">Stok Fisik</th>
                                    <th>Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="tabelOpname"></tbody>
                        </table>
                    </div>
                </div>
            </div>

            <div id="laporan" class="section-view">
                <h2>Laporan Stok & Export</h2>
                <div class="card">
                    <div style="margin-bottom: 24px; display: flex; gap: 12px;">
                        <button class="btn-info" onclick="window.print()">Cetak PDF</button>
                        <button onclick="exportCSV()" style="background-color: var(--success);">Export ke Excel (CSV)</button>
                    </div>
                    
                    <div style="overflow-x: auto;">
                        <table>
                            <thead>
                                <tr>
                                    <th>Kode</th>
                                    <th>Kategori</th>
                                    <th>Nama Bahan</th>
                                    <th>Satuan</th>
                                    <th>Saldo Stok Akhir</th>
                                    <th>Status Sistem</th>
                                </tr>
                            </thead>
                            <tbody id="tabelLaporanStok"></tbody>
                        </table>
                    </div>
                </div>
            </div>

            <div id="riwayat" class="section-view">
                <h2>Log Riwayat Transaksi</h2>
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; flex-wrap: wrap; gap: 15px;">
                        <input type="text" class="search-bar" id="searchRiwayat" placeholder="Cari log transaksi..." onkeyup="cariData('searchRiwayat', 'tabelRiwayat')">
                        <button class="btn-info" style="color: var(--danger); border-color: var(--danger);" onclick="hapusRiwayat()">Bersihkan Log</button>
                    </div>
                    
                    <div style="overflow-x: auto;">
                        <table>
                            <thead>
                                <tr>
                                    <th>Waktu Transaksi</th>
                                    <th>Jenis Log</th>
                                    <th>Detail Bahan</th>
                                    <th>Kuantitas</th>
                                    <th>Keterangan / Nilai</th>
                                </tr>
                            </thead>
                            <tbody id="tabelRiwayat"></tbody>
                        </table>
                    </div>
                </div>
            </div>

        </div>
    </div> <script>
        // === INISIALISASI DATABASE LOCALSTORAGE ===
        let dbBahanBaku = [];
        let dbRiwayat = [];
        
        try {
            const rawBahan = localStorage.getItem('warmindo_bahan_baku');
            dbBahanBaku = rawBahan ? JSON.parse(rawBahan) : [];
            if (!Array.isArray(dbBahanBaku)) dbBahanBaku = [];
        } catch (e) { console.error("Error parsing", e); }

        try {
            const rawRiwayat = localStorage.getItem('warmindo_riwayat');
            dbRiwayat = rawRiwayat ? JSON.parse(rawRiwayat) : [];
            if (!Array.isArray(dbRiwayat)) dbRiwayat = [];
        } catch (e) { console.error("Error parsing", e); }

        try {
            const today = new Date().toISOString().split('T')[0];
            if(document.getElementById('tglPembelian')) document.getElementById('tglPembelian').value = today;
            if(document.getElementById('tglPemakaian')) document.getElementById('tglPemakaian').value = today;
        } catch(e) {}

        const formatRupiah = (angka) => {
            return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR', minimumFractionDigits: 0 }).format(angka);
        }

        // === FUNGSI AUTENTIKASI (LOGIN & LOGOUT) ===
        function checkAuth() {
            const user = localStorage.getItem('warmindo_active_user');
            if(user) {
                document.getElementById('login-screen').style.display = 'none';
                document.getElementById('app-wrapper').style.display = 'flex';
                document.getElementById('display-user').innerText = user;
                renderData();
            } else {
                document.getElementById('login-screen').style.display = 'flex';
                document.getElementById('app-wrapper').style.display = 'none';
            }
        }

        function prosesLogin() {
            const user = document.getElementById('loginUsername').value.trim();
            const pass = document.getElementById('loginPassword').value.trim();
            
            if((user === 'admin' && pass === 'admin') || (user === 'user' && pass === 'user')) {
                localStorage.setItem('warmindo_active_user', user);
                document.getElementById('loginUsername').value = '';
                document.getElementById('loginPassword').value = '';
                checkAuth();
            } else {
                alert("Kredensial tidak valid! Gunakan 'admin' atau 'user'.");
            }
        }

        function prosesLogout() {
            if(confirm("Keluar dari sesi saat ini?")) {
                localStorage.removeItem('warmindo_active_user');
                checkAuth();
            }
        }

        // === FUNGSI NAVIGASI ===
        function showSection(sectionId) {
            document.querySelectorAll('.section-view').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.sidebar a').forEach(link => link.classList.remove('active'));
            
            const selectedSection = document.getElementById(sectionId);
            const selectedNav = document.getElementById('nav-' + sectionId);
            
            if(selectedSection) selectedSection.classList.add('active');
            if(selectedNav) selectedNav.classList.add('active');
            
            renderData();
        }

        // === FITUR PENCARIAN & EXPORT ===
        function cariData(inputId, tbodyId) {
            let filter = document.getElementById(inputId).value.toLowerCase();
            let trs = document.getElementById(tbodyId).getElementsByTagName('tr');
            
            for (let i = 0; i < trs.length; i++) {
                if (trs[i].cells.length === 1) continue; 
                let textContent = trs[i].innerText.toLowerCase();
                trs[i].style.display = (textContent.indexOf(filter) > -1) ? "" : "none";
            }
        }

        function exportCSV() {
            if(dbBahanBaku.length === 0) return alert("Belum ada data untuk diexport.");
            
            let csvContent = "data:text/csv;charset=utf-8,Kode,Nama Bahan,Kategori,Satuan,Sisa Stok\n";
            dbBahanBaku.forEach(row => {
                const kategoriSafe = row.kategori || '-';
                csvContent += `${row.kode},${row.nama},${kategoriSafe},${row.satuan},${row.stok}\n`;
            });

            let encodedUri = encodeURI(csvContent);
            let link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `Laporan_Stok_Warmindo.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        // === CRUD MASTER DATA ===
        function simpanBahanBaku() {
            const kode = document.getElementById('inputKode').value.trim();
            const nama = document.getElementById('inputNama').value.trim();
            const satuan = document.getElementById('inputSatuan').value;
            const kategori = document.getElementById('inputKategori').value;
            const deskripsi = document.getElementById('inputDeskripsi').value.trim();
            const stok = parseInt(document.getElementById('inputStok').value) || 0;

            if(!kode || !nama) return alert("Kode dan Nama Bahan harus diisi!");
            if(dbBahanBaku.find(item => item.kode === kode)) return alert("Kode bahan baku sudah digunakan!");

            dbBahanBaku.push({ kode, nama, satuan, kategori, deskripsi, stok });
            localStorage.setItem('warmindo_bahan_baku', JSON.stringify(dbBahanBaku));
            
            if(stok > 0) catatRiwayat('Masuk', kode, nama, stok, 0, 'Sistem: Saldo Awal Master');

            resetFormMaster();
            renderData();
        }

        function hapusBahan(kode) {
            if(confirm("Hapus data master ini permanen?")) {
                dbBahanBaku = dbBahanBaku.filter(item => item.kode !== kode);
                localStorage.setItem('warmindo_bahan_baku', JSON.stringify(dbBahanBaku));
                renderData();
            }
        }

        function resetFormMaster() {
            document.getElementById('inputKode').value = '';
            document.getElementById('inputNama').value = '';
            document.getElementById('inputStok').value = '0';
            document.getElementById('inputDeskripsi').value = '';
        }

        // === PENCATATAN RIWAYAT ===
        function catatRiwayat(jenis, kode, nama, qty, harga = 0, keterangan = "") {
            const waktu = new Date().toLocaleString('id-ID', { year:'numeric', month:'short', day:'numeric', hour:'2-digit', minute:'2-digit'});
            dbRiwayat.unshift({ waktu, jenis, kode, nama, qty, harga, keterangan });
            localStorage.setItem('warmindo_riwayat', JSON.stringify(dbRiwayat));
        }

        function hapusRiwayat() {
            if(confirm("Bersihkan seluruh log riwayat? Tindakan ini tidak menghapus saldo master.")) {
                dbRiwayat = [];
                localStorage.setItem('warmindo_riwayat', JSON.stringify(dbRiwayat));
                renderData();
            }
        }

        // === TRANSAKSI IN/OUT & OPNAME ===
        function simpanPembelian() {
            const tgl = document.getElementById('tglPembelian').value;
            const supplier = document.getElementById('supplierPembelian').value || 'Internal';
            const nota = document.getElementById('notaPembelian').value || '-';
            const kodeBahan = document.getElementById('selectBahanPembelian').value;
            const qty = parseInt(document.getElementById('jumlahPembelian').value);
            const harga = parseInt(document.getElementById('hargaPembelian').value) || 0;
            
            if(!kodeBahan || isNaN(qty) || qty <= 0) return alert("Validasi: Qty wajib lebih dari 0!");

            const bahan = dbBahanBaku.find(b => b.kode === kodeBahan);
            if(bahan) {
                bahan.stok = (bahan.stok || 0) + qty;
                localStorage.setItem('warmindo_bahan_baku', JSON.stringify(dbBahanBaku));
                
                const ket = `Nota: ${nota} | Suppl: ${supplier}`;
                catatRiwayat('Masuk', bahan.kode, bahan.nama, qty, harga, ket);
                
                document.getElementById('jumlahPembelian').value = '';
                document.getElementById('hargaPembelian').value = '';
                renderData();
            }
        }

        function simpanPemakaian() {
            const tgl = document.getElementById('tglPemakaian').value;
            const unit = document.getElementById('unitPemakaian').value;
            const kodeBahan = document.getElementById('selectBahanPemakaian').value;
            const qty = parseInt(document.getElementById('jumlahPemakaian').value);
            
            if(!kodeBahan || isNaN(qty) || qty <= 0) return alert("Validasi: Qty wajib lebih dari 0!");

            const bahan = dbBahanBaku.find(b => b.kode === kodeBahan);
            if(bahan) {
                const currentStok = bahan.stok || 0;
                if(currentStok < qty) return alert(`Saldo kurang! Sisa sistem: ${currentStok}`);
                
                bahan.stok = currentStok - qty;
                localStorage.setItem('warmindo_bahan_baku', JSON.stringify(dbBahanBaku));
                
                catatRiwayat('Keluar', bahan.kode, bahan.nama, qty, 0, `Tujuan: ${unit}`);
                
                document.getElementById('jumlahPemakaian').value = '';
                renderData();
            }
        }

        function sesuaikanOpname(kode) {
            const inputElement = document.getElementById(`opname-${kode}`);
            if(!inputElement) return;
            
            const qtyFisik = parseInt(inputElement.value);
            if(isNaN(qtyFisik) || qtyFisik < 0) return alert("Format angka stok fisik tidak valid!");

            const bahan = dbBahanBaku.find(b => b.kode === kode);
            if(bahan) {
                const stokLama = bahan.stok || 0;
                const selisih = qtyFisik - stokLama;
                
                if(selisih === 0) return alert("Telah tersinkronasi. Tidak ada update.");

                bahan.stok = qtyFisik;
                localStorage.setItem('warmindo_bahan_baku', JSON.stringify(dbBahanBaku));

                catatRiwayat('Opname', bahan.kode, bahan.nama, Math.abs(selisih), 0, `Sistem (${stokLama}) -> Fisik (${qtyFisik})`);
                renderData();
            }
        }

        // === RENDER ENGINE ===
        function renderData() {
            try {
                const tbMaster = document.getElementById('tabelMasterBahan');
                const tbOpname = document.getElementById('tabelOpname');
                const tbLaporan = document.getElementById('tabelLaporanStok');
                const tbRiwayat = document.getElementById('tabelRiwayat');
                const selBeli = document.getElementById('selectBahanPembelian');
                const selPakai = document.getElementById('selectBahanPemakaian');
                
                if(tbMaster) tbMaster.innerHTML = '';
                if(tbOpname) tbOpname.innerHTML = '';
                if(tbLaporan) tbLaporan.innerHTML = '';
                if(tbRiwayat) tbRiwayat.innerHTML = '';
                if(selBeli) selBeli.innerHTML = '<option value="">-- Pilih Bahan Baku --</option>';
                if(selPakai) selPakai.innerHTML = '<option value="">-- Pilih Bahan Baku --</option>';

                let krisisCount = 0;

                if(dbBahanBaku.length === 0) {
                    const emptyRow = '<tr><td colspan="6" style="text-align:center; color: var(--text-muted); padding: 30px;">Belum ada data tersedia.</td></tr>';
                    if(tbMaster) tbMaster.innerHTML = emptyRow;
                    if(tbOpname) tbOpname.innerHTML = emptyRow;
                    if(tbLaporan) tbLaporan.innerHTML = emptyRow;
                } else {
                    dbBahanBaku.forEach(item => {
                        const currentStok = item.stok || 0;
                        const kategori = item.kategori || '-';
                        
                        let statusTxt = "<span style='color: var(--success); font-weight: 500;'>Aman</span>";
                        let rowColor = "var(--text-main)";
                        if(currentStok <= 5 && currentStok > 0) { statusTxt = "<span style='color: var(--warning); font-weight: 600;'>Kritis</span>"; rowColor = "var(--warning)"; krisisCount++; }
                        if(currentStok === 0) { statusTxt = "<span style='color: var(--danger); font-weight: 600;'>Habis</span>"; rowColor = "var(--danger)"; krisisCount++; }

                        if(tbMaster) {
                            tbMaster.innerHTML += `
                                <tr>
                                    <td style="color: var(--text-muted);">${item.kode}</td>
                                    <td style="font-weight: 500;">${item.nama}</td>
                                    <td>${kategori}</td>
                                    <td>${item.satuan}</td>
                                    <td style="color:${rowColor}; font-weight:700;">${currentStok}</td>
                                    <td><button class="btn-info" style="color: var(--danger); border: none; padding: 6px 12px;" onclick="hapusBahan('${item.kode}')">Hapus</button></td>
                                </tr>
                            `;
                        }

                        if(tbLaporan) {
                            tbLaporan.innerHTML += `
                                <tr>
                                    <td style="color: var(--text-muted);">${item.kode}</td>
                                    <td>${kategori}</td>
                                    <td style="font-weight: 500;">${item.nama}</td>
                                    <td>${item.satuan}</td>
                                    <td style="color: ${rowColor}; font-weight: 700;">${currentStok}</td>
                                    <td>${statusTxt}</td>
                                </tr>
                            `;
                        }

                        if(tbOpname) {
                            tbOpname.innerHTML += `
                                <tr>
                                    <td style="color: var(--text-muted);">${item.kode}</td>
                                    <td style="font-weight: 500;">${item.nama}</td>
                                    <td><span style="background: #f1f5f9; padding: 4px 8px; border-radius: 4px;">${currentStok} ${item.satuan}</span></td>
                                    <td><input type="number" id="opname-${item.kode}" value="${currentStok}" style="margin:0; padding:8px;"></td>
                                    <td><button class="btn-info" style="border: 1px solid var(--primary); color: var(--primary);" onclick="sesuaikanOpname('${item.kode}')">Terapkan</button></td>
                                </tr>
                            `;
                        }

                        const opt = `<option value="${item.kode}">${item.nama} (Sisa: ${currentStok} ${item.satuan})</option>`;
                        if(selBeli) selBeli.innerHTML += opt;
                        if(selPakai) selPakai.innerHTML += opt;
                    });
                }

                if(dbRiwayat.length === 0) {
                    if(tbRiwayat) tbRiwayat.innerHTML = '<tr><td colspan="5" style="text-align:center; color: var(--text-muted); padding: 30px;">Belum ada catatan aktivitas.</td></tr>';
                } else {
                    dbRiwayat.forEach(log => {
                        let badgeClass = 'badge-masuk';
                        if(log.jenis === 'Keluar') badgeClass = 'badge-keluar';
                        if(log.jenis === 'Opname') badgeClass = 'badge-opname';
                        
                        const infoTambahan = log.harga > 0 ? `<div style="font-weight:600;">${formatRupiah(log.harga)}</div><div style="font-size:12px; color:var(--text-muted);">${log.keterangan}</div>` : `<span style="color:var(--text-muted);">${log.keterangan}</span>`;
                        
                        if(tbRiwayat) {
                            tbRiwayat.innerHTML += `
                                <tr>
                                    <td style="font-size: 13px; color: var(--text-muted);">${log.waktu}</td>
                                    <td><span class="badge ${badgeClass}">${log.jenis}</span></td>
                                    <td><span style="color: var(--text-muted); font-size: 12px;">[${log.kode}]</span><br><b>${log.nama}</b></td>
                                    <td style="font-weight: 700; font-size: 16px;">${log.qty}</td>
                                    <td>${infoTambahan}</td>
                                </tr>
                            `;
                        }
                    });
                }

                if(document.getElementById('dashTotalItem')) document.getElementById('dashTotalItem').innerText = dbBahanBaku.length;
                if(document.getElementById('dashStokKritis')) document.getElementById('dashStokKritis').innerText = krisisCount;
                if(document.getElementById('dashTotalTransaksi')) document.getElementById('dashTotalTransaksi').innerText = dbRiwayat.length;

            } catch (error) {
                console.error("Terjadi error render data:", error);
            }
        }

        // === JALANKAN SAAT HALAMAN DIBUKA ===
        window.onload = function() {
            checkAuth();
        };
    </script>
</body>
</html>
