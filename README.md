<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>المتصفح الاحترافي - حساب الأرباح للتجار الصغار</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --success-color: #27ae60;
            --warning-color: #f39c12;
            --danger-color: #e74c3c;
            --light-color: #ecf0f1;
            --dark-color: #2c3e50;
            --sidebar-width: 250px;
            --header-height: 70px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Cairo', sans-serif;
        }

        body {
            background-color: #f5f7fa;
            color: #333;
            direction: rtl;
        }

        .container {
            display: flex;
            min-height: 100vh;
        }

        /* الشريط الجانبي */
        .sidebar {
            width: var(--sidebar-width);
            background-color: var(--primary-color);
            color: white;
            padding: 20px 0;
            position: fixed;
            height: 100vh;
            overflow-y: auto;
            transition: all 0.3s;
            z-index: 100;
        }

        .logo {
            text-align: center;
            padding: 0 20px 30px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            margin-bottom: 20px;
        }

        .logo h2 {
            color: white;
            font-size: 1.5rem;
        }

        .logo span {
            color: var(--secondary-color);
        }

        .logo p {
            font-size: 0.9rem;
            opacity: 0.8;
        }

        .nav-links {
            list-style: none;
            padding: 0 15px;
        }

        .nav-links li {
            margin-bottom: 10px;
        }

        .nav-links a {
            display: flex;
            align-items: center;
            padding: 15px;
            color: var(--light-color);
            text-decoration: none;
            border-radius: 8px;
            transition: all 0.3s;
        }

        .nav-links a:hover, .nav-links a.active {
            background-color: rgba(255,255,255,0.1);
            color: white;
        }

        .nav-links i {
            margin-left: 10px;
            font-size: 1.2rem;
            width: 25px;
        }

        /* المحتوى الرئيسي */
        .main-content {
            flex: 1;
            margin-right: var(--sidebar-width);
            padding: 20px;
        }

        header {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            margin-bottom: 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .header-title h1 {
            color: var(--primary-color);
            font-size: 1.8rem;
            margin-bottom: 5px;
        }

        .header-title p {
            color: #7f8c8d;
        }

        .user-info {
            display: flex;
            align-items: center;
        }

        .user-info img {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            margin-left: 15px;
            border: 3px solid var(--light-color);
        }

        /* بطاقات الإحصائيات */
        .stats-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background-color: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            display: flex;
            align-items: center;
            transition: transform 0.3s;
        }

        .stat-card:hover {
            transform: translateY(-5px);
        }

        .stat-icon {
            width: 70px;
            height: 70px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-left: 20px;
            font-size: 1.8rem;
        }

        .stat-content h3 {
            font-size: 1.8rem;
            margin-bottom: 5px;
            color: var(--primary-color);
        }

        .stat-content p {
            color: #7f8c8d;
        }

        .income .stat-icon {
            background-color: rgba(39, 174, 96, 0.1);
            color: var(--success-color);
        }

        .expenses .stat-icon {
            background-color: rgba(231, 76, 60, 0.1);
            color: var(--danger-color);
        }

        .profit .stat-icon {
            background-color: rgba(52, 152, 219, 0.1);
            color: var(--secondary-color);
        }

        .products .stat-icon {
            background-color: rgba(243, 156, 18, 0.1);
            color: var(--warning-color);
        }

        /* الأقسام الرئيسية */
        .content-sections {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
        }

        .section {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            overflow: hidden;
        }

        .section-header {
            background-color: var(--primary-color);
            color: white;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .section-header h3 {
            font-size: 1.3rem;
        }

        .section-content {
            padding: 20px;
        }

        /* نموذج إضافة معاملة */
        .transaction-form .form-group,
        .product-form .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: var(--primary-color);
            font-weight: 500;
        }

        .form-control {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
            transition: border 0.3s;
        }

        .form-control:focus {
            border-color: var(--secondary-color);
            outline: none;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .btn-primary {
            background-color: var(--secondary-color);
            color: white;
        }

        .btn-primary:hover {
            background-color: #2980b9;
        }

        .btn-success {
            background-color: var(--success-color);
            color: white;
        }

        .btn-success:hover {
            background-color: #229954;
        }

        .btn-danger {
            background-color: var(--danger-color);
            color: white;
        }

        .btn-danger:hover {
            background-color: #c0392b;
        }

        .btn-warning {
            background-color: var(--warning-color);
            color: white;
        }

        .btn-warning:hover {
            background-color: #d68910;
        }

        .btn-block {
            width: 100%;
        }

        .btn-sm {
            padding: 8px 15px;
            font-size: 0.9rem;
        }

        /* قائمة المنتجات */
        .product-list,
        .transaction-list {
            list-style: none;
        }

        .product-item,
        .transaction-item {
            padding: 15px;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .product-item:last-child,
        .transaction-item:last-child {
            border-bottom: none;
        }

        .product-info h4 {
            margin-bottom: 5px;
            color: var(--primary-color);
        }

        .product-price {
            font-weight: 600;
            color: var(--success-color);
        }

        .product-actions {
            display: flex;
            gap: 8px;
            margin-top: 10px;
        }

        /* قائمة المعاملات */
        .transaction-type {
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.9rem;
            font-weight: 500;
        }

        .income-badge {
            background-color: rgba(39, 174, 96, 0.1);
            color: var(--success-color);
        }

        .expense-badge {
            background-color: rgba(231, 76, 60, 0.1);
            color: var(--danger-color);
        }

        /* الرسم البياني */
        .chart-container {
            height: 250px;
            position: relative;
        }

        /* التبويبات */
        .tabs {
            display: flex;
            border-bottom: 1px solid #ddd;
            margin-bottom: 20px;
        }

        .tab {
            padding: 15px 25px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
        }

        .tab:hover {
            background-color: #f8f9fa;
        }

        .tab.active {
            border-bottom-color: var(--secondary-color);
            color: var(--secondary-color);
            font-weight: 600;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        /* التكيف مع الشاشات الصغيرة */
        @media (max-width: 992px) {
            .sidebar {
                width: 70px;
                overflow: visible;
            }

            .sidebar .logo h2 span,
            .sidebar .nav-links li a span {
                display: none;
            }

            .sidebar .logo h2 {
                font-size: 1.2rem;
            }

            .main-content {
                margin-right: 70px;
            }

            .nav-links a {
                justify-content: center;
                padding: 15px 10px;
            }

            .nav-links i {
                margin-left: 0;
            }
        }

        @media (max-width: 768px) {
            .stats-cards {
                grid-template-columns: 1fr;
            }

            .content-sections {
                grid-template-columns: 1fr;
            }

            header {
                flex-direction: column;
                align-items: flex-start;
            }

            .user-info {
                margin-top: 15px;
            }
            
            .tabs {
                flex-wrap: wrap;
            }
            
            .tab {
                flex: 1 0 auto;
                text-align: center;
            }
        }

        /* الرسائل */
        .alert {
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .alert-success {
            background-color: rgba(39, 174, 96, 0.1);
            color: var(--success-color);
            border: 1px solid rgba(39, 174, 96, 0.2);
        }

        .alert-danger {
            background-color: rgba(231, 76, 60, 0.1);
            color: var(--danger-color);
            border: 1px solid rgba(231, 76, 60, 0.2);
        }

        /* المودال */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            width: 90%;
            max-width: 500px;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-header h3 {
            color: var(--primary-color);
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #7f8c8d;
        }
    </style>
</head>
<body>
    <!-- مودال إضافة منتج -->
    <div id="productModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>إضافة منتج جديد</h3>
                <button class="close-modal" onclick="closeModal('productModal')">&times;</button>
            </div>
            <form id="productForm">
                <div class="form-group">
                    <label for="productName">اسم المنتج</label>
                    <input type="text" id="productName" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="purchasePrice">سعر الشراء (ريال)</label>
                    <input type="number" id="purchasePrice" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="salePrice">سعر البيع (ريال)</label>
                    <input type="number" id="salePrice" class="form-control" required>
                </div>
                
                <div class="form-group">
                    <label for="quantity">الكمية في المخزون</label>
                    <input type="number" id="quantity" class="form-control" value="1" required>
                </div>
                
                <div class="form-group">
                    <label for="productCategory">الفئة</label>
                    <select id="productCategory" class="form-control">
                        <option value="عام">عام</option>
                        <option value="إلكترونيات">إلكترونيات</option>
                        <option value="ملابس">ملابس</option>
                        <option value="أغذية">أغذية</option>
                        <option value="مستلزمات منزلية">مستلزمات منزلية</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="productDescription">وصف المنتج (اختياري)</label>
                    <textarea id="productDescription" class="form-control" rows="3"></textarea>
                </div>
                
                <button type="submit" class="btn btn-success btn-block">
                    <i class="fas fa-save"></i> حفظ المنتج
                </button>
            </form>
        </div>
    </div>

    <!-- مودال التقارير -->
    <div id="reportsModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>التقارير المالية</h3>
                <button class="close-modal" onclick="closeModal('reportsModal')">&times;</button>
            </div>
            <div class="tabs">
                <div class="tab active" onclick="switchReportTab('daily')">يومي</div>
                <div class="tab" onclick="switchReportTab('monthly')">شهري</div>
                <div class="tab" onclick="switchReportTab('yearly')">سنوي</div>
            </div>
            
            <div id="dailyReport" class="tab-content active">
                <h4>تقرير اليوم</h4>
                <div id="dailyStats" style="margin: 20px 0;"></div>
                <canvas id="dailyChart"></canvas>
            </div>
            
            <div id="monthlyReport" class="tab-content">
                <h4>تقرير الشهر</h4>
                <div id="monthlyStats" style="margin: 20px 0;"></div>
                <canvas id="monthlyChart"></canvas>
            </div>
            
            <div id="yearlyReport" class="tab-content">
                <h4>تقرير السنة</h4>
                <div id="yearlyStats" style="margin: 20px 0;"></div>
                <canvas id="yearlyChart"></canvas>
            </div>
            
            <div style="margin-top: 20px;">
                <button class="btn btn-primary" onclick="exportToPDF()">
                    <i class="fas fa-file-pdf"></i> تصدير كـ PDF
                </button>
                <button class="btn btn-success" onclick="exportToExcel()">
                    <i class="fas fa-file-excel"></i> تصدير كـ Excel
                </button>
            </div>
        </div>
    </div>

    <!-- مودال الإعدادات -->
    <div id="settingsModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>الإعدادات</h3>
                <button class="close-modal" onclick="closeModal('settingsModal')">&times;</button>
            </div>
            
            <div class="tabs">
                <div class="tab active" onclick="switchSettingsTab('general')">عام</div>
                <div class="tab" onclick="switchSettingsTab('backup')">النسخ الاحتياطي</div>
                <div class="tab" onclick="switchSettingsTab('account')">الحساب</div>
            </div>
            
            <div id="generalSettings" class="tab-content active">
                <div class="form-group">
                    <label>العملة</label>
                    <select id="currency" class="form-control">
                        <option value="ريال">ريال سعودي (ريال)</option>
                        <option value="دينار">دينار كويتي (د.ك)</option>
                        <option value="درهم">درهم إماراتي (د.إ)</option>
                        <option value="دولار">دولار أمريكي ($)</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label>تنسيق التاريخ</label>
                    <select id="dateFormat" class="form-control">
                        <option value="dd/mm/yyyy">يوم/شهر/سنة</option>
                        <option value="mm/dd/yyyy">شهر/يوم/سنة</option>
                        <option value="yyyy-mm-dd">سنة-شهر-يوم</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label>بداية الأسبوع</label>
                    <select id="weekStart" class="form-control">
                        <option value="0">الأحد</option>
                        <option value="6">السبت</option>
                        <option value="1">الإثنين</option>
                    </select>
                </div>
                
                <button class="btn btn-primary btn-block" onclick="saveSettings()">
                    <i class="fas fa-save"></i> حفظ الإعدادات
                </button>
            </div>
            
            <div id="backupSettings" class="tab-content">
                <div class="alert alert-success">
                    <i class="fas fa-info-circle"></i>
                    <div>
                        <strong>النسخ الاحتياطي</strong>
                        <p>احفظ نسخة من بياناتك لتجنب فقدانها</p>
                    </div>
                </div>
                
                <div class="form-group">
                    <label>تاريخ آخر نسخة احتياطية</label>
                    <input type="text" id="lastBackup" class="form-control" readonly>
                </div>
                
                <div style="display: flex; gap: 10px; margin-top: 20px;">
                    <button class="btn btn-primary" onclick="backupData()">
                        <i class="fas fa-download"></i> إنشاء نسخة احتياطية
                    </button>
                    <button class="btn btn-warning" onclick="restoreData()">
                        <i class="fas fa-upload"></i> استعادة نسخة
                    </button>
                </div>
                
                <div style="margin-top: 20px;">
                    <button class="btn btn-danger" onclick="clearAllData()">
                        <i class="fas fa-trash"></i> حذف جميع البيانات
                    </button>
                </div>
            </div>
            
            <div id="accountSettings" class="tab-content">
                <div class="form-group">
                    <label>اسم المستخدم</label>
                    <input type="text" id="username" class="form-control">
                </div>
                
                <div class="form-group">
                    <label>البريد الإلكتروني</label>
                    <input type="email" id="email" class="form-control">
                </div>
                
                <div class="form-group">
                    <label>كلمة المرور الجديدة</label>
                    <input type="password" id="password" class="form-control">
                </div>
                
                <button class="btn btn-primary btn-block">
                    <i class="fas fa-save"></i> تحديث الحساب
                </button>
            </div>
        </div>
    </div>

    <div class="container">
        <!-- الشريط الجانبي -->
        <nav class="sidebar">
            <div class="logo">
                <h2>حساب <span>الأرباح</span></h2>
                <p>للتجار الصغار</p>
            </div>
            
            <ul class="nav-links">
                <li>
                    <a href="#" class="active" onclick="showSection('dashboard')">
                        <i class="fas fa-home"></i>
                        <span>الرئيسية</span>
                    </a>
                </li>
                <li>
                    <a href="#" onclick="showSection('transactions')">
                        <i class="fas fa-exchange-alt"></i>
                        <span>المعاملات</span>
                    </a>
                </li>
                <li>
                    <a href="#" onclick="showSection('products')">
                        <i class="fas fa-boxes"></i>
                        <span>المنتجات</span>
                    </a>
                </li>
                <li>
                    <a href="#" onclick="showSection('inventory')">
                        <i class="fas fa-warehouse"></i>
                        <span>المخزون</span>
                    </a>
                </li>
                <li>
                    <a href="#" onclick="openReportsModal()">
                        <i class="fas fa-chart-pie"></i>
                        <span>التقارير</span>
                    </a>
                </li>
                <li>
                    <a href="#" onclick="openSettingsModal()">
                        <i class="fas fa-cog"></i>
                        <span>الإعدادات</span>
                    </a>
                </li>
            </ul>
        </nav>

        <!-- المحتوى الرئيسي -->
        <main class="main-content">
            <!-- رأس الصفحة -->
            <header>
                <div class="header-title">
                    <h1 id="pageTitle">لوحة التحكم</h1>
                    <p id="pageDescription">إدارة متجرك وحساب أرباحك بكل سهولة</p>
                </div>
                
                <div class="user-info">
                    <img src="https://ui-avatars.com/api/?name=محمد+أحمد&background=3498db&color=fff&size=100" alt="صورة المستخدم">
                    <div>
                        <h4 id="userName">محمد أحمد</h4>
                        <p id="userRole">تاجر</p>
                    </div>
                </div>
            </header>

            <!-- قسم لوحة التحكم -->
            <section id="dashboard" class="content-section active">
                <!-- بطاقات الإحصائيات -->
                <div class="stats-cards">
                    <div class="stat-card income">
                        <div class="stat-icon">
                            <i class="fas fa-money-bill-wave"></i>
                        </div>
                        <div class="stat-content">
                            <h3 id="totalIncome">0 ريال</h3>
                            <p>إجمالي الإيرادات</p>
                        </div>
                    </div>
                    
                    <div class="stat-card expenses">
                        <div class="stat-icon">
                            <i class="fas fa-file-invoice-dollar"></i>
                        </div>
                        <div class="stat-content">
                            <h3 id="totalExpenses">0 ريال</h3>
                            <p>إجمالي المصروفات</p>
                        </div>
                    </div>
                    
                    <div class="stat-card profit">
                        <div class="stat-icon">
                            <i class="fas fa-chart-line"></i>
                        </div>
                        <div class="stat-content">
                            <h3 id="netProfit">0 ريال</h3>
                            <p>صافي الربح</p>
                        </div>
                    </div>
                    
                    <div class="stat-card products">
                        <div class="stat-icon">
                            <i class="fas fa-boxes"></i>
                        </div>
                        <div class="stat-content">
                            <h3 id="productsCount">0</h3>
                            <p>عدد المنتجات</p>
                        </div>
                    </div>
                </div>

                <!-- الرسم البياني -->
                <div class="section" style="grid-column: 1 / -1; margin-bottom: 30px;">
                    <div class="section-header">
                        <h3>تحليل الأرباح الشهري</h3>
                        <i class="fas fa-chart-bar"></i>
                    </div>
                    <div class="section-content">
                        <canvas id="monthlyProfitChart"></canvas>
                    </div>
                </div>

                <!-- الأقسام الفرعية -->
                <div class="content-sections">
                    <!-- قسم إضافة معاملة -->
                    <section class="section">
                        <div class="section-header">
                            <h3>إضافة معاملة جديدة</h3>
                            <i class="fas fa-plus-circle"></i>
                        </div>
                        <div class="section-content">
                            <form id="transactionForm">
                                <div class="form-group">
                                    <label for="transactionType">نوع المعاملة</label>
                                    <select id="transactionType" class="form-control" required>
                                        <option value="income">إيراد (بيع)</option>
                                        <option value="expense">مصروف</option>
                                    </select>
                                </div>
                                
                                <div class="form-group">
                                    <label for="transactionAmount">المبلغ (ريال)</label>
                                    <input type="number" id="transactionAmount" class="form-control" placeholder="أدخل المبلغ" required>
                                </div>
                                
                                <div class="form-group">
                                    <label for="transactionDescription">الوصف</label>
                                    <input type="text" id="transactionDescription" class="form-control" placeholder="وصف المعاملة" required>
                                </div>
                                
                                <div class="form-group">
                                    <label for="transactionDate">التاريخ</label>
                                    <input type="date" id="transactionDate" class="form-control" required>
                                </div>
                                
                                <div class="form-group">
                                    <label for="transactionCategory">الفئة</label>
                                    <select id="transactionCategory" class="form-control">
                                        <option value="عام">عام</option>
                                        <option value="مبيعات">مبيعات</option>
                                        <option value="مشتريات">مشتريات</option>
                                        <option value="رواتب">رواتب</option>
                                        <option value="إيجار">إيجار</option>
                                        <option value="فواتير">فواتير</option>
                                    </select>
                                </div>
                                
                                <button type="submit" class="btn btn-primary btn-block">
                                    <i class="fas fa-plus"></i> إضافة المعاملة
                                </button>
                            </form>
                        </div>
                    </section>

                    <!-- قسم آخر المعاملات -->
                    <section class="section">
                        <div class="section-header">
                            <h3>آخر المعاملات</h3>
                            <i class="fas fa-history"></i>
                        </div>
                        <div class="section-content">
                            <ul id="recentTransactions" class="transaction-list">
                                <!-- سيتم ملؤها بالبيانات -->
                            </ul>
                        </div>
                    </section>

                    <!-- قسم المنتجات الأكثر ربحية -->
                    <section class="section">
                        <div class="section-header">
                            <h3>المنتجات الأكثر ربحية</h3>
                            <i class="fas fa-crown"></i>
                        </div>
                        <div class="section-content">
                            <ul id="topProducts" class="product-list">
                                <!-- سيتم ملؤها بالبيانات -->
                            </ul>
                        </div>
                    </section>
                </div>
            </section>

            <!-- قسم إدارة المنتجات -->
            <section id="products" class="content-section" style="display: none;">
                <div class="section" style="margin-bottom: 30px;">
                    <div class="section-header">
                        <h3>إدارة المنتجات</h3>
                        <button class="btn btn-success" onclick="openProductModal()">
                            <i class="fas fa-plus"></i> إضافة منتج جديد
                        </button>
                    </div>
                    <div class="section-content">
                        <div class="alert alert-success" id="productMessage" style="display: none;"></div>
                        <div id="productsContainer"></div>
                    </div>
                </div>
            </section>

            <!-- قسم المعاملات -->
            <section id="transactions" class="content-section" style="display: none;">
                <div class="section">
                    <div class="section-header">
                        <h3>جميع المعاملات</h3>
                        <div>
                            <select id="filterType" class="form-control" style="display: inline-block; width: auto; margin-left: 10px;">
                                <option value="all">جميع الأنواع</option>
                                <option value="income">إيرادات فقط</option>
                                <option value="expense">مصروفات فقط</option>
                            </select>
                            <input type="month" id="filterMonth" class="form-control" style="display: inline-block; width: auto; margin-left: 10px;">
                        </div>
                    </div>
                    <div class="section-content">
                        <div id="allTransactionsContainer"></div>
                    </div>
                </div>
            </section>

            <!-- قسم المخزون -->
            <section id="inventory" class="content-section" style="display: none;">
                <div class="section">
                    <div class="section-header">
                        <h3>إدارة المخزون</h3>
                        <div>
                            <input type="text" id="searchProduct" class="form-control" placeholder="بحث عن منتج..." style="display: inline-block; width: auto;">
                        </div>
                    </div>
                    <div class="section-content">
                        <div id="inventoryContainer"></div>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <script>
        // البيانات والتخزين المحلي
        let transactions = JSON.parse(localStorage.getItem('profitCalculator_transactions')) || [];
        let products = JSON.parse(localStorage.getItem('profitCalculator_products')) || [];
        let settings = JSON.parse(localStorage.getItem('profitCalculator_settings')) || {
            currency: 'ريال',
            dateFormat: 'dd/mm/yyyy',
            weekStart: '0',
            lastBackup: null
        };

        // المتغيرات العامة
        let charts = {};
        let currentEditingProduct = null;

        // تهيئة التطبيق
        document.addEventListener('DOMContentLoaded', function() {
            initApp();
        });

        // تهيئة التطبيق
        function initApp() {
            // تعيين التاريخ الافتراضي
            document.getElementById('transactionDate').valueAsDate = new Date();
            
            // تحميل الإعدادات
            loadSettings();
            
            // تحميل البيانات وعرضها
            loadData();
            
            // إضافة معاملة جديدة
            document.getElementById('transactionForm').addEventListener('submit', function(e) {
                e.preventDefault();
                addTransaction();
            });
            
            // إضافة منتج جديد
            document.getElementById('productForm').addEventListener('submit', function(e) {
                e.preventDefault();
                saveProduct();
            });
            
            // تصفية المعاملات
            document.getElementById('filterType').addEventListener('change', loadTransactions);
            document.getElementById('filterMonth').addEventListener('change', loadTransactions);
            
            // بحث المنتجات
            document.getElementById('searchProduct').addEventListener('input', loadInventory);
            
            // إنشاء الرسم البياني
            createMonthlyChart();
        }

        // تحميل البيانات
        function loadData() {
            calculateStats();
            loadRecentTransactions();
            loadTopProducts();
            loadProducts();
            loadTransactions();
            loadInventory();
        }

        // تحميل الإعدادات
        function loadSettings() {
            document.getElementById('currency').value = settings.currency || 'ريال';
            document.getElementById('dateFormat').value = settings.dateFormat || 'dd/mm/yyyy';
            document.getElementById('weekStart').value = settings.weekStart || '0';
            document.getElementById('lastBackup').value = settings.lastBackup || 'لم يتم إنشاء نسخة احتياطية بعد';
            document.getElementById('username').value = settings.username || 'محمد أحمد';
            document.getElementById('email').value = settings.email || 'mohammed@example.com';
        }

        // حفظ الإعدادات
        function saveSettings() {
            settings.currency = document.getElementById('currency').value;
            settings.dateFormat = document.getElementById('dateFormat').value;
            settings.weekStart = document.getElementById('weekStart').value;
            settings.username = document.getElementById('username').value;
            settings.email = document.getElementById('email').value;
            
            localStorage.setItem('profitCalculator_settings', JSON.stringify(settings));
            
            showAlert('تم حفظ الإعدادات بنجاح', 'success');
            setTimeout(() => location.reload(), 1000);
        }

        // حساب الإحصائيات
        function calculateStats() {
            let totalIncome = 0;
            let totalExpenses = 0;
            
            transactions.forEach(transaction => {
                if (transaction.type === 'income') {
                    totalIncome += parseFloat(transaction.amount);
                } else {
                    totalExpenses += parseFloat(transaction.amount);
                }
            });
            
            const netProfit = totalIncome - totalExpenses;
            
            document.getElementById('totalIncome').textContent = `${formatNumber(totalIncome)} ${settings.currency}`;
            document.getElementById('totalExpenses').textContent = `${formatNumber(totalExpenses)} ${settings.currency}`;
            document.getElementById('netProfit').textContent = `${formatNumber(netProfit)} ${settings.currency}`;
            document.getElementById('productsCount').textContent = products.length;
        }

        // إضافة معاملة جديدة
        function addTransaction() {
            const type = document.getElementById('transactionType').value;
            const amount = parseFloat(document.getElementById('transactionAmount').value);
            const description = document.getElementById('transactionDescription').value;
            const date = document.getElementById('transactionDate').value;
            const category = document.getElementById('transactionCategory').value;
            
            const transaction = {
                id: Date.now(),
                type: type,
                amount: amount,
                description: description,
                date: date,
                category: category,
                timestamp: new Date().toISOString()
            };
            
            transactions.push(transaction);
            saveData();
            
            document.getElementById('transactionForm').reset();
            document.getElementById('transactionDate').valueAsDate = new Date();
            
            showAlert('تم إضافة المعاملة بنجاح', 'success');
            loadData();
        }

        // تحميل المعاملات الحديثة
        function loadRecentTransactions() {
            const container = document.getElementById('recentTransactions');
            container.innerHTML = '';
            
            // ترتيب من الأحدث إلى الأقدم
            const sortedTransactions = [...transactions].sort((a, b) => new Date(b.date) - new Date(a.date));
            const recent = sortedTransactions.slice(0, 5);
            
            if (recent.length === 0) {
                container.innerHTML = '<li style="text-align: center; color: #7f8c8d; padding: 20px;">لا توجد معاملات</li>';
                return;
            }
            
            recent.forEach(transaction => {
                const item = document.createElement('li');
                item.className = 'transaction-item';
                
                const typeClass = transaction.type === 'income' ? 'income-badge' : 'expense-badge';
                const typeText = transaction.type === 'income' ? 'إيراد' : 'مصروف';
                const sign = transaction.type === 'income' ? '+' : '-';
                const color = transaction.type === 'income' ? '#27ae60' : '#e74c3c';
                
                item.innerHTML = `
                    <div>
                        <h4>${transaction.description}</h4>
                        <p>${formatDate(transaction.date)} - ${transaction.category}</p>
                    </div>
                    <div style="text-align: left;">
                        <span class="transaction-type ${typeClass}">${typeText}</span>
                        <div style="margin-top: 5px; font-weight: 600; color: ${color}">
                            ${sign}${formatNumber(transaction.amount)} ${settings.currency}
                        </div>
                    </div>
                `;
                container.appendChild(item);
            });
        }

        // تحميل جميع المعاملات
        function loadTransactions() {
            const container = document.getElementById('allTransactionsContainer');
            const filterType = document.getElementById('filterType').value;
            const filterMonth = document.getElementById('filterMonth').value;
            
            let filteredTransactions = transactions;
            
            // تطبيق الفلاتر
            if (filterType !== 'all') {
                filteredTransactions = filteredTransactions.filter(t => t.type === filterType);
            }
            
            if (filterMonth) {
                filteredTransactions = filteredTransactions.filter(t => t.date.startsWith(filterMonth));
            }
            
            // ترتيب من الأحدث إلى الأقدم
            filteredTransactions.sort((a, b) => new Date(b.date) - new Date(a.date));
            
            if (filteredTransactions.length === 0) {
                container.innerHTML = '<div style="text-align: center; color: #7f8c8d; padding: 40px 20px;">لا توجد معاملات</div>';
                return;
            }
            
            let html = `
                <div style="overflow-x: auto;">
                    <table style="width: 100%; border-collapse: collapse;">
                        <thead>
                            <tr style="background-color: #f8f9fa;">
                                <th style="padding: 12px; text-align: right;">التاريخ</th>
                                <th style="padding: 12px; text-align: right;">الوصف</th>
                                <th style="padding: 12px; text-align: right;">الفئة</th>
                                <th style="padding: 12px; text-align: right;">النوع</th>
                                <th style="padding: 12px; text-align: right;">المبلغ</th>
                                <th style="padding: 12px; text-align: right;">الإجراءات</th>
                            </tr>
                        </thead>
                        <tbody>
            `;
            
            filteredTransactions.forEach(transaction => {
                const typeText = transaction.type === 'income' ? 'إيراد' : 'مصروف';
                const typeColor = transaction.type === 'income' ? '#27ae60' : '#e74c3c';
                const sign = transaction.type === 'income' ? '+' : '-';
                
                html += `
                    <tr style="border-bottom: 1px solid #eee;">
                        <td style="padding: 12px;">${formatDate(transaction.date)}</td>
                        <td style="padding: 12px;">${transaction.description}</td>
                        <td style="padding: 12px;">${transaction.category}</td>
                        <td style="padding: 12px;">
                            <span style="color: ${typeColor}; font-weight: 500;">${typeText}</span>
                        </td>
                        <td style="padding: 12px; font-weight: 600; color: ${typeColor}">
                            ${sign}${formatNumber(transaction.amount)} ${settings.currency}
                        </td>
                        <td style="padding: 12px;">
                            <button class="btn btn-danger btn-sm" onclick="deleteTransaction(${transaction.id})">
                                <i class="fas fa-trash"></i>
                            </button>
                        </td>
                    </tr>
                `;
            });
            
            html += `
                        </tbody>
                    </table>
                </div>
            `;
            
            container.innerHTML = html;
        }

        // تحميل المنتجات
        function loadProducts() {
            const container = document.getElementById('productsContainer');
            
            if (products.length === 0) {
                container.innerHTML = '<div style="text-align: center; color: #7f8c8d; padding: 40px 20px;">لا توجد منتجات</div>';
                return;
            }
            
            let html = '<div class="product-list">';
            
            products.forEach(product => {
                const profit = product.salePrice - product.purchasePrice;
                const profitPercentage = ((profit / product.purchasePrice) * 100).toFixed(1);
                const profitClass = profit >= 0 ? 'success-color' : 'danger-color';
                
                html += `
                    <div class="product-item">
                        <div style="flex: 1;">
                            <h4>${product.name}</h4>
                            <p>الفئة: ${product.category} | المخزون: ${product.quantity}</p>
                            <div class="product-actions">
                                <button class="btn btn-primary btn-sm" onclick="editProduct(${product.id})">
                                    <i class="fas fa-edit"></i> تعديل
                                </button>
                                <button class="btn btn-danger btn-sm" onclick="deleteProduct(${product.id})">
                                    <i class="fas fa-trash"></i> حذف
                                </button>
                                <button class="btn btn-warning btn-sm" onclick="updateInventory(${product.id}, 1)">
                                    <i class="fas fa-plus"></i> إضافة
                                </button>
                                <button class="btn btn-warning btn-sm" onclick="updateInventory(${product.id}, -1)">
                                    <i class="fas fa-minus"></i> خصم
                                </button>
                            </div>
                        </div>
                        <div style="text-align: left;">
                            <div>شراء: ${formatNumber(product.purchasePrice)} ${settings.currency}</div>
                            <div>بيع: ${formatNumber(product.salePrice)} ${settings.currency}</div>
                            <div style="margin-top: 5px; font-weight: 600; color: ${profit >= 0 ? '#27ae60' : '#e74c3c'}">
                                ربح: ${formatNumber(profit)} ${settings.currency} (${profitPercentage}%)
                            </div>
                        </div>
                    </div>
                `;
            });
            
            html += '</div>';
            container.innerHTML = html;
        }

        // تحميل المنتجات الأكثر ربحية
        function loadTopProducts() {
            const container = document.getElementById('topProducts');
            container.innerHTML = '';
            
            if (products.length === 0) {
                container.innerHTML = '<li style="text-align: center; color: #7f8c8d; padding: 20px;">لا توجد منتجات</li>';
                return;
            }
            
            // ترتيب حسب الربح
            const sortedProducts = [...products].sort((a, b) => {
                const profitA = a.salePrice - a.purchasePrice;
                const profitB = b.salePrice - b.purchasePrice;
                return profitB - profitA;
            }).slice(0, 5);
            
            sortedProducts.forEach(product => {
                const profit = product.salePrice - product.purchasePrice;
                const profitPercentage = ((profit / product.purchasePrice) * 100).toFixed(1);
                
                const item = document.createElement('li');
                item.className = 'product-item';
                item.innerHTML = `
                    <div class="product-info">
                        <h4>${product.name}</h4>
                        <p>${product.category} | مخزون: ${product.quantity}</p>
                    </div>
                    <div class="product-price">
                        +${formatNumber(profit)} ${settings.currency}<br>
                        <small>(${profitPercentage}%)</small>
                    </div>
                `;
                container.appendChild(item);
            });
        }

        // تحميل المخزون
        function loadInventory() {
            const container = document.getElementById('inventoryContainer');
            const searchTerm = document.getElementById('searchProduct').value.toLowerCase();
            
            let filteredProducts = products;
            
            if (searchTerm) {
                filteredProducts = products.filter(p => 
                    p.name.toLowerCase().includes(searchTerm) || 
                    p.category.toLowerCase().includes(searchTerm)
                );
            }
            
            if (filteredProducts.length === 0) {
                container.innerHTML = '<div style="text-align: center; color: #7f8c8d; padding: 40px 20px;">لا توجد منتجات</div>';
                return;
            }
            
            let html = `
                <div style="overflow-x: auto;">
                    <table style="width: 100%; border-collapse: collapse;">
                        <thead>
                            <tr style="background-color: #f8f9fa;">
                                <th style="padding: 12px; text-align: right;">المنتج</th>
                                <th style="padding: 12px; text-align: right;">الفئة</th>
                                <th style="padding: 12px; text-align: right;">سعر الشراء</th>
                                <th style="padding: 12px; text-align: right;">سعر البيع</th>
                                <th style="padding: 12px; text-align: right;">الربح</th>
                                <th style="padding: 12px; text-align: right;">المخزون</th>
                                <th style="padding: 12px; text-align: right;">القيمة الإجمالية</th>
                            </tr>
                        </thead>
                        <tbody>
            `;
            
            filteredProducts.forEach(product => {
                const profit = product.salePrice - product.purchasePrice;
                const totalValue = product.purchasePrice * product.quantity;
                
                html += `
                    <tr style="border-bottom: 1px solid #eee;">
                        <td style="padding: 12px;">${product.name}</td>
                        <td style="padding: 12px;">${product.category}</td>
                        <td style="padding: 12px;">${formatNumber(product.purchasePrice)} ${settings.currency}</td>
                        <td style="padding: 12px;">${formatNumber(product.salePrice)} ${settings.currency}</td>
                        <td style="padding: 12px; color: ${profit >= 0 ? '#27ae60' : '#e74c3c'}; font-weight: 600;">
                            ${formatNumber(profit)} ${settings.currency}
                        </td>
                        <td style="padding: 12px;">
                            <span class="${product.quantity <= 5 ? 'danger-color' : 'success-color'}" style="font-weight: 600;">
                                ${product.quantity}
                            </span>
                        </td>
                        <td style="padding: 12px; font-weight: 600;">
                            ${formatNumber(totalValue)} ${settings.currency}
                        </td>
                    </tr>
                `;
            });
            
            html += `
                        </tbody>
                    </table>
                </div>
            `;
            
            container.innerHTML = html;
        }

        // فتح مودال المنتج
        function openProductModal(productId = null) {
            const modal = document.getElementById('productModal');
            const form = document.getElementById('productForm');
            const title = modal.querySelector('h3');
            
            if (productId) {
                // وضع التعديل
                currentEditingProduct = products.find(p => p.id === productId);
                title.textContent = 'تعديل المنتج';
                
                document.getElementById('productName').value = currentEditingProduct.name;
                document.getElementById('purchasePrice').value = currentEditingProduct.purchasePrice;
                document.getElementById('salePrice').value = currentEditingProduct.salePrice;
                document.getElementById('quantity').value = currentEditingProduct.quantity;
                document.getElementById('productCategory').value = currentEditingProduct.category;
                document.getElementById('productDescription').value = currentEditingProduct.description || '';
            } else {
                // وضع الإضافة
                currentEditingProduct = null;
                title.textContent = 'إضافة منتج جديد';
                form.reset();
                document.getElementById('quantity').value = 1;
            }
            
            modal.style.display = 'flex';
        }

        // حفظ المنتج
        function saveProduct() {
            const name = document.getElementById('productName').value;
            const purchasePrice = parseFloat(document.getElementById('purchasePrice').value);
            const salePrice = parseFloat(document.getElementById('salePrice').value);
            const quantity = parseInt(document.getElementById('quantity').value);
            const category = document.getElementById('productCategory').value;
            const description = document.getElementById('productDescription').value;
            
            if (currentEditingProduct) {
                // تحديث المنتج
                currentEditingProduct.name = name;
                currentEditingProduct.purchasePrice = purchasePrice;
                currentEditingProduct.salePrice = salePrice;
                currentEditingProduct.quantity = quantity;
                currentEditingProduct.category = category;
                currentEditingProduct.description = description;
            } else {
                // إضافة منتج جديد
                const product = {
                    id: Date.now(),
                    name: name,
                    purchasePrice: purchasePrice,
                    salePrice: salePrice,
                    quantity: quantity,
                    category: category,
                    description: description,
                    createdAt: new Date().toISOString()
                };
                products.push(product);
            }
            
            saveData();
            closeModal('productModal');
            
            showAlert(
                currentEditingProduct ? 'تم تحديث المنتج بنجاح' : 'تم إضافة المنتج بنجاح',
                'success',
                'productMessage'
            );
            
            loadData();
        }

        // تعديل المنتج
        function editProduct(productId) {
            openProductModal(productId);
        }

        // حذف المنتج
        function deleteProduct(productId) {
            if (confirm('هل أنت متأكد من حذف هذا المنتج؟')) {
                products = products.filter(p => p.id !== productId);
                saveData();
                showAlert('تم حذف المنتج بنجاح', 'success', 'productMessage');
                loadData();
            }
        }

        // تحديث المخزون
        function updateInventory(productId, change) {
            const product = products.find(p => p.id === productId);
            if (product) {
                const newQuantity = product.quantity + change;
                if (newQuantity >= 0) {
                    product.quantity = newQuantity;
                    saveData();
                    showAlert('تم تحديث المخزون بنجاح', 'success');
                    loadData();
                } else {
                    showAlert('لا يمكن أن تكون الكمية أقل من الصفر', 'danger');
                }
            }
        }

        // حذف معاملة
        function deleteTransaction(transactionId) {
            if (confirm('هل أنت متأكد من حذف هذه المعاملة؟')) {
                transactions = transactions.filter(t => t.id !== transactionId);
                saveData();
                showAlert('تم حذف المعاملة بنجاح', 'success');
                loadData();
            }
        }

        // إنشاء الرسم البياني الشهري
        function createMonthlyChart() {
            const ctx = document.getElementById('monthlyProfitChart').getContext('2d');
            
            // تجميع البيانات الشهرية
            const monthlyData = {};
            const currentYear = new Date().getFullYear();
            
            transactions.forEach(transaction => {
                const date = new Date(transaction.date);
                if (date.getFullYear() === currentYear) {
                    const month = date.getMonth();
                    if (!monthlyData[month]) {
                        monthlyData[month] = { income: 0, expenses: 0 };
                    }
                    
                    if (transaction.type === 'income') {
                        monthlyData[month].income += transaction.amount;
                    } else {
                        monthlyData[month].expenses += transaction.amount;
                    }
                }
            });
            
            // تحضير البيانات للرسم البياني
            const months = ['يناير', 'فبراير', 'مارس', 'أبريل', 'مايو', 'يونيو', 'يوليو', 'أغسطس', 'سبتمبر', 'أكتوبر', 'نوفمبر', 'ديسمبر'];
            const incomeData = [];
            const expensesData = [];
            const profitData = [];
            
            for (let i = 0; i < 12; i++) {
                const data = monthlyData[i] || { income: 0, expenses: 0 };
                incomeData.push(data.income);
                expensesData.push(data.expenses);
                profitData.push(data.income - data.expenses);
            }
            
            // تدمير الرسم البياني السابق إذا كان موجوداً
            if (charts.monthlyProfit) {
                charts.monthlyProfit.destroy();
            }
            
            // إنشاء الرسم البياني الجديد
            charts.monthlyProfit = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: months,
                    datasets: [
                        {
                            label: 'الإيرادات',
                            data: incomeData,
                            borderColor: '#27ae60',
                            backgroundColor: 'rgba(39, 174, 96, 0.1)',
                            tension: 0.3,
                            fill: true
                        },
                        {
                            label: 'المصروفات',
                            data: expensesData,
                            borderColor: '#e74c3c',
                            backgroundColor: 'rgba(231, 76, 60, 0.1)',
                            tension: 0.3,
                            fill: true
                        },
                        {
                            label: 'صافي الربح',
                            data: profitData,
                            borderColor: '#3498db',
                            backgroundColor: 'rgba(52, 152, 219, 0.1)',
                            tension: 0.3,
                            fill: true
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    return formatNumber(value) + ' ' + settings.currency;
                                }
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'top',
                            rtl: true
                        },
                        tooltip: {
                            rtl: true,
                            callbacks: {
                                label: function(context) {
                                    return context.dataset.label + ': ' + formatNumber(context.parsed.y) + ' ' + settings.currency;
                                }
                            }
                        }
                    }
                }
            });
        }

        // حفظ البيانات
        function saveData() {
            localStorage.setItem('profitCalculator_transactions', JSON.stringify(transactions));
            localStorage.setItem('profitCalculator_products', JSON.stringify(products));
            localStorage.setItem('profitCalculator_settings', JSON.stringify(settings));
            calculateStats();
            createMonthlyChart();
        }

        // عرض الأقسام
        function showSection(sectionId) {
            // إخفاء جميع الأقسام
            document.querySelectorAll('.content-section').forEach(section => {
                section.style.display = 'none';
            });
            
            // إزالة النشاط من جميع الروابط
            document.querySelectorAll('.nav-links a').forEach(link => {
                link.classList.remove('active');
            });
            
            // إظهار القسم المطلوب
            document.getElementById(sectionId).style.display = 'block';
            
            // تفعيل الرابط المناسب
            document.querySelector(`.nav-links a[onclick*="${sectionId}"]`).classList.add('active');
            
            // تحديث عنوان الصفحة
            updatePageTitle(sectionId);
            
            // تحديث البيانات في القسم الجديد
            if (sectionId === 'transactions') {
                loadTransactions();
            } else if (sectionId === 'products') {
                loadProducts();
            } else if (sectionId === 'inventory') {
                loadInventory();
            }
        }

        // تحديث عنوان الصفحة
        function updatePageTitle(sectionId) {
            const titles = {
                dashboard: 'لوحة التحكم',
                transactions: 'إدارة المعاملات',
                products: 'إدارة المنتجات',
                inventory: 'إدارة المخزون'
            };
            
            const descriptions = {
                dashboard: 'نظرة عامة على أداء متجرك',
                transactions: 'إدارة جميع المعاملات المالية',
                products: 'إدارة منتجاتك وأسعارها',
                inventory: 'تتبع مخزون منتجاتك'
            };
            
            document.getElementById('pageTitle').textContent = titles[sectionId];
            document.getElementById('pageDescription').textContent = descriptions[sectionId];
        }

        // فتح مودال التقارير
        function openReportsModal() {
            const modal = document.getElementById('reportsModal');
            modal.style.display = 'flex';
            switchReportTab('daily');
        }

        // فتح مودال الإعدادات
        function openSettingsModal() {
            const modal = document.getElementById('settingsModal');
            modal.style.display = 'flex';
            switchSettingsTab('general');
        }

        // تبديل تبويبات التقارير
        function switchReportTab(tabName) {
            document.querySelectorAll('#reportsModal .tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            document.querySelectorAll('#reportsModal .tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            document.querySelector(`#reportsModal .tab[onclick*="${tabName}"]`).classList.add('active');
            document.getElementById(`${tabName}Report`).classList.add('active');
            
            // توليد تقرير التبويب المحدد
            generateReport(tabName);
        }

        // تبديل تبويبات الإعدادات
        function switchSettingsTab(tabName) {
            document.querySelectorAll('#settingsModal .tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            document.querySelectorAll('#settingsModal .tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            document.querySelector(`#settingsModal .tab[onclick*="${tabName}"]`).classList.add('active');
            document.getElementById(`${tabName}Settings`).classList.add('active');
        }

        // توليد التقارير
        function generateReport(type) {
            let income = 0, expenses = 0, profit = 0;
            const
