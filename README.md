<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>SAYYADI Metal Cutting Company - Management System</title>
<link href="https://fonts.googleapis.com/css2?family=Chakra+Petch:ital,wght@0,400;0,600;0,700;1,700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
  :root {
    --bg-base: #0c0e12;
    --bg-surface: #141820;
    --bg-card: #1c222d;
    --bg-card-hover: #252d3c;
    --border-color: #2e3748;
    --border-light: #414d63;
    
    --orange-primary: #ff6b00;
    --orange-glow: rgba(255, 107, 0, 0.25);
    --orange-hover: #e05d00;
    
    --steel-light: #e2e8f0;
    --steel-mid: #94a3b8;
    --steel-dark: #475569;
    
    --success: #10b981;
    --danger: #ef4444;
    --warning: #f59e0b;
    --info: #3b82f6;
    
    --font-heading: 'Chakra Petch', sans-serif;
    --font-body: 'Inter', sans-serif;
  }

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    -webkit-tap-highlight-color: transparent;
  }

  body {
    background-color: #050608;
    color: var(--steel-light);
    font-family: var(--font-body);
    font-size: 14px;
    line-height: 1.5;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Android Device Shell Container */
  .app-container {
    width: 100%;
    max-width: 480px;
    height: 100vh;
    max-height: 920px;
    background-color: var(--bg-base);
    display: flex;
    flex-direction: column;
    position: relative;
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.8), 0 0 30px rgba(255, 107, 0, 0.1);
    border: 1px solid var(--border-color);
    overflow: hidden;
  }

  @media (min-width: 500px) {
    .app-container {
      height: 92vh;
      border-radius: 28px;
    }
  }

  /* Lock Screen Modal */
  #pin-lock-screen {
    position: absolute;
    inset: 0;
    background-color: var(--bg-base);
    z-index: 9999;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 30px;
    background-image: radial-gradient(circle at 50% 30%, rgba(255,107,0,0.15) 0%, transparent 70%);
  }

  .lock-logo {
    width: 80px;
    height: 80px;
    background: linear-gradient(135deg, #2a3241 0%, #141820 100%);
    border: 2px solid var(--orange-primary);
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 36px;
    color: var(--orange-primary);
    margin-bottom: 20px;
    box-shadow: 0 0 20px var(--orange-glow);
  }

  .pin-dots {
    display: flex;
    gap: 15px;
    margin: 30px 0;
  }

  .dot {
    width: 16px;
    height: 16px;
    border-radius: 50%;
    border: 2px solid var(--steel-mid);
    transition: all 0.2s;
  }

  .dot.filled {
    background-color: var(--orange-primary);
    border-color: var(--orange-primary);
    box-shadow: 0 0 10px var(--orange-primary);
  }

  .keypad {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 15px;
    width: 100%;
    max-width: 280px;
  }

  .key-btn {
    background: var(--bg-card);
    border: 1px solid var(--border-color);
    color: var(--steel-light);
    font-family: var(--font-heading);
    font-size: 22px;
    font-weight: 700;
    height: 60px;
    border-radius: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: background 0.1s;
  }

  .key-btn:active {
    background: var(--orange-primary);
    color: #000;
  }

  /* App Header */
  .app-header {
    background: linear-gradient(180deg, #1a202c 0%, var(--bg-surface) 100%);
    padding: 15px 18px;
    border-bottom: 1px solid var(--border-color);
    display: flex;
    align-items: center;
    justify-content: space-between;
    z-index: 10;
    position: relative;
  }

  .header-brand {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .header-brand i {
    color: var(--orange-primary);
    font-size: 22px;
  }

  .header-title {
    font-family: var(--font-heading);
    font-size: 16px;
    font-weight: 700;
    letter-spacing: 0.5px;
    color: #fff;
    text-transform: uppercase;
  }

  .header-subtitle {
    font-size: 10px;
    color: var(--steel-mid);
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .header-actions {
    display: flex;
    gap: 10px;
  }

  .icon-btn {
    background: var(--bg-card);
    border: 1px solid var(--border-color);
    color: var(--steel-light);
    width: 38px;
    height: 38px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    position: relative;
  }

  .icon-btn:active {
    border-color: var(--orange-primary);
    color: var(--orange-primary);
  }

  /* App Content Area */
  .app-content {
    flex: 1;
    overflow-y: auto;
    padding: 16px;
    position: relative;
    scroll-behavior: smooth;
  }

  /* Custom Scrollbar */
  .app-content::-webkit-scrollbar {
    width: 4px;
  }
  .app-content::-webkit-scrollbar-thumb {
    background: var(--border-color);
    border-radius: 4px;
  }

  /* Bottom Navigation */
  .bottom-nav {
    background: var(--bg-surface);
    border-top: 1px solid var(--border-color);
    display: flex;
    justify-content: space-around;
    padding: 8px 0 12px 0;
    z-index: 10;
  }

  .nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
    color: var(--steel-mid);
    text-decoration: none;
    font-size: 10px;
    font-weight: 500;
    cursor: pointer;
    width: 20%;
    transition: color 0.2s;
  }

  .nav-item i {
    font-size: 18px;
  }

  .nav-item.active {
    color: var(--orange-primary);
  }

  /* General Components */
  .view-panel {
    display: none;
  }
  .view-panel.active {
    display: block;
    animation: fadeIn 0.25s ease-in-out;
  }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(6px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .filter-bar {
    display: flex;
    background: var(--bg-card);
    border-radius: 12px;
    padding: 4px;
    margin-bottom: 16px;
    border: 1px solid var(--border-color);
  }

  .filter-btn {
    flex: 1;
    background: transparent;
    border: none;
    color: var(--steel-mid);
    padding: 8px 0;
    font-size: 12px;
    font-weight: 600;
    border-radius: 8px;
    cursor: pointer;
    text-align: center;
    transition: all 0.2s;
  }

  .filter-btn.active {
    background: var(--orange-primary);
    color: #000;
  }

  .card {
    background: var(--bg-card);
    border: 1px solid var(--border-color);
    border-radius: 16px;
    padding: 16px;
    margin-bottom: 16px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  }

  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 12px;
  }

  .card-title {
    font-family: var(--font-heading);
    font-size: 14px;
    font-weight: 700;
    color: var(--steel-light);
    display: flex;
    align-items: center;
    gap: 8px;
    text-transform: uppercase;
  }

  .card-title i {
    color: var(--orange-primary);
  }

  .kpi-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
    margin-bottom: 16px;
  }

  .kpi-card {
    background: var(--bg-card);
    border: 1px solid var(--border-color);
    border-radius: 14px;
    padding: 14px;
    display: flex;
    flex-direction: column;
    position: relative;
    overflow: hidden;
  }

  .kpi-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 3px;
    height: 100%;
    background: var(--border-light);
  }

  .kpi-card.income::before { background: var(--success); }
  .kpi-card.expenses::before { background: var(--danger); }
  .kpi-card.profit::before { background: var(--orange-primary); }
  .kpi-card.jobs::before { background: var(--info); }

  .kpi-label {
    font-size: 11px;
    color: var(--steel-mid);
    margin-bottom: 4px;
    text-transform: uppercase;
    font-weight: 600;
  }

  .kpi-value {
    font-family: var(--font-heading);
    font-size: 18px;
    font-weight: 700;
    color: #fff;
  }

  .kpi-value.income { color: var(--success); }
  .kpi-value.expenses { color: var(--danger); }
  .kpi-value.profit { color: var(--orange-primary); }

  .quick-actions {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    margin-bottom: 16px;
  }

  .action-btn {
    background: var(--bg-card);
    border: 1px solid var(--border-color);
    border-radius: 12px;
    padding: 12px 8px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 6px;
    cursor: pointer;
    text-align: center;
    transition: border-color 0.2s;
  }

  .action-btn i {
    font-size: 20px;
    color: var(--orange-primary);
  }

  .action-btn span {
    font-size: 11px;
    font-weight: 600;
    color: var(--steel-light);
  }

  .action-btn:active {
    border-color: var(--orange-primary);
    background: var(--bg-card-hover);
  }

  /* Form Controls */
  .form-group {
    margin-bottom: 14px;
  }

  .form-label {
    display: block;
    font-size: 12px;
    color: var(--steel-mid);
    margin-bottom: 6px;
    font-weight: 500;
  }

  .form-control {
    width: 100%;
    background: var(--bg-surface);
    border: 1px solid var(--border-color);
    border-radius: 10px;
    padding: 10px 12px;
    color: #fff;
    font-family: var(--font-body);
    font-size: 14px;
    outline: none;
  }

  .form-control:focus {
    border-color: var(--orange-primary);
  }

  select.form-control {
    appearance: none;
    background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%2394a3b8' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
    background-repeat: no-repeat;
    background-position: right 10px center;
    background-size: 16px;
  }

  .btn {
    width: 100%;
    padding: 12px;
    border: none;
    border-radius: 10px;
    font-family: var(--font-heading);
    font-size: 14px;
    font-weight: 700;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .btn-primary {
    background: var(--orange-primary);
    color: #000;
    box-shadow: 0 4px 12px var(--orange-glow);
  }

  .btn-primary:active {
    background: var(--orange-hover);
  }

  .btn-secondary {
    background: var(--bg-card);
    color: var(--steel-light);
    border: 1px solid var(--border-color);
  }

  .btn-danger {
    background: rgba(239, 68, 68, 0.15);
    color: var(--danger);
    border: 1px solid var(--danger);
  }

  /* Lists & Records */
  .list-item {
    background: var(--bg-card);
    border: 1px solid var(--border-color);
    border-radius: 12px;
    padding: 12px;
    margin-bottom: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .list-info-main {
    font-weight: 600;
    font-size: 13px;
    color: #fff;
  }

  .list-info-sub {
    font-size: 11px;
    color: var(--steel-mid);
    margin-top: 2px;
  }

  .list-amount {
    font-family: var(--font-heading);
    font-weight: 700;
    font-size: 14px;
    text-align: right;
  }

  .status-badge {
    padding: 2px 8px;
    border-radius: 6px;
    font-size: 10px;
    font-weight: 700;
    text-transform: uppercase;
    display: inline-block;
  }

  .status-pending { background: rgba(245, 158, 11, 0.2); color: var(--warning); }
  .status-progress { background: rgba(59, 130, 246, 0.2); color: var(--info); }
  .status-completed { background: rgba(16, 185, 129, 0.2); color: var(--success); }
  .status-paid { background: rgba(16, 185, 129, 0.3); color: #fff; }

  /* Modal Slide Overlay */
  .modal-overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.7);
    backdrop-filter: blur(4px);
    z-index: 100;
    display: none;
    align-items: flex-end;
  }

  .modal-overlay.active {
    display: flex;
  }

  .modal-content {
    background: var(--bg-surface);
    border-top: 2px solid var(--orange-primary);
    border-radius: 20px 20px 0 0;
    width: 100%;
    max-height: 85%;
    overflow-y: auto;
    padding: 20px;
    animation: slideUp 0.25s ease-out;
  }

  @keyframes slideUp {
    from { transform: translateY(100%); }
    to { transform: translateY(0); }
  }

  .modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--border-color);
  }

  .modal-title {
    font-family: var(--font-heading);
    font-size: 16px;
    font-weight: 700;
    color: #fff;
    text-transform: uppercase;
  }

  /* WhatsApp Invoice Style Container */
  .invoice-container {
    background: #ffffff;
    color: #0c0e12;
    padding: 20px;
    border-radius: 12px;
    font-family: var(--font-body);
    font-size: 12px;
    border: 3px solid var(--orange-primary);
  }

  .invoice-header {
    text-align: center;
    border-bottom: 2px dashed #ccc;
    padding-bottom: 12px;
    margin-bottom: 12px;
  }

  .invoice-company {
    font-family: var(--font-heading);
    font-size: 18px;
    font-weight: 700;
    color: #0c0e12;
    text-transform: uppercase;
  }

  .invoice-table {
    width: 100%;
    border-collapse: collapse;
    margin: 12px 0;
  }

  .invoice-table th, .invoice-table td {
    padding: 6px;
    text-align: left;
    border-bottom: 1px solid #eee;
  }

  .invoice-total-row {
    font-weight: 700;
    font-size: 14px;
  }

  /* Drawer Menu */
  .drawer-menu {
    position: absolute;
    top: 0;
    right: 0;
    width: 75%;
    height: 100%;
    background: var(--bg-surface);
    z-index: 150;
    box-shadow: -5px 0 25px rgba(0,0,0,0.8);
    display: none;
    flex-direction: column;
    padding: 20px;
    border-left: 1px solid var(--border-color);
  }

  .drawer-menu.active {
    display: flex;
    animation: slideLeft 0.2s ease-out;
  }

  @keyframes slideLeft {
    from { transform: translateX(100%); }
    to { transform: translateX(0); }
  }

  .drawer-item {
    display: flex;
    align-items: center;
    gap: 14px;
    padding: 14px;
    color: var(--steel-light);
    border-bottom: 1px solid var(--border-color);
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
  }

  .drawer-item i {
    color: var(--orange-primary);
    width: 20px;
  }
