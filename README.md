# Household-Expense-Manager
Household Expense Manager
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Household Expense Manager</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --success: #4cc9f0;
            --warning: #f72585;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
            --light-gray: #e9ecef;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fb;
            color: var(--dark);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 15px;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 1rem;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .app-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 700;
            font-size: 1.5rem;
        }
        
        .device-info {
            display: flex;
            align-items: center;
            gap: 15px;
            font-size: 0.9rem;
        }
        
        .weather-info {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .main-content {
            display: flex;
            margin-top: 20px;
            gap: 20px;
        }
        
        .sidebar {
            flex: 0 0 250px;
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            height: calc(100vh - 100px);
            position: sticky;
            top: 90px;
            overflow-y: auto;
        }
        
        .content {
            flex: 1;
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            min-height: 600px;
        }
        
        .nav-item {
            padding: 12px 15px;
            border-radius: 8px;
            margin-bottom: 8px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .nav-item:hover {
            background-color: var(--light-gray);
        }
        
        .nav-item.active {
            background-color: var(--primary);
            color: white;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .welcome-header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .welcome-header h1 {
            color: var(--primary);
            margin-bottom: 10px;
        }
        
        .welcome-header p {
            color: var(--gray);
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .stat-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            text-align: center;
            border-left: 4px solid var(--primary);
        }
        
        .stat-card h3 {
            font-size: 1.2rem;
            margin-bottom: 10px;
            color: var(--gray);
        }
        
        .stat-card .value {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--dark);
        }
        
        .connected-devices {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            margin-bottom: 30px;
        }
        
        .devices-list {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            margin-top: 15px;
        }
        
        .device-card {
            background: var(--light);
            border-radius: 8px;
            padding: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
            min-width: 200px;
        }
        
        .device-icon {
            font-size: 1.5rem;
            color: var(--primary);
        }
        
        .table-container {
            overflow-x: auto;
            margin-bottom: 20px;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        
        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid var(--light-gray);
        }
        
        th {
            background-color: var(--light);
            font-weight: 600;
        }
        
        tr:hover {
            background-color: #f8f9fa;
        }
        
        .btn {
            padding: 8px 16px;
            border-radius: 6px;
            border: none;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
            margin: 2px;
        }
        
        .btn-primary {
            background-color: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background-color: var(--secondary);
        }
        
        .btn-danger {
            background-color: var(--warning);
            color: white;
        }
        
        .btn-success {
            background-color: #28a745;
            color: white;
        }
        
        .btn-success:hover {
            background-color: #218838;
        }
        
        .btn-warning {
            background-color: #ffc107;
            color: black;
        }
        
        .btn-warning:hover {
            background-color: #e0a800;
        }
        
        .btn-sm {
            padding: 5px 10px;
            font-size: 0.875rem;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
        }
        
        .form-control {
            width: 100%;
            padding: 10px 15px;
            border: 1px solid var(--light-gray);
            border-radius: 6px;
            font-size: 1rem;
        }
        
        .chart-container {
            position: relative;
            height: 400px;
            margin: 20px 0;
        }
        
        .summary-cards {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }
        
        .summary-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .summary-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .summary-card h3 {
            color: var(--gray);
            margin-bottom: 15px;
            font-size: 1.2rem;
        }
        
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0, 0, 0, 0.5);
        }
        
        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            width: 80%;
            max-width: 700px;
        }
        
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }
        
        .close:hover {
            color: black;
        }
        
        .transaction-form {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        .form-full-width {
            grid-column: 1 / span 2;
        }
        
        .detail-view {
            display: none;
        }
        
        .back-button {
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 5px;
            cursor: pointer;
            color: var(--primary);
            font-weight: 500;
        }
        
        .detail-summary {
            background-color: var(--light);
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
        }
        
        .summary-detail {
            display: none;
        }
        
        .wheel-container {
            text-align: center;
            margin: 20px 0;
        }
        
        .wheel {
            width: 300px;
            height: 300px;
            position: relative;
            margin: 0 auto;
        }
        
        .wheel-circle {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            background: conic-gradient(
                from 0deg,
                #ff6b6b, #ff9e6b, #ffcf6b, #e8ff6b,
                #6bff6b, #6bffcf, #6be8ff, #6b9eff,
                #6b6bff, #9e6bff, #cf6bff, #ff6be8
            );
            position: relative;
            overflow: hidden;
            transition: transform 5s cubic-bezier(0.17, 0.67, 0.83, 0.67);
        }
        
        .wheel-pointer {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 20px;
            height: 40px;
            background-color: var(--primary);
            clip-path: polygon(50% 100%, 0 0, 100% 0);
            z-index: 10;
        }
        
        .wheel-item {
            position: absolute;
            top: 0;
            left: 50%;
            width: 50%;
            height: 50%;
            transform-origin: bottom left;
            text-align: center;
            display: flex;
            align-items: center;
            justify-content: center;
            padding-top: 20px;
            font-weight: bold;
            color: white;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
        }
        
        .spin-button {
            margin-top: 20px;
            padding: 15px 30px;
            font-size: 1.2rem;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .spin-button:hover {
            background-color: var(--secondary);
            transform: scale(1.05);
        }
        
        .winner-display {
            margin-top: 20px;
            padding: 20px;
            background-color: var(--light);
            border-radius: 10px;
            text-align: center;
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary);
        }
        
        @media (max-width: 992px) {
            .main-content {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                height: auto;
                position: relative;
                top: 0;
                margin-bottom: 20px;
            }
            
            .transaction-form {
                grid-template-columns: 1fr;
            }
            
            .form-full-width {
                grid-column: 1;
            }
            
            .wheel {
                width: 250px;
                height: 250px;
            }
        }
        
        @media (max-width: 576px) {
            .app-header {
                flex-direction: column;
                gap: 10px;
            }
            
            .stats-grid {
                grid-template-columns: 1fr;
            }
            
            .device-info {
                flex-wrap: wrap;
                justify-content: center;
            }
            
            .modal-content {
                width: 95%;
                margin: 10% auto;
            }
            
            .wheel {
                width: 200px;
                height: 200px;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div class="app-header">
                <div class="logo">
                    <i class="fas fa-money-bill-wave"></i>
                    <span>Household Expense Manager</span>
                </div>
                <div class="device-info">
                    <div class="weather-info">
                        <i class="fas fa-cloud-sun"></i>
                        <span id="weather">28°C, Sunny</span>
                    </div>
                    <div class="location">
                        <i class="fas fa-location-dot"></i>
                        <span id="location">Hyderabad, IN</span>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <div class="container">
        <div class="main-content">
            <div class="sidebar">
                <div class="nav-item active" data-tab="welcome">
                    <i class="fas fa-home"></i>
                    <span>Welcome</span>
                </div>
                <div class="nav-item" data-tab="business">
                    <i class="fas fa-business-time"></i>
                    <span>Business</span>
                </div>
                <div class="nav-item" data-tab="chits">
                    <i class="fas fa-hand-holding-usd"></i>
                    <span>Chits</span>
                </div>
                <div class="nav-item" data-tab="expenses">
                    <i class="fas fa-receipt"></i>
                    <span>Household Expenses</span>
                </div>
                <div class="nav-item" data-tab="loans">
                    <i class="fas fa-money-bill-transfer"></i>
                    <span>Loans</span>
                </div>
                <div class="nav-item" data-tab="summary">
                    <i class="fas fa-chart-pie"></i>
                    <span>Summary Report</span>
                </div>
                <div class="nav-item" data-tab="settings">
                    <i class="fas fa-gear"></i>
                    <span>Settings</span>
                </div>
            </div>

            <div class="content">
                <!-- Welcome Tab -->
                <div class="tab-content active" id="welcome">
                    <div class="welcome-header">
                        <h1>Welcome to Household Expense Manager</h1>
                        <p>Manage your household expenses, business, chits, and loans in one place</p>
                    </div>
                    
                    <div class="stats-grid">
                        <div class="stat-card">
                            <h3>Total Balance</h3>
                            <div class="value">₹85,420</div>
                        </div>
                        <div class="stat-card">
                            <h3>Business Revenue</h3>
                            <div class="value">₹52,300</div>
                        </div>
                        <div class="stat-card">
                            <h3>Household Expenses</h3>
                            <div class="value">₹18,560</div>
                        </div>
                        <div class="stat-card">
                            <h3>Active Loans</h3>
                            <div class="value">₹12,500</div>
                        </div>
                    </div>
                    
                    <div class="connected-devices">
                        <h2>Connected Devices</h2>
                        <div class="devices-list">
                            <div class="device-card">
                                <div class="device-icon">
                                    <i class="fas fa-mobile-alt"></i>
                                </div>
                                <div class="device-info">
                                    <div>Dad's Phone</div>
                                    <div class="status">Online</div>
                                </div>
                            </div>
                            <div class="device-card">
                                <div class="device-icon">
                                    <i class="fas fa-mobile-alt"></i>
                                </div>
                                <div class="device-info">
                                    <div>Mom's Phone</div>
                                    <div class="status">Online</div>
                                </div>
                            </div>
                            <div class="device-card">
                                <div class="device-icon">
                                    <i class="fas fa-mobile-alt"></i>
                                </div>
                                <div class="device-info">
                                    <div>Brother's Phone</div>
                                    <div class="status">Online</div>
                                </div>
                            </div>
                            <div class="device-card">
                                <div class="device-icon">
                                    <i class="fas fa-tablet-alt"></i>
                                </div>
                                <div class="device-info">
                                    <div>Family Tablet</div>
                                    <div class="status">Online</div>
                                </div>
                            </div>
                            <div class="device-card">
                                <div class="device-icon">
                                    <i class="fas fa-laptop"></i>
                                </div>
                                <div class="device-info">
                                    <div>Home Laptop</div>
                                    <div class="status">Online</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Business Tab -->
                <div class="tab-content" id="business">
                    <div class="list-view">
                        <h2>Business Management</h2>
                        <p>Track your business transactions, customers, and balances</p>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Customer Name</th>
                                        <th>Total Given</th>
                                        <th>Total Received</th>
                                        <th>Balance</th>
                                        <th>Status</th>
                                        <th>Actions</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Rajesh Kumar</td>
                                        <td>₹15,000</td>
                                        <td>₹12,500</td>
                                        <td>₹2,500</td>
                                        <td>Active</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-customer" data-id="1">View</button>
                                            <button class="btn btn-success btn-sm add-transaction" data-type="business" data-id="1">Add Transaction</button>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>Suresh Babu</td>
                                        <td>₹8,000</td>
                                        <td>₹8,000</td>
                                        <td>₹0</td>
                                        <td>Paid Off</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-customer" data-id="2">View</button>
                                            <button class="btn btn-success btn-sm add-transaction" data-type="business" data-id="2">Add Transaction</button>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>Anil Reddy</td>
                                        <td>₹20,000</td>
                                        <td>₹15,000</td>
                                        <td>₹5,000</td>
                                        <td>Active</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-customer" data-id="3">View</button>
                                            <button class="btn btn-success btn-sm add-transaction" data-type="business" data-id="3">Add Transaction</button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        
                        <button class="btn btn-primary" id="addCustomerBtn">Add New Customer</button>
                    </div>
                    
                    <div class="detail-view" id="business-detail">
                        <div class="back-button" onclick="showBusinessListView()">
                            <i class="fas fa-arrow-left"></i> Back to Business List
                        </div>
                        
                        <h2>Customer Transaction Details</h2>
                        <p>Detailed transaction history for <span id="customer-name">Rajesh Kumar</span></p>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Date</th>
                                        <th>Transaction Type</th>
                                        <th>Amount</th>
                                        <th>Description</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>12/10/2023</td>
                                        <td>Given</td>
                                        <td>₹5,000</td>
                                        <td>Initial payment</td>
                                    </tr>
                                    <tr>
                                        <td>05/10/2023</td>
                                        <td>Given</td>
                                        <td>₹10,000</td>
                                        <td>Second payment</td>
                                    </tr>
                                    <tr>
                                        <td>01/10/2023</td>
                                        <td>Received</td>
                                        <td>₹7,500</td>
                                        <td>Partial repayment</td>
                                    </tr>
                                    <tr>
                                        <td>25/09/2023</td>
                                        <td>Received</td>
                                        <td>₹5,000</td>
                                        <td>Repayment</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        
                        <div class="detail-summary">
                            <h3>Transaction Summary</h3>
                            <p>Total Given: ₹15,000</p>
                            <p>Total Received: ₹12,500</p>
                            <p>Balance: ₹2,500</p>
                        </div>
                    </div>
                </div>

                <!-- Chits Tab -->
                <div class="tab-content" id="chits">
                    <div class="list-view">
                        <h2>Chits Management</h2>
                        <p>Manage your chit funds and track contributions</p>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Chit Name</th>
                                        <th>Total Value</th>
                                        <th>Members</th>
                                        <th>Amount Collected</th>
                                        <th>Amount Given</th>
                                        <th>Savings</th>
                                        <th>Status</th>
                                        <th>Actions</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Family Chit 2023</td>
                                        <td>₹1,00,000</td>
                                        <td>10/20</td>
                                        <td>₹75,000</td>
                                        <td>₹60,000</td>
                                        <td>₹15,000</td>
                                        <td>Active</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-chit" data-id="1">View</button>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>Friends Chit 2023</td>
                                        <td>₹50,000</td>
                                        <td>15/15</td>
                                        <td>₹50,000</td>
                                        <td>₹50,000</td>
                                        <td>₹0</td>
                                        <td>Completed</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-chit" data-id="2">View</button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        
                        <button class="btn btn-primary" id="addChitBtn">Add New Chit</button>
                    </div>
                    
                    <div class="detail-view" id="chit-detail">
                        <div class="back-button" onclick="showChitListView()">
                            <i class="fas fa-arrow-left"></i> Back to Chits List
                        </div>
                        
                        <h2>Chit Details: <span id="chit-name">Family Chit 2023</span></h2>
                        <p>Chit value: ₹1,00,000 | Status: Active | Members: <span id="chit-members-count">10</span>/<span id="chit-total-members">20</span></p>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Member Name</th>
                                        <th>Total Received</th>
                                        <th>Total Given</th>
                                        <th>Last Transaction</th>
                                        <th>Lottery Status</th>
                                        <th>Actions</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Rajesh Kumar</td>
                                        <td>₹15,000</td>
                                        <td>₹12,500</td>
                                        <td>12/10/2023</td>
                                        <td>Not Won</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-member" data-id="1">View</button>
                                            <button class="btn btn-warning btn-sm edit-member" data-id="1">Edit</button>
                                            <button class="btn btn-success btn-sm add-transaction" data-type="chit-member" data-id="1">Add Transaction</button>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>Suresh Babu</td>
                                        <td>₹8,000</td>
                                        <td>₹8,000</td>
                                        <td>05/10/2023</td>
                                        <td>Won</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-member" data-id="2">View</button>
                                            <button class="btn btn-warning btn-sm edit-member" data-id="2">Edit</button>
                                            <button class="btn btn-success btn-sm add-transaction" data-type="chit-member" data-id="2">Add Transaction</button>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>Anil Reddy</td>
                                        <td>₹20,000</td>
                                        <td>₹15,000</td>
                                        <td>01/10/2023</td>
                                        <td>Not Won</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-member" data-id="3">View</button>
                                            <button class="btn btn-warning btn-sm edit-member" data-id="3">Edit</button>
                                            <button class="btn btn-success btn-sm add-transaction" data-type="chit-member" data-id="3">Add Transaction</button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        
                        <div class="wheel-container">
                            <h3>Chit Lottery</h3>
                            <p>Spin the wheel to randomly select a winner from members who haven't won yet</p>
                            
                            <div class="wheel">
                                <div class="wheel-pointer"></div>
                                <div class="wheel-circle" id="wheel-circle">
                                    <!-- Wheel items will be added dynamically -->
                                </div>
                            </div>
                            
                            <button class="spin-button" id="spin-button">Spin the Wheel</button>
                            
                            <div class="winner-display" id="winner-display" style="display: none;">
                                <p>Congratulations to the winner:</p>
                                <h3 id="winner-name"></h3>
                            </div>
                        </div>
                        
                        <button class="btn btn-success" id="addMemberBtn">Add New Member</button>
                    </div>
                </div>

                <!-- Expenses Tab -->
                <div class="tab-content" id="expenses">
                    <h2>Household Expenses</h2>
                    <p>Track your household income and expenses</p>
                    
                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>Date</th>
                                    <th>Description</th>
                                    <th>Category</th>
                                    <th>Amount</th>
                                    <th>Type</th>
                                    <th>Actions</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>12/10/2023</td>
                                    <td>Groceries</td>
                                    <td>Food</td>
                                    <td>₹2,500</td>
                                    <td>Expense</td>
                                    <td>
                                        <button class="btn btn-warning btn-sm edit-expense" data-id="1">Edit</button>
                                        <button class="btn btn-danger btn-sm remove-expense" data-id="1">Remove</button>
                                    </td>
                                </tr>
                                <tr>
                                    <td>10/10/2023</td>
                                    <td>Freelance Work</td>
                                    <td>Income</td>
                                    <td>₹8,000</td>
                                    <td>Income</td>
                                    <td>
                                        <button class="btn btn-warning btn-sm edit-expense" data-id="2">Edit</button>
                                        <button class="btn btn-danger btn-sm remove-expense" data-id="2">Remove</button>
                                    </td>
                                </tr>
                                <tr>
                                    <td>08/10/2023</td>
                                    <td>Electricity Bill</td>
                                    <td>Utilities</td>
                                    <td>₹1,200</td>
                                    <td>Expense</td>
                                    <td>
                                        <button class="btn btn-warning btn-sm edit-expense" data-id="3">Edit</button>
                                        <button class="btn btn-danger btn-sm remove-expense" data-id="3">Remove</button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    
                    <button class="btn btn-primary" id="addExpenseBtn">Add New Transaction</button>
                </div>

                <!-- Loans Tab -->
                <div class="tab-content" id="loans">
                    <div class="list-view">
                        <h2>Loans Management</h2>
                        <p>Track loans taken and given</p>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Loan Name</th>
                                        <th>Principal</th>
                                        <th>Paid</th>
                                        <th>Balance</th>
                                        <th>Type</th>
                                        <th>Status</th>
                                        <th>Actions</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Business Expansion</td>
                                        <td>₹50,000</td>
                                        <td>₹20,000</td>
                                        <td>₹30,000</td>
                                        <td>Taken</td>
                                        <td>Active</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-loan" data-id="1">View</button>
                                            <button class="btn btn-success btn-sm add-transaction" data-type="loan" data-id="1">Add Payment</button>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td>Car Loan to Ramesh</td>
                                        <td>₹25,000</td>
                                        <td>₹10,000</td>
                                        <td>₹15,000</td>
                                        <td>Given</td>
                                        <td>Active</td>
                                        <td>
                                            <button class="btn btn-primary btn-sm view-loan" data-id="2">View</button>
                                            <button class="btn btn-success btn-sm add-transaction" data-type="loan" data-id="2">Add Payment</button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        
                        <button class="btn btn-primary" id="addLoanBtn">Add New Loan</button>
                    </div>
                    
                    <div class="detail-view" id="loan-detail">
                        <div class="back-button" onclick="showLoanListView()">
                            <i class="fas fa-arrow-left"></i> Back to Loans List
                        </div>
                        
                        <h2>Loan Details: <span id="loan-name">Business Expansion</span></h2>
                        <p>Principal: ₹50,000 | Type: Taken | Status: Active</p>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Date</th>
                                        <th>Transaction Type</th>
                                        <th>Amount</th>
                                        <th>Description</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>15/09/2023</td>
                                        <td>Disbursement</td>
                                        <td>₹50,000</td>
                                        <td>Initial loan amount</td>
                                    </tr>
                                    <tr>
                                        <td>05/10/2023</td>
                                        <td>Payment</td>
                                        <td>₹10,000</td>
                                        <td>First installment</td>
                                    </tr>
                                    <tr>
                                        <td>12/10/2023</td>
                                        <td>Payment</td>
                                        <td>₹10,000</td>
                                        <td>Second installment</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        
                        <div class="detail-summary">
                            <h3>Loan Summary</h3>
                            <p>Principal Amount: ₹50,000</p>
                            <p>Total Paid: ₹20,000</p>
                            <p>Balance: ₹30,000</p>
                            <p>Next Due Date: 05/11/2023</p>
                        </div>
                    </div>
                </div>

                <!-- Summary Tab -->
                <div class="tab-content" id="summary">
                    <div class="list-view">
                        <h2>Summary Report</h2>
                        <p>Overall financial summary with charts and graphs</p>
                        
                        <div class="chart-container">
                            <canvas id="financialChart"></canvas>
                        </div>
                        
                        <div class="summary-cards">
                            <div class="summary-card" data-summary="business">
                                <h3>Business Summary</h3>
                                <p>Total Given: ₹43,000</p>
                                <p>Total Received: ₹35,500</p>
                                <p>Balance: ₹7,500</p>
                            </div>
                            <div class="summary-card" data-summary="chits">
                                <h3>Chits Summary</h3>
                                <p>Total Value: ₹1,50,000</p>
                                <p>Amount Collected: ₹1,25,000</p>
                                <p>Amount Given: ₹1,10,000</p>
                                <p>Savings: ₹15,000</p>
                            </div>
                            <div class="summary-card" data-summary="household">
                                <h3>Household Summary</h3>
                                <p>Total Income: ₹25,000</p>
                                <p>Total Expenses: ₹18,560</p>
                                <p>Net: ₹6,440</p>
                            </div>
                            <div class="summary-card" data-summary="loans">
                                <h3>Loans Summary</h3>
                                <p>Total Taken: ₹50,000</p>
                                <p>Total Given: ₹25,000</p>
                                <p>Balance to Pay: ₹30,000</p>
                                <p>Balance to Receive: ₹15,000</p>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Summary Detail Views -->
                    <div class="summary-detail" id="business-summary">
                        <div class="back-button" onclick="showSummaryListView()">
                            <i class="fas fa-arrow-left"></i> Back to Summary
                        </div>
                        
                        <h2>Business Detailed Summary</h2>
                        
                        <div class="chart-container">
                            <canvas id="businessChart"></canvas>
                        </div>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Customer Name</th>
                                        <th>Total Given</th>
                                        <th>Total Received</th>
                                        <th>Balance</th>
                                        <th>Status</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Rajesh Kumar</td>
                                        <td>₹15,000</td>
                                        <td>₹12,500</td>
                                        <td>₹2,500</td>
                                        <td>Active</td>
                                    </tr>
                                    <tr>
                                        <td>Suresh Babu</td>
                                        <td>₹8,000</td>
                                        <td>₹8,000</td>
                                        <td>₹0</td>
                                        <td>Paid Off</td>
                                    </tr>
                                    <tr>
                                        <td>Anil Reddy</td>
                                        <td>₹20,000</td>
                                        <td>₹15,000</td>
                                        <td>₹5,000</td>
                                        <td>Active</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    
                    <div class="summary-detail" id="chits-summary">
                        <div class="back-button" onclick="showSummaryListView()">
                            <i class="fas fa-arrow-left"></i> Back to Summary
                        </div>
                        
                        <h2>Chits Detailed Summary</h2>
                        
                        <div class="chart-container">
                            <canvas id="chitsChart"></canvas>
                        </div>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Chit Name</th>
                                        <th>Total Value</th>
                                        <th>Amount Collected</th>
                                        <th>Amount Given</th>
                                        <th>Savings</th>
                                        <th>Status</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Family Chit 2023</td>
                                        <td>₹1,00,000</td>
                                        <td>₹75,000</td>
                                        <td>₹60,000</td>
                                        <td>₹15,000</td>
                                        <td>Active</td>
                                    </tr>
                                    <tr>
                                        <td>Friends Chit 2023</td>
                                        <td>₹50,000</td>
                                        <td>₹50,000</td>
                                        <td>₹50,000</td>
                                        <td>₹0</td>
                                        <td>Completed</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    
                    <div class="summary-detail" id="household-summary">
                        <div class="back-button" onclick="showSummaryListView()">
                            <i class="fas fa-arrow-left"></i> Back to Summary
                        </div>
                        
                        <h2>Household Detailed Summary</h2>
                        
                        <div class="chart-container">
                            <canvas id="householdChart"></canvas>
                        </div>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Category</th>
                                        <th>Amount</th>
                                        <th>Type</th>
                                        <th>Trend</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Food</td>
                                        <td>₹8,500</td>
                                        <td>Expense</td>
                                        <td>+12%</td>
                                    </tr>
                                    <tr>
                                        <td>Utilities</td>
                                        <td>₹5,200</td>
                                        <td>Expense</td>
                                        <td>-5%</td>
                                    </tr>
                                    <tr>
                                        <td>Income</td>
                                        <td>₹25,000</td>
                                        <td>Income</td>
                                        <td>+8%</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    
                    <div class="summary-detail" id="loans-summary">
                        <div class="back-button" onclick="showSummaryListView()">
                            <i class="fas fa-arrow-left"></i> Back to Summary
                        </div>
                        
                        <h2>Loans Detailed Summary</h2>
                        
                        <div class="chart-container">
                            <canvas id="loansChart"></canvas>
                        </div>
                        
                        <div class="table-container">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Loan Name</th>
                                        <th>Principal</th>
                                        <th>Paid</th>
                                        <th>Balance</th>
                                        <th>Type</th>
                                        <th>Status</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>Business Expansion</td>
                                        <td>₹50,000</td>
                                        <td>₹20,000</td>
                                        <td>₹30,000</td>
                                        <td>Taken</td>
                                        <td>Active</td>
                                    </tr>
                                    <tr>
                                        <td>Car Loan to Ramesh</td>
                                        <td>₹25,000</td>
                                        <td>₹10,000</td>
                                        <td>₹15,000</td>
                                        <td>Given</td>
                                        <td>Active</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- Settings Tab -->
                <div class="tab-content" id="settings">
                    <h2>Settings</h2>
                    <p>Configure your application and Google Sheets integration</p>
                    
                    <div class="form-group">
                        <label for="sheetUrl">Google Sheet URL</label>
                        <input type="text" id="sheetUrl" class="form-control" placeholder="https://docs.google.com/spreadsheets/d/...">
                    </div>
                    
                    <div class="form-group">
                        <label for="apiKey">Google Sheets API Key</label>
                        <input type="password" id="apiKey" class="form-control" placeholder="Enter your API key">
                    </div>
                    
                    <div class="form-group">
                        <label for="syncFrequency">Sync Frequency</label>
                        <select id="syncFrequency" class="form-control">
                            <option value="5">Every 5 minutes</option>
                            <option value="15">Every 15 minutes</option>
                            <option value="30">Every 30 minutes</option>
                            <option value="60">Every hour</option>
                        </select>
                    </div>
                    
                    <button class="btn btn-primary">Save Settings</button>
                    
                    <div class="detail-summary" style="margin-top: 30px;">
                        <h3>Google Sheets Setup Instructions</h3>
                        <p>1. Create a new Google Sheet with the following tabs:</p>
                        <ul>
                            <li>Business_Customers</li>
                            <li>Business_Transactions</li>
                            <li>Chits</li>
                            <li>Chit_Members</li>
                            <li>Chit_Transactions</li>
                            <li>Household_Expenses</li>
                            <li>Loans</li>
                            <li>Loan_Transactions</li>
                        </ul>
                        <p>2. Enable Google Sheets API in Google Cloud Console</p>
                        <p>3. Create API credentials and add the key above</p>
                        <p>4. Share your Google Sheet with the service account email</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Customer Modal -->
    <div id="customerModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 id="modal-title">Add New Customer</h2>
            
            <div class="transaction-form">
                <div class="form-group">
                    <label for="customer-name">Customer Name</label>
                    <input type="text" id="customer-name" class="form-control" placeholder="Enter customer name">
                </div>
                
                <div class="form-group">
                    <label for="customer-phone">Phone Number</label>
                    <input type="text" id="customer-phone" class="form-control" placeholder="Enter phone number">
                </div>
                
                <div class="form-group form-full-width">
                    <label for="customer-address">Address</label>
                    <textarea id="customer-address" class="form-control" placeholder="Enter address" rows="3"></textarea>
                </div>
                
                <div class="form-group form-full-width">
                    <button class="btn btn-primary" style="width: 100%;" onclick="saveCustomer()">Save Customer</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Chit Modal -->
    <div id="chitModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 id="modal-title">Add New Chit</h2>
            
            <div class="transaction-form">
                <div class="form-group">
                    <label for="chit-name">Chit Name</label>
                    <input type="text" id="chit-name" class="form-control" placeholder="Enter chit name">
                </div>
                
                <div class="form-group">
                    <label for="chit-value">Chit Value (₹)</label>
                    <input type="number" id="chit-value" class="form-control" placeholder="Enter chit value">
                </div>
                
                <div class="form-group">
                    <label for="chit-members">Number of Members</label>
                    <input type="number" id="chit-members" class="form-control" placeholder="Enter number of members">
                </div>
                
                <div class="form-group">
                    <label for="chit-duration">Duration (months)</label>
                    <input type="number" id="chit-duration" class="form-control" placeholder="Enter duration">
                </div>
                
                <div class="form-group form-full-width">
                    <button class="btn btn-primary" style="width: 100%;" onclick="saveChit()">Save Chit</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Transaction Modal -->
    <div id="transactionModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 id="modal-title">Add Transaction</h2>
            
            <div class="transaction-form">
                <div class="form-group">
                    <label for="trans-date">Date</label>
                    <input type="date" id="trans-date" class="form-control" value="2023-10-15">
                </div>
                
                <div class="form-group">
                    <label for="trans-amount">Amount (₹)</label>
                    <input type="number" id="trans-amount" class="form-control" placeholder="Enter amount">
                </div>
                
                <div class="form-group form-full-width">
                    <label for="trans-description">Description</label>
                    <input type="text" id="trans-description" class="form-control" placeholder="Enter description">
                </div>
                
                <div class="form-group" id="trans-type-container">
                    <label for="trans-type">Transaction Type</label>
                    <select id="trans-type" class="form-control">
                        <option value="given">Amount Given</option>
                        <option value="received">Amount Received</option>
                    </select>
                </div>
                
                <div class="form-group" id="loan-trans-type-container" style="display: none;">
                    <label for="loan-trans-type">Transaction Type</label>
                    <select id="loan-trans-type" class="form-control">
                        <option value="payment">Payment</option>
                        <option value="disbursement">Disbursement</option>
                    </select>
                </div>
                
                <div class="form-group form-full-width">
                    <button class="btn btn-primary" style="width: 100%;" onclick="saveTransaction()">Save Transaction</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Expense Modal -->
    <div id="expenseModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 id="expense-modal-title">Add Expense</h2>
            
            <div class="transaction-form">
                <div class="form-group">
                    <label for="expense-date">Date</label>
                    <input type="date" id="expense-date" class="form-control" value="2023-10-15">
                </div>
                
                <div class="form-group">
                    <label for="expense-amount">Amount (₹)</label>
                    <input type="number" id="expense-amount" class="form-control" placeholder="Enter amount">
                </div>
                
                <div class="form-group">
                    <label for="expense-category">Category</label>
                    <select id="expense-category" class="form-control">
                        <option value="food">Food</option>
                        <option value="utilities">Utilities</option>
                        <option value="transport">Transport</option>
                        <option value="entertainment">Entertainment</option>
                        <option value="other">Other</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="expense-type">Type</label>
                    <select id="expense-type" class="form-control">
                        <option value="expense">Expense</option>
                        <option value="income">Income</option>
                    </select>
                </div>
                
                <div class="form-group form-full-width">
                    <label for="expense-description">Description</label>
                    <input type="text" id="expense-description" class="form-control" placeholder="Enter description">
                </div>
                
                <div class="form-group form-full-width">
                    <button class="btn btn-primary" style="width: 100%;" onclick="saveExpense()">Save Transaction</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Loan Modal -->
    <div id="loanModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 id="modal-title">Add New Loan</h2>
            
            <div class="transaction-form">
                <div class="form-group">
                    <label for="loan-name">Loan Name</label>
                    <input type="text" id="loan-name" class="form-control" placeholder="Enter loan name">
                </div>
                
                <div class="form-group">
                    <label for="loan-amount">Loan Amount (₹)</label>
                    <input type="number" id="loan-amount" class="form-control" placeholder="Enter loan amount">
                </div>
                
                <div class="form-group">
                    <label for="loan-type">Loan Type</label>
                    <select id="loan-type" class="form-control">
                        <option value="taken">Taken</option>
                        <option value="given">Given</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="loan-interest">Interest Rate (%)</label>
                    <input type="number" id="loan-interest" class="form-control" placeholder="Enter interest rate">
                </div>
                
                <div class="form-group">
                    <label for="loan-duration">Duration (months)</label>
                    <input type="number" id="loan-duration" class="form-control" placeholder="Enter duration">
                </div>
                
                <div class="form-group form-full-width">
                    <button class="btn btn-primary" style="width: 100%;" onclick="saveLoan()">Save Loan</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Member Modal -->
    <div id="memberModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2 id="modal-title">Add New Member</h2>
            
            <div class="transaction-form">
                <div class="form-group">
                    <label for="member-name">Member Name</label>
                    <input type="text" id="member-name" class="form-control" placeholder="Enter member name">
                </div>
                
                <div class="form-group">
                    <label for="member-phone">Phone Number</label>
                    <input type="text" id="member-phone" class="form-control" placeholder="Enter phone number">
                </div>
                
                <div class="form-group form-full-width">
                    <label for="member-address">Address</label>
                    <textarea id="member-address" class="form-control" placeholder="Enter address" rows="3"></textarea>
                </div>
                
                <div class="form-group form-full-width">
                    <button class="btn btn-primary" style="width: 100%;" onclick="saveMember()">Save Member</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Tab navigation
        document.querySelectorAll('.nav-item').forEach(item => {
            item.addEventListener('click', function() {
                // Remove active class from all items
                document.querySelectorAll('.nav-item').forEach(i => {
                    i.classList.remove('active');
                });
                
                // Add active class to clicked item
                this.classList.add('active');
                
                // Hide all tab content
                document.querySelectorAll('.tab-content').forEach(tab => {
                    tab.classList.remove('active');
                });
                
                // Show selected tab content
                const tabId = this.getAttribute('data-tab');
                document.getElementById(tabId).classList.add('active');
            });
        });
        
        // Initialize chart
        document.addEventListener('DOMContentLoaded', function() {
            const ctx = document.getElementById('financialChart').getContext('2d');
            const financialChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Business', 'Chits', 'Household', 'Loans'],
                    datasets: [{
                        label: 'Amount in ₹',
                        data: [43500, 125000, 18560, 75000],
                        backgroundColor: [
                            'rgba(67, 97, 238, 0.7)',
                            'rgba(76, 201, 240, 0.7)',
                            'rgba(247, 37, 133, 0.7)',
                            'rgba(58, 12, 163, 0.7)'
                        ],
                        borderColor: [
                            'rgb(67, 97, 238)',
                            'rgb(76, 201, 240)',
                            'rgb(247, 37, 133)',
                            'rgb(58, 12, 163)'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true
                        }
                    }
                }
            });
            
            // Initialize detail charts
            initDetailCharts();
            
            // Simulate weather and location data
            simulateWeatherData();
            simulateLocationData();
            
            // Set up modal functionality
            setupModals();
            
            // Set up view buttons
            setupViewButtons();
            
            // Set up summary cards
            setupSummaryCards();
            
            // Set up lottery wheel
            setupLotteryWheel();
        });
        
        // Initialize detail charts
        function initDetailCharts() {
            // Business chart
            const businessCtx = document.getElementById('businessChart').getContext('2d');
            new Chart(businessCtx, {
                type: 'pie',
                data: {
                    labels: ['Given', 'Received', 'Balance'],
                    datasets: [{
                        data: [43000, 35500, 7500],
                        backgroundColor: [
                            'rgba(67, 97, 238, 0.7)',
                            'rgba(76, 201, 240, 0.7)',
                            'rgba(247, 37, 133, 0.7)'
                        ]
                    }]
                }
            });
            
            // Chits chart
            const chitsCtx = document.getElementById('chitsChart').getContext('2d');
            new Chart(chitsCtx, {
                type: 'pie',
                data: {
                    labels: ['Collected', 'Given', 'Savings'],
                    datasets: [{
                        data: [125000, 110000, 15000],
                        backgroundColor: [
                            'rgba(67, 97, 238, 0.7)',
                            'rgba(76, 201, 240, 0.7)',
                            'rgba(247, 37, 133, 0.7)'
                        ]
                    }]
                }
            });
            
            // Household chart
            const householdCtx = document.getElementById('householdChart').getContext('2d');
            new Chart(householdCtx, {
                type: 'doughnut',
                data: {
                    labels: ['Income', 'Expenses'],
                    datasets: [{
                        data: [25000, 18560],
                        backgroundColor: [
                            'rgba(67, 97, 238, 0.7)',
                            'rgba(247, 37, 133, 0.7)'
                        ]
                    }]
                }
            });
            
            // Loans chart
            const loansCtx = document.getElementById('loansChart').getContext('2d');
            new Chart(loansCtx, {
                type: 'pie',
                data: {
                    labels: ['Taken', 'Given', 'Balance to Pay', 'Balance to Receive'],
                    datasets: [{
                        data: [50000, 25000, 30000, 15000],
                        backgroundColor: [
                            'rgba(67, 97, 238, 0.7)',
                            'rgba(76, 201, 240, 0.7)',
                            'rgba(247, 37, 133, 0.7)',
                            'rgba(58, 12, 163, 0.7)'
                        ]
                    }]
                }
            });
        }
        
        // Simulate weather data
        function simulateWeatherData() {
            const weatherElement = document.getElementById('weather');
            const temperatures = ['28°C, Sunny', '26°C, Partly Cloudy', '30°C, Clear', '25°C, Light Rain'];
            const randomWeather = temperatures[Math.floor(Math.random() * temperatures.length)];
            weatherElement.textContent = randomWeather;
        }
        
        // Simulate location data
        function simulateLocationData() {
            const locations = ['Hyderabad, IN', 'Mumbai, IN', 'Delhi, IN', 'Chennai, IN', 'Bangalore, IN'];
            const randomLocation = locations[Math.floor(Math.random() * locations.length)];
            document.getElementById('location').textContent = randomLocation;
        }
        
        // Set up modal functionality
        function setupModals() {
            const modals = document.querySelectorAll('.modal');
            const closeButtons = document.querySelectorAll('.close');
            
            // Close modals when clicking on X
            closeButtons.forEach(button => {
                button.onclick = function() {
                    modals.forEach(modal => {
                        modal.style.display = "none";
                    });
                }
            });
            
            // Close modals when clicking outside
            window.onclick = function(event) {
                modals.forEach(modal => {
                    if (event.target == modal) {
                        modal.style.display = "none";
                    }
                });
            }
            
            // Add customer button
            document.getElementById('addCustomerBtn').addEventListener('click', function() {
                document.getElementById('customerModal').style.display = "block";
            });
            
            // Add chit button
            document.getElementById('addChitBtn').addEventListener('click', function() {
                document.getElementById('chitModal').style.display = "block";
            });
            
            // Add expense button
            document.getElementById('addExpenseBtn').addEventListener('click', function() {
                document.getElementById('expenseModal').style.display = "block";
            });
            
            // Add loan button
            document.getElementById('addLoanBtn').addEventListener('click', function() {
                document.getElementById('loanModal').style.display = "block";
            });
            
            // Add member button
            document.getElementById('addMemberBtn').addEventListener('click', function() {
                document.getElementById('memberModal').style.display = "block";
            });
            
            // Add transaction buttons
            document.querySelectorAll('.add-transaction').forEach(button => {
                button.addEventListener('click', function() {
                    const type = this.getAttribute('data-type');
                    const id = this.getAttribute('data-id');
                    showTransactionModal(type, id);
                });
            });
            
            // Edit expense buttons
            document.querySelectorAll('.edit-expense').forEach(button => {
                button.addEventListener('click', function() {
                    const expenseId = this.getAttribute('data-id');
                    editExpense(expenseId);
                });
            });
            
            // Remove expense buttons
            document.querySelectorAll('.remove-expense').forEach(button => {
                button.addEventListener('click', function() {
                    const expenseId = this.getAttribute('data-id');
                    removeExpense(expenseId);
                });
            });
            
            // Edit member buttons
            document.querySelectorAll('.edit-member').forEach(button => {
                button.addEventListener('click', function() {
                    const memberId = this.getAttribute('data-id');
                    editMember(memberId);
                });
            });
        }
        
        // Set up view buttons
        function setupViewButtons() {
            // Business view buttons
            document.querySelectorAll('.view-customer').forEach(button => {
                button.addEventListener('click', function() {
                    const customerId = this.getAttribute('data-id');
                    showBusinessDetailView(customerId);
                });
            });
            
            // Chit view buttons
            document.querySelectorAll('.view-chit').forEach(button => {
                button.addEventListener('click', function() {
                    const chitId = this.getAttribute('data-id');
                    showChitDetailView(chitId);
                });
            });
            
            // Loan view buttons
            document.querySelectorAll('.view-loan').forEach(button => {
                button.addEventListener('click', function() {
                    const loanId = this.getAttribute('data-id');
                    showLoanDetailView(loanId);
                });
            });
        }
        
        // Set up summary cards
        function setupSummaryCards() {
            document.querySelectorAll('.summary-card').forEach(card => {
                card.addEventListener('click', function() {
                    const summaryType = this.getAttribute('data-summary');
                    showSummaryDetail(summaryType);
                });
            });
        }
        
        // Set up lottery wheel
        function setupLotteryWheel() {
            const spinButton = document.getElementById('spin-button');
            if (spinButton) {
                spinButton.addEventListener('click', spinWheel);
            }
        }
        
        // Spin the lottery wheel
        function spinWheel() {
            const wheel = document.getElementById('wheel-circle');
            const winnerDisplay = document.getElementById('winner-display');
            const winnerName = document.getElementById('winner-name');
            
            // Get members who haven't won yet (from your data)
            const eligibleMembers = [
                { name: 'Rajesh Kumar', won: false },
                { name: 'Anil Reddy', won: false },
                { name: 'Priya Sharma', won: false },
                { name: 'Vikram Singh', won: false }
            ];
            
            // Generate wheel items
            const wheelElement = document.getElementById('wheel-circle');
            wheelElement.innerHTML = '';
            
            const anglePerItem = 360 / eligibleMembers.length;
            
            eligibleMembers.forEach((member, index) => {
                const item = document.createElement('div');
                item.className = 'wheel-item';
                item.textContent = member.name;
                item.style.transform = `rotate(${index * anglePerItem}deg)`;
                wheelElement.appendChild(item);
            });
            
            // Spin the wheel
            const spinDegrees = 1800 + Math.floor(Math.random() * 360); // Multiple full rotations plus random
            wheel.style.transform = `rotate(${spinDegrees}deg)`;
            
            // Determine winner after spin
            setTimeout(() => {
                const winnerIndex = Math.floor((spinDegrees % 360) / anglePerItem);
                const winner = eligibleMembers[winnerIndex];
                
                // Display winner
                winnerName.textContent = winner.name;
                winnerDisplay.style.display = 'block';
                
                // In a real app, you would update the member's status in Google Sheets
                alert(`Congratulations! The winner is ${winner.name}. This would be saved to Google Sheets.`);
            }, 5000);
        }
        
        // Show transaction modal
        function showTransactionModal(type, id) {
            const modal = document.getElementById("transactionModal");
            const title = document.getElementById("modal-title");
            const transTypeContainer = document.getElementById("trans-type-container");
            const loanTransTypeContainer = document.getElementById("loan-trans-type-container");
            
            if (type === 'business') {
                title.textContent = "Add Business Transaction";
                transTypeContainer.style.display = "block";
                loanTransTypeContainer.style.display = "none";
            } else if (type === 'chit' || type === 'chit-member') {
                title.textContent = "Add Chit Transaction";
                transTypeContainer.style.display = "block";
                loanTransTypeContainer.style.display = "none";
            } else if (type === 'loan') {
                title.textContent = "Add Loan Transaction";
                transTypeContainer.style.display = "none";
                loanTransTypeContainer.style.display = "block";
            }
            
            modal.style.display = "block";
        }
        
        // Save customer
        function saveCustomer() {
            alert("Customer saved successfully! In a real application, this would save to Google Sheets.");
            document.getElementById("customerModal").style.display = "none";
        }
        
        // Save chit
        function saveChit() {
            alert("Chit saved successfully! In a real application, this would save to Google Sheets.");
            document.getElementById("chitModal").style.display = "none";
        }
        
        // Save transaction
        function saveTransaction() {
            alert("Transaction saved successfully! In a real application, this would save to Google Sheets.");
            document.getElementById("transactionModal").style.display = "none";
        }
        
        // Save expense
        function saveExpense() {
            alert("Expense saved successfully! In a real application, this would save to Google Sheets.");
            document.getElementById("expenseModal").style.display = "none";
        }
        
        // Save loan
        function saveLoan() {
            alert("Loan saved successfully! In a real application, this would save to Google Sheets.");
            document.getElementById("loanModal").style.display = "none";
        }
        
        // Save member
        function saveMember() {
            alert("Member saved successfully! In a real application, this would save to Google Sheets.");
            document.getElementById("memberModal").style.display = "none";
        }
        
        // Edit expense
        function editExpense(id) {
            alert(`Editing expense with ID: ${id}. In a real application, this would open an edit form.`);
        }
        
        // Remove expense
        function removeExpense(id) {
            if (confirm("Are you sure you want to remove this expense?")) {
                alert(`Expense with ID: ${id} removed. In a real application, this would remove from Google Sheets.`);
            }
        }
        
        // Edit member
        function editMember(id) {
            alert(`Editing member with ID: ${id}. In a real application, this would open an edit form.`);
        }
        
        // Show business detail view
        function showBusinessDetailView(customerId) {
            document.querySelector('#business .list-view').style.display = 'none';
            document.getElementById('business-detail').style.display = 'block';
            
            // In a real app, you would fetch customer data based on ID
            const customerName = document.querySelector(`.view-customer[data-id="${customerId}"]`).closest('tr').querySelector('td:first-child').textContent;
            document.getElementById('customer-name').textContent = customerName;
        }
        
        // Show business list view
        function showBusinessListView() {
            document.querySelector('#business .list-view').style.display = 'block';
            document.getElementById('business-detail').style.display = 'none';
        }
        
        // Show chit detail view
        function showChitDetailView(chitId) {
            document.querySelector('#chits .list-view').style.display = 'none';
            document.getElementById('chit-detail').style.display = 'block';
            
            // In a real app, you would fetch chit data based on ID
            const chitName = document.querySelector(`.view-chit[data-id="${chitId}"]`).closest('tr').querySelector('td:first-child').textContent;
            document.getElementById('chit-name').textContent = chitName;
        }
        
        // Show chit list view
        function showChitListView() {
            document.querySelector('#chits .list-view').style.display = 'block';
            document.getElementById('chit-detail').style.display = 'none';
        }
        
        // Show loan detail view
        function showLoanDetailView(loanId) {
            document.querySelector('#loans .list-view').style.display = 'none';
            document.getElementById('loan-detail').style.display = 'block';
            
            // In a real app, you would fetch loan data based on ID
            const loanName = document.querySelector(`.view-loan[data-id="${loanId}"]`).closest('tr').querySelector('td:first-child').textContent;
            document.getElementById('loan-name').textContent = loanName;
        }
        
        // Show loan list view
        function showLoanListView() {
            document.querySelector('#loans .list-view').style.display = 'block';
            document.getElementById('loan-detail').style.display = 'none';
        }
        
        // Show summary detail view
        function showSummaryDetail(type) {
            document.querySelector('#summary .list-view').style.display = 'none';
            document.getElementById(`${type}-summary`).style.display = 'block';
        }
        
        // Show summary list view
        function showSummaryListView() {
            document.querySelector('#summary .list-view').style.display = 'block';
            document.querySelectorAll('.summary-detail').forEach(detail => {
                detail.style.display = 'none';
            });
        }
        
        // Google Sheets integration functions
        function connectToGoogleSheets() {
            const sheetUrl = document.getElementById('sheetUrl').value;
            const apiKey = document.getElementById('apiKey').value;
            
            if (!sheetUrl || !apiKey) {
                alert("Please enter both Google Sheet URL and API Key");
                return;
            }
            
            console.log("Connecting to Google Sheets...");
            // Implementation would go here
        }
        
        function readDataFromSheet(sheetName) {
            console.log(`Reading data from ${sheetName} sheet...`);
            // Implementation would go here
            return [];
        }
        
        function writeDataToSheet(sheetName, data) {
            console.log(`Writing data to ${sheetName} sheet...`);
            // Implementation would go here
        }
        
        // Example Google Sheets structure
        /*
        Business Sheet:
        - Business_Customers: ID, Name, Phone, Address, TotalGiven, TotalReceived, Balance, Status
        - Business_Transactions: ID, CustomerID, Date, Type, Amount, Description
        
        Chits Sheet:
        - Chits: ID, Name, TotalValue, TotalMembers, AmountCollected, AmountGiven, Savings, Status
        - Chit_Members: ID, ChitID, Name, Phone, Address, TotalReceived, TotalGiven, LastTransaction, LotteryStatus
        - Chit_Transactions: ID, ChitID, MemberID, Date, Amount, Type, Description
        
        Household Sheet:
        - Household_Expenses: ID, Date, Description, Category, Amount, Type
        
        Loans Sheet:
        - Loans: ID, Name, Principal, Paid, Balance, Type, Status, InterestRate, Duration
        - Loan_Transactions: ID, LoanID, Date, Type, Amount, Description
        */
    </script>
</body>
</html>