</style>
</head>
<body>

<div class="app-container">
  
  <!-- PIN Lock Screen -->
  <div id-pin-lock-screen id="pin-lock-screen">
    <div class="lock-logo"><i class="fa-solid fa-industry"></i></div>
    <div style="font-family: var(--font-heading); font-size: 16px; font-weight:700;" id="txt-lock-title">SAYYADI METAL CUTTING</div>
    <div style="font-size: 12px; color: var(--steel-mid); margin-top: 4px;" id="txt-lock-sub">Enter Access PIN / Shigar da Passcode</div>
    <div class="pin-dots">
      <div class="dot" id="dot-1"></div>
      <div class="dot" id="dot-2"></div>
      <div class="dot" id="dot-3"></div>
      <div class="dot" id="dot-4"></div>
    </div>
    <div class="keypad">
      <button class="key-btn" onclick="pressPin('1')">1</button>
      <button class="key-btn" onclick="pressPin('2')">2</button>
      <button class="key-btn" onclick="pressPin('3')">3</button>
      <button class="key-btn" onclick="pressPin('4')">4</button>
      <button class="key-btn" onclick="pressPin('5')">5</button>
      <button class="key-btn" onclick="pressPin('6')">6</button>
      <button class="key-btn" onclick="pressPin('7')">7</button>
      <button class="key-btn" onclick="pressPin('8')">8</button>
      <button class="key-btn" onclick="pressPin('9')">9</button>
      <button class="key-btn" style="font-size:14px; color:var(--danger)" onclick="clearPin()">CLR</button>
      <button class="key-btn" onclick="pressPin('0')">0</button>
      <button class="key-btn" style="font-size:14px; color:var(--orange-primary)" onclick="checkPin()"><i class="fa-solid fa-check"></i></button>
    </div>
  </div>

  <!-- Header -->
  <div class="app-header">
    <div class="header-brand">
      <i class="fa-solid fa-fire-flame-curved"></i>
      <div>
        <div class="header-title">SAYYADI METAL</div>
        <div class="header-subtitle">Kano, Nigeria</div>
      </div>
    </div>
    <div class="header-actions">
      <button class="icon-btn" onclick="toggleLang()" title="Switch Language">
        <span id="lang-indicator" style="font-weight:700; font-size:11px; color:var(--orange-primary)">HA</span>
      </button>
      <button class="icon-btn" onclick="toggleDrawer()">
        <i class="fa-solid fa-bars"></i>
      </button>
    </div>
  </div>

  <!-- Drawer Side Navigation -->
  <div class="drawer-menu" id="drawer-menu">
    <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:20px;">
      <span style="font-family:var(--font-heading); font-weight:700; color:var(--orange-primary);" id="txt-drawer-title">MENU / SHAFUKA</span>
      <button class="icon-btn" onclick="toggleDrawer()"><i class="fa-solid fa-xmark"></i></button>
    </div>
    <div class="drawer-item" onclick="navigateFromDrawer('reports')"><i class="fa-solid fa-chart-line"></i> <span data-i18n="reports">Reports</span></div>
    <div class="drawer-item" onclick="navigateFromDrawer('invoices')"><i class="fa-solid fa-file-invoice"></i> <span data-i18n="invoices">Invoices / Receipts</span></div>
    <div class="drawer-item" onclick="navigateFromDrawer('customers')"><i class="fa-solid fa-address-book"></i> <span data-i18n="customers">Customers</span></div>
    <div class="drawer-item" onclick="navigateFromDrawer('profile')"><i class="fa-solid fa-building"></i> <span data-i18n="profile">Business Profile</span></div>
    <div class="drawer-item" onclick="navigateFromDrawer('settings')"><i class="fa-solid fa-gear"></i> <span data-i18n="settings">Settings</span></div>
    <div style="margin-top:auto; padding-top:20px; text-align:center; font-size:10px; color:var(--steel-dark);">
      SAYYADI METAL v2.4 Industrial Edition<br>Kofar Ruwa, Kano
    </div>
  </div>

  <!-- Main Scrollable Content -->
  <div class="app-content">

    <!-- DASHBOARD VIEW -->
    <div id="view-dashboard" class="view-panel active">
      
      <div class="filter-bar">
        <button class="filter-btn active" onclick="setDashboardTimeframe('weekly', this)" data-i18n="weekly">Weekly</button>
        <button class="filter-btn" onclick="setDashboardTimeframe('monthly', this)" data-i18n="monthly">Monthly</button>
        <button class="filter-btn" onclick="setDashboardTimeframe('yearly', this)" data-i18n="yearly">Yearly</button>
      </div>

      <div class="kpi-grid">
        <div class="kpi-card income">
          <div class="kpi-label" data-i18n="total_income">Total Income</div>
          <div class="kpi-value income" id="dash-income">₦0</div>
        </div>
        <div class="kpi-card expenses">
          <div class="kpi-label" data-i18n="total_expenses">Total Expenses</div>
          <div class="kpi-value expenses" id="dash-expenses">₦0</div>
        </div>
        <div class="kpi-card profit">
          <div class="kpi-label" data-i18n="net_profit">Net Profit</div>
          <div class="kpi-value profit" id="dash-profit">₦0</div>
        </div>
        <div class="kpi-card jobs">
          <div class="kpi-label" data-i18n="jobs_count">Total Jobs</div>
          <div class="kpi-value" id="dash-jobs">0</div>
        </div>
      </div>

      <!-- Quick Action Buttons -->
      <div class="quick-actions">
        <div class="action-btn" onclick="openModal('modal-income')">
          <i class="fa-solid fa-circle-plus" style="color:var(--success)"></i>
          <span data-i18n="add_income">+ Income</span>
        </div>
        <div class="action-btn" onclick="openModal('modal-expense')">
          <i class="fa-solid fa-circle-minus" style="color:var(--danger)"></i>
          <span data-i18n="add_expense">+ Expense</span>
        </div>
        <div class="action-btn" onclick="openModal('modal-worker-pay')">
          <i class="fa-solid fa-hand-holding-dollar" style="color:var(--orange-primary)"></i>
          <span data-i18n="pay_worker">Pay Worker</span>
        </div>
      </div>

      <!-- Financial Chart Card -->
      <div class="card">
        <div class="card-header">
          <div class="card-title"><i class="fa-solid fa-chart-pie"></i> <span data-i18n="expense_breakdown">Expense Breakdown</span></div>
        </div>
        <div style="height: 180px; position: relative;">
          <canvas id="chartExpense"></canvas>
        </div>
      </div>

      <!-- Category Expenses Overview Card -->
      <div class="card">
        <div class="card-header">
          <div class="card-title"><i class="fa-solid fa-list-check"></i> <span data-i18n="expense_summary">Category Totals</span></div>
        </div>
        <div style="display:flex; flex-direction:column; gap:8px;" id="dash-expense-categories">
          <!-- Populated by JS -->
        </div>
      </div>

    </div>

    <!-- JOBS VIEW -->
    <div id="view-jobs" class="view-panel">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;">
        <span style="font-family:var(--font-heading); font-weight:700; font-size:16px;" data-i18n="jobs_management">JOBS / AYYUKA</span>
        <button class="btn btn-primary" style="width:auto; padding:6px 12px; font-size:12px;" onclick="openModal('modal-job')">+ <span data-i18n="new_job">New Job</span></button>
      </div>

      <div id="jobs-list">
        <!-- Rendered via JavaScript -->
      </div>
    </div>

    <!-- INCOME VIEW -->
    <div id="view-income" class="view-panel">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;">
        <span style="font-family:var(--font-heading); font-weight:700; font-size:16px;" data-i18n="income_records">INCOME RECORDS</span>
        <button class="btn btn-primary" style="width:auto; padding:6px 12px; font-size:12px;" onclick="openModal('modal-income')">+ <span data-i18n="add">Add</span></button>
      </div>
      <div id="income-list">
        <!-- Rendered via JavaScript -->
      </div>
    </div>

    <!-- EXPENSES VIEW -->
    <div id="view-expenses" class="view-panel">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;">
        <span style="font-family:var(--font-heading); font-weight:700; font-size:16px;" data-i18n="expense_records">EXPENSE RECORDS</span>
        <button class="btn btn-primary" style="width:auto; padding:6px 12px; font-size:12px;" onclick="openModal('modal-expense')">+ <span data-i18n="add">Add</span></button>
      </div>
      <div id="expenses-list">
        <!-- Rendered via JavaScript -->
      </div>
    </div>

    <!-- WORKERS VIEW -->
    <div id="view-workers" class="view-panel">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;">
        <span style="font-family:var(--font-heading); font-weight:700; font-size:16px;" data-i18n="worker_management">WORKERS / MA'AIKATA</span>
        <div style="display:flex; gap:6px;">
          <button class="btn btn-secondary" style="width:auto; padding:6px 10px; font-size:11px;" onclick="openModal('modal-worker')">+ <span data-i18n="add_worker">Worker</span></button>
          <button class="btn btn-primary" style="width:auto; padding:6px 10px; font-size:11px;" onclick="openModal('modal-worker-pay')"><span data-i18n="pay">Pay</span></button>
        </div>
      </div>

      <div id="workers-list">
        <!-- Rendered via JavaScript -->
      </div>
    </div>

    <!-- REPORTS VIEW -->
    <div id="view-reports" class="view-panel">
      <div class="card">
        <div class="card-title" style="margin-bottom:12px;"><i class="fa-solid fa-file-invoice-dollar"></i> <span data-i18n="profit_loss_statement">PROFIT & LOSS STATEMENT</span></div>
        <div style="display:grid; grid-template-columns:1fr 1fr; gap:10px; text-align:center;">
          <div style="background:var(--bg-surface); padding:10px; border-radius:10px;">
            <div style="font-size:10px; color:var(--steel-mid);" data-i18n="today_profit">TODAY PROFIT</div>
            <div style="font-family:var(--font-heading); font-weight:700; color:var(--orange-primary);" id="rpt-today-profit">₦0</div>
          </div>
          <div style="background:var(--bg-surface); padding:10px; border-radius:10px;">
            <div style="font-size:10px; color:var(--steel-mid);" data-i18n="month_profit">THIS MONTH</div>
            <div style="font-family:var(--font-heading); font-weight:700; color:var(--orange-primary);" id="rpt-month-profit">₦0</div>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="card-title" style="margin-bottom:12px;"><i class="fa-solid fa-download"></i> <span data-i18n="export_reports">EXPORT DATA</span></div>
        <div class="form-group">
          <label class="form-label" data-i18n="filter_timeframe">Select Period</label>
          <select class="form-control" id="rpt-period">
            <option value="all">All Time / Dukkan Lokaci</option>
            <option value="month">This Month / Wannan Wata</option>
            <option value="week">This Week / Wannan Sati</option>
          </select>
        </div>
        <div style="display:flex; gap:10px; margin-top:10px;">
          <button class="btn btn-secondary" onclick="exportDataCSV()"><i class="fa-solid fa-file-csv"></i> CSV Export</button>
          <button class="btn btn-primary" onclick="window.print()"><i class="fa-solid fa-print"></i> Print PDF</button>
        </div>
      </div>
    </div>

    <!-- INVOICE VIEW -->
    <div id="view-invoices" class="view-panel">
      <div class="card">
        <div class="card-title" style="margin-bottom:10px;"><i class="fa-solid fa-receipt"></i> <span data-i18n="generate_invoice">GENERATE RECEIPT</span></div>
        <div class="form-group">
          <label class="form-label" data-i18n="select_job">Select Completed/Active Job</label>
          <select class="form-control" id="invoice-job-select" onchange="renderInvoicePreview()">
            <!-- Populated JS -->
          </select>
        </div>
      </div>

      <div id="invoice-preview-area">
        <!-- Rendered dynamic receipt -->
      </div>

      <button class="btn btn-primary" style="margin-top:12px;" onclick="shareInvoiceWhatsApp()"><i class="fa-brands fa-whatsapp"></i> <span data-i18n="share_whatsapp">Share via WhatsApp</span></button>
    </div>

    <!-- CUSTOMERS VIEW -->
    <div id="view-customers" class="view-panel">
      <div class="card-title" style="margin-bottom:12px;"><i class="fa-solid fa-users"></i> <span data-i18n="customer_directory">CUSTOMER DIRECTORY</span></div>
      <div id="customers-list">
        <!-- JS Render -->
      </div>
    </div>

    <!-- PROFILE VIEW -->
    <div id="view-profile" class="view-panel">
      <div class="card" style="text-align:center;">
        <div style="font-size:40px; color:var(--orange-primary); margin-bottom:10px;"><i class="fa-solid fa-industry"></i></div>
        <div style="font-family:var(--font-heading); font-size:18px; font-weight:700;">SAYYADI METAL CUTTING COMPANY</div>
        <div style="font-size:12px; color:var(--steel-mid); margin-top:4px;">Kofar Ruwa, Layin Sarkin Kasuwa, Kano, Nigeria</div>
        <div style="margin-top:12px; display:flex; justify-content:center; gap:10px;">
          <a href="tel:07019163808" class="btn btn-secondary" style="width:auto; padding:6px 12px; font-size:11px;"><i class="fa-solid fa-phone"></i> Call 07019163808</a>
          <a href="https://wa.me/2347019163808" class="btn btn-primary" style="width:auto; padding:6px 12px; font-size:11px;"><i class="fa-brands fa-whatsapp"></i> WhatsApp</a>
        </div>
      </div>

      <div class="card">
        <div class="card-title" style="margin-bottom:8px;"><i class="fa-solid fa-screwdriver-wrench"></i> <span data-i18n="our_services">OUR SERVICES / AYYUKANMU</span></div>
        <ul style="list-style-type:none; line-height:2.2; font-size:13px; color:var(--steel-light);">
          <li><i class="fa-solid fa-check" style="color:var(--orange-primary); margin-right:8px;"></i> Metal Cutting / Yankan Ƙarfe</li>
          <li><i class="fa-solid fa-check" style="color:var(--orange-primary); margin-right:8px;"></i> Steel Plate & Base Plate Cutting</li>
          <li><i class="fa-solid fa-check" style="color:var(--orange-primary); margin-right:8px;"></i> Oxygen & Cooking Gas Flame Services</li>
          <li><i class="fa-solid fa-check" style="color:var(--orange-primary); margin-right:8px;"></i> Heavy Machine & Rafta Custom Shaping</li>
        </ul>
      </div>
    </div>

    <!-- SETTINGS VIEW -->
    <div id="view-settings" class="view-panel">
      <div class="card">
        <div class="card-title" style="margin-bottom:12px;"><i class="fa-solid fa-sliders"></i> <span data-i18n="app_settings">APP SETTINGS</span></div>
        
        <div class="form-group">
          <label class="form-label" data-i18n="app_language">App Language</label>
          <select class="form-control" id="setting-language" onchange="changeLanguage(this.value)">
            <option value="en">English</option>
            <option value="ha">Hausa (Harshen Hausa)</option>
          </select>
        </div>

        <div class="form-group">
          <label class="form-label" data-i18n="security_pin">Security Lock PIN (4 Digits)</label>
          <input type="number" class="form-control" id="setting-pin" placeholder="Default: 1234">
        </div>

        <button class="btn btn-primary" onclick="saveSettings()" style="margin-bottom:15px;"><span data-i18n="save_settings">Save Settings</span></button>

        <hr style="border-color:var(--border-color); margin:15px 0;">

        <div class="card-title" style="margin-bottom:12px;"><i class="fa-solid fa-database"></i> <span data-i18n="data_management">DATA MANAGEMENT</span></div>
        <div style="display:flex; flex-direction:column; gap:10px;">
          <button class="btn btn-secondary" onclick="exportFullBackup()"><i class="fa-solid fa-file-export"></i> Export Backup JSON</button>
          <button class="btn btn-danger" onclick="resetAllData()"><i class="fa-solid fa-trash"></i> Reset All Business Records</button>
        </div>
      </div>
    </div>

  </div>

  <!-- Bottom Navigation Bar -->
  <div class="bottom-nav">
    <div class="nav-item active" onclick="switchTab('dashboard', this)">
      <i class="fa-solid fa-gauge-high"></i>
      <span data-i18n="nav_dashboard">Dashboard</span>
    </div>
    <div class="nav-item" onclick="switchTab('jobs', this)">
      <i class="fa-solid fa-fire-burner"></i>
      <span data-i18n="nav_jobs">Jobs</span>
    </div>
    <div class="nav-item" onclick="switchTab('income', this)">
      <i class="fa-solid fa-wallet"></i>
      <span data-i18n="nav_income">Income</span>
    </div>
    <div class="nav-item" onclick="switchTab('expenses', this)">
      <i class="fa-solid fa-receipt"></i>
      <span data-i18n="nav_expenses">Expenses</span>
    </div>
    <div class="nav-item" onclick="switchTab('workers', this)">
      <i class="fa-solid fa-user-gear"></i>
      <span data-i18n="nav_workers">Workers</span>
    </div>
  </div>

  <!-- MODALS -->

  <!-- Add Income Modal -->
  <div class="modal-overlay" id="modal-income">
    <div class="modal-content">
      <div class="modal-header">
        <div class="modal-title" data-i18n="record_income">RECORD INCOME / KUƊIN SHIGA</div>
        <button class="icon-btn" onclick="closeModal('modal-income')"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form onsubmit="saveIncome(event)">
        <div class="form-group">
          <label class="form-label" data-i18n="date">Date</label>
          <input type="date" class="form-control" id="inc-date" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="customer_name">Customer Name</label>
          <input type="text" class="form-control" id="inc-customer" placeholder="e.g. Alhaji Sani" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="job_description">Job Description</label>
          <input type="text" class="form-control" id="inc-desc" placeholder="e.g. 12mm Base Plate Cut" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="amount_naira">Amount Received (₦)</label>
          <input type="number" class="form-control" id="inc-amount" placeholder="0.00" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="payment_method">Payment Method</label>
          <select class="form-control" id="inc-method">
            <option value="Cash">Cash / Tsagaron Kuɗi</option>
            <option value="Bank Transfer">Bank Transfer / Tura Banki</option>
            <option value="Other">Other</option>
          </select>
        </div>
        <button type="submit" class="btn btn-primary" data-i18n="save_record">Save Income Record</button>
      </form>
    </div>
  </div>

  <!-- Add Expense Modal -->
  <div class="modal-overlay" id="modal-expense">
    <div class="modal-content">
      <div class="modal-header">
        <div class="modal-title" data-i18n="record_expense">RECORD EXPENSE / KUƊIN KASHEWA</div>
        <button class="icon-btn" onclick="closeModal('modal-expense')"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form onsubmit="saveExpense(event)">
        <div class="form-group">
          <label class="form-label" data-i18n="date">Date</label>
          <input type="date" class="form-control" id="exp-date" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="category">Category</label>
          <select class="form-control" id="exp-cat">
            <option value="Oxygen">Oxygen (Refill / Cylinder)</option>
            <option value="Cooking Gas">Cooking Gas Refill</option>
            <option value="Transport">Transport / Delivery / Fuel</option>
            <option value="Other">Other (Tools / Repairs / Maintenance)</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="amount_naira">Amount Spent (₦)</label>
          <input type="number" class="form-control" id="exp-amount" placeholder="0.00" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="description">Description</label>
          <input type="text" class="form-control" id="exp-desc" placeholder="e.g. Oxygen cylinder refill 2 big tanks" required>
        </div>
        <button type="submit" class="btn btn-primary" data-i18n="save_record">Save Expense Record</button>
      </form>
    </div>
  </div>

  <!-- Create Worker Modal -->
  <div class="modal-overlay" id="modal-worker">
    <div class="modal-content">
      <div class="modal-header">
        <div class="modal-title" data-i18n="add_new_worker">ADD WORKER / MA'AIKACI</div>
        <button class="icon-btn" onclick="closeModal('modal-worker')"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form onsubmit="saveWorker(event)">
        <div class="form-group">
          <label class="form-label" data-i18n="worker_name">Worker Full Name</label>
          <input type="text" class="form-control" id="wrk-name" placeholder="e.g. Ibrahim Musa" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="phone">Phone Number</label>
          <input type="tel" class="form-control" id="wrk-phone" placeholder="08012345678">
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="position">Position / Role</label>
          <input type="text" class="form-control" id="wrk-role" placeholder="e.g. Cutter / Machine Assistant">
        </div>
        <button type="submit" class="btn btn-primary" data-i18n="save_record">Create Worker Profile</button>
      </form>
    </div>
  </div>

  <!-- Worker Payment Modal -->
  <div class="modal-overlay" id="modal-worker-pay">
    <div class="modal-content">
      <div class="modal-header">
        <div class="modal-title" data-i18n="pay_worker">RECORD WORKER PAYMENT</div>
        <button class="icon-btn" onclick="closeModal('modal-worker-pay')"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form onsubmit="saveWorkerPayment(event)">
        <div class="form-group">
          <label class="form-label" data-i18n="select_worker">Select Worker</label>
          <select class="form-control" id="wpay-worker" required>
            <!-- Populated via JS -->
          </select>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="date">Date</label>
          <input type="date" class="form-control" id="wpay-date" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="amount_naira">Amount Paid (₦)</label>
          <input type="number" class="form-control" id="wpay-amount" placeholder="0.00" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="payment_type">Payment Type</label>
          <select class="form-control" id="wpay-type">
            <option value="Daily Payment">Daily Payment / Albashin Yau</option>
            <option value="Salary">Salary / Albashin Wata</option>
            <option value="Advance">Advance / Bashi</option>
            <option value="Transport">Transport Allowance</option>
            <option value="Other">Other</option>
          </select>
        </div>
        <button type="submit" class="btn btn-primary" data-i18n="save_record">Record Payment</button>
      </form>
    </div>
  </div>

  <!-- New Job Modal -->
  <div class="modal-overlay" id="modal-job">
    <div class="modal-content">
      <div class="modal-header">
        <div class="modal-title" data-i18n="create_job">CREATE METAL CUTTING JOB</div>
        <button class="icon-btn" onclick="closeModal('modal-job')"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <form onsubmit="saveJob(event)">
        <div class="form-group">
          <label class="form-label" data-i18n="customer_name">Customer Name</label>
          <input type="text" class="form-control" id="job-customer" placeholder="e.g. Alhaji Kabiru" required>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="phone">Phone Number</label>
          <input type="tel" class="form-control" id="job-phone" placeholder="070...">
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="job_type">Job Type</label>
          <select class="form-control" id="job-type">
            <option value="Base Plate Cutting">Base Plate Cutting</option>
            <option value="Steel Cutting">Steel Cutting</option>
            <option value="Metal Cutting">Metal Cutting / Yankan Ƙarfe</option>
            <option value="Machine/Rafta Cutting">Machine / Rafta Cutting</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label" data-i18n="job_description">Job Details</label>
          <input type="text" class="form-control" id="job-desc" placeholder="e.g. 10 Pcs Steel Rafta 15mm" required>
        </div>
        <div style="display:grid; grid-template-columns:1fr 1fr; gap:10px;">
          <div class="form-group">
            <label class="form-label" data-i18n="total_charge">Total Charge (₦)</label>
            <input type="number" class="form-control" id="job-charge" placeholder="0.00" required>
          </div>
          <div class="form-group">
            <label class="form-label" data-i18n="deposit_paid">Paid Now (₦)</label>
            <input type="number" class="form-control" id="job-paid" placeholder="0.00" value="0">
          </div>
        </div>
        <button type="submit" class="btn btn-primary" data-i18n="save_record">Create Job Record</button>
      </form>
    </div>
  </div>

</div>

<script>
  /* ================= Global Application State ================= */
  let appState = {
    settings: {
      lang: 'en',
      pin: '1234',
      currency: '₦'
    },
    incomes: [],
    expenses: [],
    workers: [],
    workerPayments: [],
    jobs: []
  };

  let dashboardFilter = 'weekly';
  let enteredPin = '';
  let chartInstance = null;

  const translations = {
    en: {
      weekly: "Weekly",
      monthly: "Monthly",
      yearly: "Yearly",
      total_income: "Total Income",
      total_expenses: "Total Expenses",
      net_profit: "Net Profit",
      jobs_count: "Total Jobs",
      add_income: "+ Income",
      add_expense: "+ Expense",
      pay_worker: "Pay Worker",
      expense_breakdown: "Expense Breakdown",
      expense_summary: "Category Totals",
      jobs_management: "JOBS MANAGEMENT",
      new_job: "New Job",
      income_records: "INCOME RECORDS",
      expense_records: "EXPENSE RECORDS",
      worker_management: "WORKER MANAGEMENT",
      add_worker: "Worker",
      pay: "Pay",
      reports: "Reports & Financials",
      invoices: "Invoices & Receipts",
      customers: "Customer Records",
      profile: "Company Profile",
      settings: "App Settings",
      nav_dashboard: "Dashboard",
      nav_jobs: "Jobs",
      nav_income: "Income",
      nav_expenses: "Expenses",
      nav_workers: "Workers",
      record_income: "RECORD INCOME",
      record_expense: "RECORD EXPENSE",
      add_new_worker: "ADD NEW WORKER",
      create_job: "CREATE METAL JOB",
      date: "Date",
      customer_name: "Customer Name",
      job_description: "Job Description",
      amount_naira: "Amount (₦)",
      payment_method: "Payment Method",
      category: "Category",
      description: "Description",
      worker_name: "Worker Full Name",
      phone: "Phone Number",
      position: "Position / Role",
      save_record: "Save Record",
      select_worker: "Select Worker",
      payment_type: "Payment Type",
      job_type: "Job Category",
      total_charge: "Total Charge (₦)",
      deposit_paid: "Deposit Paid (₦)",
      profit_loss_statement: "PROFIT & LOSS STATEMENT",
      today_profit: "TODAY PROFIT",
      month_profit: "THIS MONTH PROFIT",
      export_reports: "EXPORT REPORTS",
      filter_timeframe: "Timeframe",
      generate_invoice: "INVOICE GENERATOR",
      select_job: "Select Job",
      share_whatsapp: "Share via WhatsApp",
      customer_directory: "CUSTOMER DIRECTORY",
      our_services: "OUR INDUSTRIAL SERVICES",
      app_settings: "SYSTEM SETTINGS",
      app_language: "App Language",
      security_pin: "App PIN Lock",
      save_settings: "Save Settings",
      data_management: "DATA BACKUP & RESET"
    },
    ha: {
      weekly: "Mako",
      monthly: "Wata",
      yearly: "Shekara",
      total_income: "Kuɗin Shiga",
      total_expenses: "Kuɗin Kashewa",
      net_profit: "Riba Kalas",
      jobs_count: "Ayyuka",
      add_income: "+ Kuɗin Shiga",
      add_expense: "+ Kashewa",
      pay_worker: "Biyan Ma'aikaci",
      expense_breakdown: "Rarrabuwar Kashewa",
      expense_summary: "Jimillar Rukunai",
      jobs_management: "SHAFIN AYYUKA",
      new_job: "Sabon Aiki",
      income_records: "LITTAFIN KUƊIN SHIGA",
      expense_records: "LITTAFIN KASHEWA",
      worker_management: "SHAFIN MA'AIKATA",
      add_worker: "Ma'aikaci",
      pay: "Biya",
      reports: "Rahotanni & Riba",
      invoices: "Rasiɗi & Invoice",
      customers: "Abokan Ciniki",
      profile: "Bayanin Kamfani",
      settings: "Saitunan Manhaja",
      nav_dashboard: "Babban Shafi",
      nav_jobs: "Ayyuka",
      nav_income: "Shiga",
      nav_expenses: "Kashewa",
      nav_workers: "Ma'aikata",
      record_income: "SHIGA DA KUƊIN SHIGA",
      record_expense: "SHIGA DA KASHEWA",
      add_new_worker: "SABON MA'AIKACI",
      create_job: "SABON AIKIN YANKAN ƘARFE",
      date: "Kwanan Wata",
      customer_name: "Sunan Abokin Ciniki",
      job_description: "Bayanin Aiki",
      amount_naira: "Adadi (₦)",
      payment_method: "Hanyar Biya",
      category: "Rukuni",
      description: "Bayanin Dalla-Dalla",
      worker_name: "Sunan Ma'aikaci",
      phone: "Lamba Tarho",
      position: "Matsayi / Aiki",
      save_record: "Ajiye Bayani",
      select_worker: "Zaɓi Ma'aikaci",
      payment_type: "Nau'in Biya",
      job_type: "Rukunin Aiki",
      total_charge: "Kuɗin Aiki Baki Ɗaya (₦)",
      deposit_paid: "Kuɗin Da Aka Biya (₦)",
      profit_loss_statement: "LITTAFIN RIBA DA ASARA",
      today_profit: "RIBAR YAU",
      month_profit: "RIBAR WANNAN WATA",
      export_reports: "FITAR DA RAHOTO",
      filter_timeframe: "Zaɓi Lokaci",
      generate_invoice: "HAƊA RASIƊI / INVOICE",
      select_job: "Zaɓi Aiki",
      share_whatsapp: "Tura ta WhatsApp",
      customer_directory: "LITTAFIN ABOKAN CINIKI",
      our_services: "AYYUKANMU TA YANKAN ƘARFE",
      app_settings: "SAITUNAN MANHAJA",
      app_language: "Harshen Manhaja",
      security_pin: "Lambar Sirri (PIN)",
      save_settings: "Ajiye Saituna",
      data_management: "SARAFA BAYANAI & RESET"
    }
  };

  /* ================= Startup Initialization ================= */
  window.addEventListener('DOMContentLoaded', () => {
    loadDataFromStorage();
    setTodayDates();
    renderAllViews();
    applyLanguage(appState.settings.lang);
  });

  function setTodayDates() {
    const today = new Date().toISOString().split('T')[0];
    ['inc-date', 'exp-date', 'wpay-date'].forEach(id => {
      const el = document.getElementById(id);
      if(el) el.value = today;
    });
  }

  /* ================= Local Storage Operations ================= */
  function saveDataToStorage() {
    localStorage.setItem('SAYYADI_METAL_DATA', JSON.stringify(appState));
    renderAllViews();
  }

  function loadDataFromStorage() {
    const stored = localStorage.getItem('SAYYADI_METAL_DATA');
    if (stored) {
      try {
        appState = JSON.parse(stored);
      } catch (e) {
        console.error("Data restore error", e);
      }
    } else {
      // Load Initial Sample Seed Data if empty
      seedInitialData();
    }
  }

  function seedInitialData() {
    const today = new Date().toISOString().split('T')[0];
    appState = {
      settings: { lang: 'en', pin: '1234', currency: '₦' },
      incomes: [
        { id: 101, date: today, customer: 'Alhaji Umar', desc: '16mm Steel Plate Cutting', amount: 45000, method: 'Bank Transfer' },
        { id: 102, date: today, customer: 'Musa Tanko', desc: 'Machine Rafta Shaping', amount: 28000, method: 'Cash' }
      ],
      expenses: [
        { id: 201, date: today, category: 'Oxygen', amount: 12000, desc: 'Oxygen Refill 1 Large Cylinder' },
        { id: 202, date: today, category: 'Cooking Gas', amount: 8500, desc: 'Gas Refill 12.5kg' }
      ],
      workers: [
        { id: 1, name: 'Sani Abdullahi', phone: '08039281722', role: 'Chief Flame Torch Cutter' }
      ],
      workerPayments: [
        { id: 301, workerId: 1, date: today, amount: 5000, type: 'Daily Payment' }
      ],
      jobs: [
        { id: 401, customer: 'Alhaji Umar', phone: '08031112233', type: 'Base Plate Cutting', desc: '16mm Steel Plate', charge: 45000, paid: 45000, status: 'Completed', date: today }
      ]
    };
    saveDataToStorage();
  }

  /* ================= Lock Screen Logic ================= */
  function pressPin(num) {
    if (enteredPin.length < 4) {
      enteredPin += num;
      updatePinDots();
    }
  }

  function clearPin() {
    enteredPin = '';
    updatePinDots();
  }

  function updatePinDots() {
    for (let i = 1; i <= 4; i++) {
      const dot = document.getElementById(`dot-${i}`);
      if (i <= enteredPin.length) dot.classList.add('filled');
      else dot.classList.remove('filled');
    }
  }

  function checkPin() {
    const correctPin = appState.settings.pin || '1234';
    if (enteredPin === correctPin) {
      document.getElementById('pin-lock-screen').style.display = 'none';
      enteredPin = '';
      updatePinDots();
    } else {
      alert('Incorrect PIN Code / Lambar Sirri Ba Ta Yi Ba');
      clearPin();
    }
  }

  /* ================= Navigation & Drawers ================= */
  function switchTab(viewName, element) {
    document.querySelectorAll('.view-panel').forEach(el => el.classList.remove('active'));
    document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
    
    document.getElementById(`view-${viewName}`).classList.add('active');
    if (element) element.classList.add('active');
  }

  function toggleDrawer() {
    const drawer = document.getElementById('drawer-menu');
    drawer.classList.toggle('active');
  }

  function navigateFromDrawer(viewName) {
    toggleDrawer();
    document.querySelectorAll('.view-panel').forEach(el => el.classList.remove('active'));
    document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
    document.getElementById(`view-${viewName}`).classList.add('active');
  }

  function openModal(id) {
    if(id === 'modal-worker-pay') populateWorkerDropdown();
    document.getElementById(id).classList.add('active');
  }

  function closeModal(id) {
    document.getElementById(id).classList.remove('active');
  }

  /* ================= Language Switching ================= */
  function toggleLang() {
    const newLang = appState.settings.lang === 'en' ? 'ha' : 'en';
    changeLanguage(newLang);
  }

  function changeLanguage(lang) {
    appState.settings.lang = lang;
    document.getElementById('lang-indicator').innerText = lang.toUpperCase();
    applyLanguage(lang);
    saveDataToStorage();
  }

  function applyLanguage(lang) {
    const dict = translations[lang] || translations.en;
    document.querySelectorAll('[data-i18n]').forEach(el => {
      const key = el.getAttribute('data-i18n');
      if (dict[key]) el.innerText = dict[key];
    });
  }

  /* ================= Render & Calculations Engine ================= */
  function setDashboardTimeframe(tf, btn) {
    dashboardFilter = tf;
    document.querySelectorAll('.filter-bar .filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    renderDashboard();
  }

  function renderAllViews() {
    renderDashboard();
    renderJobs();
    renderIncomeList();
    renderExpensesList();
    renderWorkersList();
    renderReports();
    renderCustomers();
    populateInvoiceDropdown();
  }

  function filterByTimeframe(items, timeframe) {
    const now = new Date();
    return items.filter(item => {
      const itemDate = new Date(item.date);
      if (isNaN(itemDate.getTime())) return true;
      if (timeframe === 'weekly') {
        const oneWeekAgo = new Date(now.getTime() - 7 * 24 * 60 * 60 * 1000);
        return itemDate >= oneWeekAgo;
      } else if (timeframe === 'monthly') {
        return itemDate.getMonth() === now.getMonth() && itemDate.getFullYear() === now.getFullYear();
      } else if (timeframe === 'yearly') {
        return itemDate.getFullYear() === now.getFullYear();
      }
      return true;
    });
  }

  function renderDashboard() {
    const filteredIncome = filterByTimeframe(appState.incomes, dashboardFilter);
    const filteredExpense = filterByTimeframe(appState.expenses, dashboardFilter);
    const filteredWorkerPay = filterByTimeframe(appState.workerPayments, dashboardFilter);
    const filteredJobs = filterByTimeframe(appState.jobs, dashboardFilter);

    const totalIncome = filteredIncome.reduce((sum, item) => sum + Number(item.amount), 0);
    const directExpenses = filteredExpense.reduce((sum, item) => sum + Number(item.amount), 0);
    const workerExpenses = filteredWorkerPay.reduce((sum, item) => sum + Number(item.amount), 0);
    const totalExpenses = directExpenses + workerExpenses;
    const netProfit = totalIncome - totalExpenses;

    document.getElementById('dash-income').innerText = `₦${totalIncome.toLocaleString()}`;
    document.getElementById('dash-expenses').innerText = `₦${totalExpenses.toLocaleString()}`;
    document.getElementById('dash-profit').innerText = `₦${netProfit.toLocaleString()}`;
    document.getElementById('dash-jobs').innerText = filteredJobs.length;

    // Categorized breakdown for chart & list
    const categories = { Oxygen: 0, 'Cooking Gas': 0, Transport: 0, Workers: workerExpenses, Other: 0 };
    filteredExpense.forEach(exp => {
      const cat = exp.category || 'Other';
      if (categories[cat] !== undefined) categories[cat] += Number(exp.amount);
      else categories['Other'] += Number(exp.amount);
    });

    renderExpenseChart(categories);
    
    // Render Category summary list
    const categoryContainer = document.getElementById('dash-expense-categories');
    categoryContainer.innerHTML = '';
    Object.keys(categories).forEach(cat => {
      categoryContainer.innerHTML += `
        <div style="display:flex; justify-content:space-between; font-size:12px; padding:6px 0; border-bottom:1px solid var(--border-color)">
          <span style="color:var(--steel-mid);"><i class="fa-solid fa-angle-right" style="color:var(--orange-primary)"></i> ${cat}</span>
          <span style="font-weight:700; color:#fff;">₦${categories[cat].toLocaleString()}</span>
        </div>
      `;
    });
  }

  function renderExpenseChart(dataObj) {
    const ctx = document.getElementById('chartExpense').getContext('2d');
    if (chartInstance) chartInstance.destroy();

    chartInstance = new Chart(ctx, {
      type: 'doughnut',
      data: {
        labels: Object.keys(dataObj),
        datasets: [{
          data: Object.values(dataObj),
          backgroundColor: ['#ef4444', '#f59e0b', '#3b82f6', '#ff6b00', '#64748b'],
          borderWidth: 2,
          borderColor: '#1c222d'
        }]
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: { position: 'right', labels: { color: '#94a3b8', font: { size: 10 } } }
        }
      }
    });
  }

  function renderJobs() {
    const container = document.getElementById('jobs-list');
    container.innerHTML = '';
    if (appState.jobs.length === 0) {
      container.innerHTML = `<div style="text-align:center; padding:30px; color:var(--steel-mid);">No active jobs. Tap "+ New Job" to create one.</div>`;
      return;
    }

    appState.jobs.slice().reverse().forEach(job => {
      const balance = Number(job.charge) - Number(job.paid);
      let statusClass = 'status-pending';
      if (job.status === 'Completed') statusClass = 'status-completed';
      if (job.status === 'In Progress') statusClass = 'status-progress';

      container.innerHTML += `
        <div class="card">
          <div class="card-header">
            <div>
              <div style="font-weight:700; font-size:15px; color:#fff;">${job.customer}</div>
              <div style="font-size:11px; color:var(--steel-mid);">${job.phone || 'No phone'} | ${job.date}</div>
            </div>
            <span class="status-badge ${statusClass}">${job.status}</span>
          </div>
          <div style="font-size:13px; color:var(--steel-light); margin-bottom:10px;">
            <strong style="color:var(--orange-primary);">${job.type}:</strong> ${job.desc}
          </div>
          <div style="display:flex; justify-content:space-between; font-size:12px; background:var(--bg-surface); padding:8px 12px; border-radius:8px;">
            <div>Total: <strong>₦${Number(job.charge).toLocaleString()}</strong></div>
            <div>Paid: <strong style="color:var(--success);">₦${Number(job.paid).toLocaleString()}</strong></div>
            <div>Bal: <strong style="color:var(--danger);">₦${balance.toLocaleString()}</strong></div>
          </div>
        </div>
      `;
    });
  }

  function renderIncomeList() {
    const container = document.getElementById('income-list');
    container.innerHTML = '';
    appState.incomes.slice().reverse().forEach(inc => {
      container.innerHTML += `
        <div class="list-item">
          <div>
            <div class="list-info-main">${inc.customer}</div>
            <div class="list-info-sub">${inc.desc} • ${inc.date}</div>
          </div>
          <div class="list-amount" style="color:var(--success);">+₦${Number(inc.amount).toLocaleString()}</div>
        </div>
      `;
    });
  }

  function renderExpensesList() {
    const container = document.getElementById('expenses-list');
    container.innerHTML = '';
    
    // Combine regular expenses and worker payments for overall expense view
    const allExp = [
      ...appState.expenses.map(e => ({ ...e, isWorker: false })),
      ...appState.workerPayments.map(w => {
        const worker = appState.workers.find(x => x.id == w.workerId);
        return {
          id: w.id,
          date: w.date,
          category: 'Worker Payment',
          amount: w.amount,
          desc: `Paid to ${worker ? worker.name : 'Worker'} (${w.type})`,
          isWorker: true
        };
      })
    ].sort((a,b) => new Date(b.date) - new Date(a.date));

    allExp.forEach(exp => {
      container.innerHTML += `
        <div class="list-item">
          <div>
            <div class="list-info-main">${exp.category}</div>
            <div class="list-info-sub">${exp.desc} • ${exp.date}</div>
          </div>
          <div class="list-amount" style="color:var(--danger);">-₦${Number(exp.amount).toLocaleString()}</div>
        </div>
      `;
    });
  }

  function renderWorkersList() {
    const container = document.getElementById('workers-list');
    container.innerHTML = '';
    if (appState.workers.length === 0) {
      container.innerHTML = `<div style="text-align:center; padding:30px; color:var(--steel-mid);">No workers added yet.</div>`;
      return;
    }

    appState.workers.forEach(worker => {
      const totalPaid = appState.workerPayments
        .filter(p => p.workerId == worker.id)
        .reduce((sum, p) => sum + Number(p.amount), 0);

      const history = appState.workerPayments
        .filter(p => p.workerId == worker.id)
        .map(p => `<div style="font-size:11px; color:var(--steel-mid); display:flex; justify-content:space-between; padding:3px 0;"><span>${p.date} (${p.type})</span><span style="color:#fff; font-weight:600;">₦${Number(p.amount).toLocaleString()}</span></div>`)
        .join('');

      container.innerHTML += `
        <div class="card">
          <div class="card-header">
            <div>
              <div style="font-weight:700; font-size:15px; color:#fff;">${worker.name}</div>
              <div style="font-size:11px; color:var(--orange-primary);">${worker.role || 'Assistant Cutter'} | ${worker.phone}</div>
            </div>
            <div style="text-align:right;">
              <div style="font-size:10px; color:var(--steel-mid);">TOTAL PAID</div>
              <div style="font-family:var(--font-heading); font-weight:700; color:var(--success);">₦${totalPaid.toLocaleString()}</div>
            </div>
          </div>
          <div style="background:var(--bg-surface); padding:10px; border-radius:10px; margin-top:8px;">
            <div style="font-size:11px; font-weight:700; color:var(--steel-mid); margin-bottom:4px; text-transform:uppercase;">Payment History</div>
            ${history || '<div style="font-size:11px; color:var(--steel-dark);">No payments recorded yet.</div>'}
          </div>
        </div>
      `;
    });
  }

  function renderReports() {
    const today = new Date().toISOString().split('T')[0];
    const todayInc = appState.incomes.filter(i => i.date === today).reduce((sum, i) => sum + Number(i.amount), 0);
    const todayExp = appState.expenses.filter(e => e.date === today).reduce((sum, e) => sum + Number(e.amount), 0);
    const todayWkr = appState.workerPayments.filter(w => w.date === today).reduce((sum, w) => sum + Number(w.amount), 0);
    const todayProfit = todayInc - (todayExp + todayWkr);

    const monthFilteredInc = filterByTimeframe(appState.incomes, 'monthly').reduce((sum, i) => sum + Number(i.amount), 0);
    const monthFilteredExp = filterByTimeframe(appState.expenses, 'monthly').reduce((sum, e) => sum + Number(e.amount), 0);
    const monthFilteredWkr = filterByTimeframe(appState.workerPayments, 'monthly').reduce((sum, w) => sum + Number(w.amount), 0);
    const monthProfit = monthFilteredInc - (monthFilteredExp + monthFilteredWkr);

    document.getElementById('rpt-today-profit').innerText = `₦${todayProfit.toLocaleString()}`;
    document.getElementById('rpt-month-profit').innerText = `₦${monthProfit.toLocaleString()}`;
  }

  function renderCustomers() {
    const container = document.getElementById('customers-list');
    container.innerHTML = '';
    const uniqueCustomers = {};

    appState.jobs.forEach(j => {
      if (!uniqueCustomers[j.customer]) {
        uniqueCustomers[j.customer] = { name: j.customer, phone: j.phone, count: 1, totalSpent: Number(j.charge) };
      } else {
        uniqueCustomers[j.customer].count += 1;
        uniqueCustomers[j.customer].totalSpent += Number(j.charge);
      }
    });

    Object.values(uniqueCustomers).forEach(c => {
      container.innerHTML += `
        <div class="list-item">
          <div>
            <div class="list-info-main">${c.name}</div>
            <div class="list-info-sub">${c.phone || 'No phone'} • ${c.count} Job(s)</div>
          </div>
          <div class="list-amount" style="color:var(--orange-primary);">₦${c.totalSpent.toLocaleString()}</div>
        </div>
      `;
    });
  }

  /* ================= Invoices & WhatsApp Integration ================= */
  function populateInvoiceDropdown() {
    const select = document.getElementById('invoice-job-select');
    select.innerHTML = '';
    appState.jobs.forEach(j => {
      select.innerHTML += `<option value="${j.id}">${j.customer} - ${j.desc} (₦${Number(j.charge).toLocaleString()})</option>`;
    });
    renderInvoicePreview();
  }

  function renderInvoicePreview() {
    const select = document.getElementById('invoice-job-select');
    const jobId = select.value;
    const container = document.getElementById('invoice-preview-area');
    const job = appState.jobs.find(j => j.id == jobId);

    if (!job) {
      container.innerHTML = `<div style="text-align:center; padding:20px; color:var(--steel-mid);">No job selected.</div>`;
      return;
    }

    const balance = Number(job.charge) - Number(job.paid);

    container.innerHTML = `
      <div class="invoice-container" id="printable-invoice">
        <div class="invoice-header">
          <div class="invoice-company">SAYYADI METAL CUTTING</div>
          <div style="font-size:10px; color:#555;">Kofar Ruwa, Layin Sarkin Kasuwa, Kano</div>
          <div style="font-size:10px; color:#555;">Tel: 07019163808 / 07060759052</div>
        </div>
        <div style="display:flex; justify-content:space-between; margin-bottom:10px; font-size:11px;">
          <div><strong>Customer:</strong> ${job.customer}</div>
          <div><strong>Date:</strong> ${job.date}</div>
        </div>
        <table class="invoice-table">
          <thead>
            <tr><th>Description</th><th style="text-align:right;">Amount</th></tr>
          </thead>
          <tbody>
            <tr>
              <td>${job.type} - ${job.desc}</td>
              <td style="text-align:right;">₦${Number(job.charge).toLocaleString()}</td>
            </tr>
            <tr class="invoice-total-row">
              <td>Total Amount</td>
              <td style="text-align:right;">₦${Number(job.charge).toLocaleString()}</td>
            </tr>
            <tr>
              <td>Amount Paid</td>
              <td style="text-align:right; color:green;">₦${Number(job.paid).toLocaleString()}</td>
            </tr>
            <tr style="font-weight:700;">
              <td>Balance Due</td>
              <td style="text-align:right; color:red;">₦${balance.toLocaleString()}</td>
            </tr>
          </tbody>
        </table>
        <div style="text-align:center; font-size:10px; color:#777; margin-top:15px;">
          Thank you for your business! / Mungode da Kasuwancinku!
        </div>
      </div>
    `;
  }

  function shareInvoiceWhatsApp() {
    const select = document.getElementById('invoice-job-select');
    const job = appState.jobs.find(j => j.id == select.value);
    if (!job) return;

    const balance = Number(job.charge) - Number(job.paid);
    const text = `*SAYYADI METAL CUTTING COMPANY*%0A` +
      `_Kofar Ruwa, Kano | Tel: 07019163808_%0A%0A` +
      `*OFFICIAL INVOICE / RECEIPT*%0A` +
      `----------------------------------%0A` +
      `*Customer:* ${job.customer}%0A` +
      `*Job:* ${job.type} (${job.desc})%0A` +
      `*Total Charge:* ₦${Number(job.charge).toLocaleString()}%0A` +
      `*Amount Paid:* ₦${Number(job.paid).toLocaleString()}%0A` +
      `*Balance Due:* ₦${balance.toLocaleString()}%0A` +
      `----------------------------------%0A` +
      `Thank you for your business!`;

    window.open(`https://wa.me/234${job.phone ? job.phone.replace(/^0/, '') : ''}?text=${text}`, '_blank');
  }

  /* ================= Save Form Records ================= */
  function saveIncome(e) {
    e.preventDefault();
    const newInc = {
      id: Date.now(),
      date: document.getElementById('inc-date').value,
      customer: document.getElementById('inc-customer').value,
      desc: document.getElementById('inc-desc').value,
      amount: Number(document.getElementById('inc-amount').value),
      method: document.getElementById('inc-method').value
    };
    appState.incomes.push(newInc);
    saveDataToStorage();
    closeModal('modal-income');
    e.target.reset();
    setTodayDates();
  }

  function saveExpense(e) {
    e.preventDefault();
    const newExp = {
      id: Date.now(),
      date: document.getElementById('exp-date').value,
      category: document.getElementById('exp-cat').value,
      amount: Number(document.getElementById('exp-amount').value),
      desc: document.getElementById('exp-desc').value
    };
    appState.expenses.push(newExp);
    saveDataToStorage();
    closeModal('modal-expense');
    e.target.reset();
    setTodayDates();
  }

  function saveWorker(e) {
    e.preventDefault();
    const newWorker = {
      id: Date.now(),
      name: document.getElementById('wrk-name').value,
      phone: document.getElementById('wrk-phone').value,
      role: document.getElementById('wrk-role').value
    };
    appState.workers.push(newWorker);
    saveDataToStorage();
    closeModal('modal-worker');
    e.target.reset();
  }

  function populateWorkerDropdown() {
    const select = document.getElementById('wpay-worker');
    select.innerHTML = '';
    appState.workers.forEach(w => {
      select.innerHTML += `<option value="${w.id}">${w.name} (${w.role})</option>`;
    });
  }

  function saveWorkerPayment(e) {
    e.preventDefault();
    const newPay = {
      id: Date.now(),
      workerId: document.getElementById('wpay-worker').value,
      date: document.getElementById('wpay-date').value,
      amount: Number(document.getElementById('wpay-amount').value),
      type: document.getElementById('wpay-type').value
    };
    appState.workerPayments.push(newPay);
    saveDataToStorage();
    closeModal('modal-worker-pay');
    e.target.reset();
    setTodayDates();
  }

  function saveJob(e) {
    e.preventDefault();
    const charge = Number(document.getElementById('job-charge').value);
    const paid = Number(document.getElementById('job-paid').value);
    const newJob = {
      id: Date.now(),
      customer: document.getElementById('job-customer').value,
      phone: document.getElementById('job-phone').value,
      type: document.getElementById('job-type').value,
      desc: document.getElementById('job-desc').value,
      charge: charge,
      paid: paid,
      status: paid >= charge ? 'Completed' : 'In Progress',
      date: new Date().toISOString().split('T')[0]
    };
    
    appState.jobs.push(newJob);

    // If money was paid upfront, automatically add income record
    if (paid > 0) {
      appState.incomes.push({
        id: Date.now() + 1,
        date: newJob.date,
        customer: newJob.customer,
        desc: `Deposit/Payment for ${newJob.type}`,
        amount: paid,
        method: 'Cash'
      });
    }

    saveDataToStorage();
    closeModal('modal-job');
    e.target.reset();
  }

  function saveSettings() {
    const pin = document.getElementById('setting-pin').value;
    if (pin && pin.length === 4) appState.settings.pin = pin;
    saveDataToStorage();
    alert('Settings Saved Successfully!');
  }

  /* ================= Data Management Functions ================= */
  function exportDataCSV() {
    let csv = 'Type,Date,Name/Category,Description,Amount\n';
    appState.incomes.forEach(i => {
      csv += `Income,${i.date},"${i.customer}","${i.desc}",${i.amount}\n`;
    });
    appState.expenses.forEach(e => {
      csv += `Expense,${e.date},"${e.category}","${e.desc}",${e.amount}\n`;
    });
    
    const blob = new Blob([csv], { type: 'text/csv' });
    const url = window.URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `SAYYADI_METAL_REPORT_${new Date().toISOString().split('T')[0]}.csv`;
    a.click();
  }

  function exportFullBackup() {
    const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(appState));
    const downloadAnchor = document.createElement('a');
    downloadAnchor.setAttribute("href", dataStr);
    downloadAnchor.setAttribute("download", `SAYYADI_BACKUP_${new Date().toISOString().split('T')[0]}.json`);
    document.body.appendChild(downloadAnchor);
    downloadAnchor.click();
    downloadAnchor.remove();
  }

  function resetAllData() {
    if (confirm("Are you sure you want to reset ALL records? This cannot be undone.")) {
      localStorage.removeItem('SAYYADI_METAL_DATA');
      location.reload();
    }
  }
</script>
</body>
</html>
