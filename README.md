# Tae-1.2
T&amp;E platform made to compete with both SAP Concur and RAMP. Main objective is to show how powerful LLM coding software is. 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tae v1.2 - Travel & Expense Management with ERP Integration</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .main-container {
            width: 100%;
            max-width: 1600px;
            display: flex;
            gap: 20px;
            height: 90vh;
        }

        .tae-container {
            flex: 1;
            background: white;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            display: flex;
            flex-direction: column;
        }

        .erp-panel {
            width: 400px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow-y: auto;
        }

        .erp-header {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
        }

        .erp-header h2 {
            font-size: 1.5em;
            margin-bottom: 10px;
        }

        .erp-status {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }

        .status-badge {
            display: flex;
            align-items: center;
            gap: 5px;
            padding: 5px 10px;
            background: rgba(255,255,255,0.2);
            border-radius: 20px;
            font-size: 0.85em;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #10b981;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .erp-selector {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
        }

        .erp-btn {
            width: 100%;
            padding: 12px;
            margin-bottom: 8px;
            border: 2px solid #e5e7eb;
            background: white;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 500;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .erp-btn:hover {
            border-color: #667eea;
            transform: translateX(3px);
        }

        .erp-btn.active {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border-color: transparent;
        }

        .sync-queue {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
        }

        .sync-item {
            background: white;
            border: 1px solid #e5e7eb;
            border-radius: 8px;
            padding: 10px;
            margin-bottom: 8px;
            font-size: 0.9em;
        }

        .sync-item.pending {
            border-left: 3px solid #f59e0b;
        }

        .sync-item.success {
            border-left: 3px solid #10b981;
        }

        .sync-item.error {
            border-left: 3px solid #ef4444;
        }

        .field-mapping {
            background: #fff8dc;
            border: 1px solid #fbbf24;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
        }

        .mapping-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #fef3c7;
            font-size: 0.85em;
        }

        .mapping-row:last-child {
            border-bottom: none;
        }

        .arrow {
            color: #f59e0b;
        }

        .api-log {
            background: #1f2937;
            color: #e5e7eb;
            border-radius: 10px;
            padding: 15px;
            font-family: 'Courier New', monospace;
            font-size: 0.8em;
            max-height: 200px;
            overflow-y: auto;
        }

        .log-entry {
            padding: 3px 0;
            border-left: 2px solid #667eea;
            padding-left: 10px;
            margin-bottom: 5px;
        }

        .log-entry.success {
            border-left-color: #10b981;
        }

        .log-entry.error {
            border-left-color: #ef4444;
        }

        .iframe-container {
            flex: 1;
            position: relative;
            background: #f3f4f6;
            display: flex;
            flex-direction: column;
        }

        .tae-header {
            background: white;
            padding: 15px 20px;
            border-bottom: 1px solid #e5e7eb;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .tae-header h1 {
            font-size: 1.5em;
            color: #333;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .integration-indicator {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 8px 15px;
            background: linear-gradient(135deg, #10b981, #059669);
            color: white;
            border-radius: 20px;
            font-size: 0.9em;
            font-weight: 500;
        }

        .tae-iframe {
            flex: 1;
            width: 100%;
            border: none;
            background: white;
        }

        .sync-button {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 500;
            width: 100%;
            margin-top: 10px;
            transition: all 0.3s ease;
        }

        .sync-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.3);
        }

        .metric-cards {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }

        .metric-card {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }

        .metric-value {
            font-size: 1.5em;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .metric-label {
            font-size: 0.8em;
            opacity: 0.9;
        }

        @media (max-width: 1200px) {
            .main-container {
                flex-direction: column;
                height: auto;
            }

            .erp-panel {
                width: 100%;
                max-width: 600px;
                margin: 0 auto;
            }
        }
    </style>
</head>
<body>
    <div class="main-container">
        <!-- Tae Application Container -->
        <div class="tae-container">
            <div class="tae-header">
                <h1>
                    <span style="background: linear-gradient(135deg, #667eea, #764ba2); -webkit-background-clip: text; -webkit-text-fill-color: transparent;">Tae v1.2</span>
                    Travel & Expense Management
                </h1>
                <div class="integration-indicator">
                    <span style="width: 8px; height: 8px; background: white; border-radius: 50%; animation: pulse 2s infinite;"></span>
                    ERP Connected
                </div>
            </div>
            <div class="iframe-container">
                <div id="taeApp" style="width: 100%; height: 100%; background: white; overflow-y: auto;"></div>
            </div>
        </div>

        <!-- ERP Integration Panel -->
        <div class="erp-panel">
            <div class="erp-header">
                <h2>ERP Integration Hub</h2>
                <p style="font-size: 0.9em; opacity: 0.9;">Real-time sync with your accounting systems</p>
                <div class="erp-status">
                    <div class="status-badge">
                        <div class="status-dot"></div>
                        NetSuite
                    </div>
                    <div class="status-badge">
                        <div class="status-dot"></div>
                        Sage
                    </div>
                    <div class="status-badge">
                        <div class="status-dot"></div>
                        QuickBooks
                    </div>
                </div>
            </div>

            <div class="metric-cards">
                <div class="metric-card">
                    <div class="metric-value" id="syncedToday">47</div>
                    <div class="metric-label">Synced Today</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value" id="pendingSync">3</div>
                    <div class="metric-label">Pending Sync</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value" id="lastSync">2m</div>
                    <div class="metric-label">Last Sync</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value" id="successRate">99.8%</div>
                    <div class="metric-label">Success Rate</div>
                </div>
            </div>

            <div class="erp-selector">
                <h3 style="margin-bottom: 10px; font-size: 1.1em;">Active ERP System</h3>
                <button class="erp-btn active" onclick="selectERP('netsuite')">
                    <span>NetSuite</span>
                    <span style="font-size: 0.8em; opacity: 0.8;">Account: PROD-001</span>
                </button>
                <button class="erp-btn" onclick="selectERP('sage')">
                    <span>Sage Intacct</span>
                    <span style="font-size: 0.8em; opacity: 0.8;">Account: SAGE-MAIN</span>
                </button>
                <button class="erp-btn" onclick="selectERP('quickbooks')">
                    <span>QuickBooks Online</span>
                    <span style="font-size: 0.8em; opacity: 0.8;">Account: QBO-2024</span>
                </button>
            </div>

            <div class="sync-queue">
                <h3 style="margin-bottom: 10px; font-size: 1.1em;">Recent Sync Activity</h3>
                <div id="syncQueue">
                    <div class="sync-item success">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
                            <strong>Expense #1247</strong>
                            <span style="color: #10b981;">✓ Synced</span>
                        </div>
                        <div style="color: #666; font-size: 0.85em;">
                            Marriott Downtown - $127.50 → NetSuite
                        </div>
                    </div>
                    <div class="sync-item success">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
                            <strong>Expense #1246</strong>
                            <span style="color: #10b981;">✓ Synced</span>
                        </div>
                        <div style="color: #666; font-size: 0.85em;">
                            Uber - $45.23 → NetSuite
                        </div>
                    </div>
                    <div class="sync-item pending">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
                            <strong>Expense #1245</strong>
                            <span style="color: #f59e0b;">⟳ Processing</span>
                        </div>
                        <div style="color: #666; font-size: 0.85em;">
                            The Capital Grille - $89.99 → NetSuite
                        </div>
                    </div>
                </div>
            </div>

            <div class="field-mapping">
                <h3 style="margin-bottom: 10px; font-size: 1.1em;">Field Mapping</h3>
                <div class="mapping-row">
                    <span>Tae Amount</span>
                    <span class="arrow">→</span>
                    <span>NS: Amount</span>
                </div>
                <div class="mapping-row">
                    <span>Tae Merchant</span>
                    <span class="arrow">→</span>
                    <span>NS: Vendor</span>
                </div>
                <div class="mapping-row">
                    <span>Tae Category</span>
                    <span class="arrow">→</span>
                    <span>NS: Account</span>
                </div>
                <div class="mapping-row">
                    <span>OCR Receipt</span>
                    <span class="arrow">→</span>
                    <span>NS: Attachment</span>
                </div>
            </div>

            <button class="sync-button" onclick="syncAllExpenses()">
                🔄 Sync All Pending Expenses
            </button>

            <div style="margin-top: 20px;">
                <h3 style="margin-bottom: 10px; font-size: 1.1em;">API Activity Log</h3>
                <div class="api-log" id="apiLog">
                    <div class="log-entry success">✓ Connected to NetSuite API</div>
                    <div class="log-entry">→ Authenticated with OAuth 2.0</div>
                    <div class="log-entry success">✓ Fetched vendor list (247 records)</div>
                    <div class="log-entry">→ Creating expense record...</div>
                    <div class="log-entry success">✓ Expense #1247 synced to NetSuite</div>
                    <div class="log-entry">→ Uploading receipt to NetSuite Files...</div>
                    <div class="log-entry success">✓ Receipt attached to transaction</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Tae Application Code (Embedded)
        const TaeApp = `
            <div style="max-width: 100%; background: #f9fafb; min-height: 100vh; position: relative;">
                <!-- Navigation Bar -->
                <div style="position: fixed; bottom: 0; left: 0; right: 0; background: white; border-top: 1px solid #e5e7eb; padding: 8px; z-index: 100;">
                    <div style="display: flex; justify-content: space-around; align-items: center;">
                        <button onclick="showDashboard()" style="display: flex; flex-direction: column; align-items: center; padding: 4px; background: none; border: none; cursor: pointer; color: #667eea;">
                            <svg width="20" height="20" fill="currentColor" viewBox="0 0 20 20"><path d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z"></path></svg>
                            <span style="font-size: 12px; margin-top: 4px;">Home</span>
                        </button>
                        <button onclick="showExpenses()" style="display: flex; flex-direction: column; align-items: center; padding: 4px; background: none; border: none; cursor: pointer; color: #6b7280;">
                            <svg width="20" height="20" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M4 4a2 2 0 00-2 2v8a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2H4zm4 5a1 1 0 011-1h2a1 1 0 110 2H9a1 1 0 01-1-1zm5 0a1 1 0 011-1h1a1 1 0 110 2h-1a1 1 0 01-1-1z" clip-rule="evenodd"></path></svg>
                            <span style="font-size: 12px; margin-top: 4px;">Expenses</span>
                        </button>
                        <button onclick="showTravel()" style="display: flex; flex-direction: column; align-items: center; padding: 4px; background: none; border: none; cursor: pointer; color: #6b7280;">
                            <svg width="20" height="20" fill="currentColor" viewBox="0 0 20 20"><path d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.429A1 1 0 009 15.571V11a1 1 0 112 0v4.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z"></path></svg>
                            <span style="font-size: 12px; margin-top: 4px;">Travel</span>
                        </button>
                        <button onclick="showReports()" style="display: flex; flex-direction: column; align-items: center; padding: 4px; background: none; border: none; cursor: pointer; color: #6b7280;">
                            <svg width="20" height="20" fill="currentColor" viewBox="0 0 20 20"><path d="M2 11a1 1 0 011-1h2a1 1 0 011 1v5a1 1 0 01-1 1H3a1 1 0 01-1-1v-5zM8 7a1 1 0 011-1h2a1 1 0 011 1v9a1 1 0 01-1 1H9a1 1 0 01-1-1V7zM14 4a1 1 0 011-1h2a1 1 0 011 1v12a1 1 0 01-1 1h-2a1 1 0 01-1-1V4z"></path></svg>
                            <span style="font-size: 12px; margin-top: 4px;">Reports</span>
                        </button>
                        <button onclick="showProfile()" style="display: flex; flex-direction: column; align-items: center; padding: 4px; background: none; border: none; cursor: pointer; color: #6b7280;">
                            <svg width="20" height="20" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd"></path></svg>
                            <span style="font-size: 12px; margin-top: 4px;">Profile</span>
                        </button>
                    </div>
                </div>

                <!-- Main Content Area -->
                <div id="mainContent" style="padding-bottom: 80px;">
                    <!-- Dashboard -->
                    <div id="dashboardScreen">
                        <div style="background: white; border-bottom: 1px solid #e5e7eb; padding: 16px;">
                            <h1 style="font-size: 1.5em; font-weight: 600;">Dashboard</h1>
                        </div>
                        
                        <!-- Quick Stats -->
                        <div style="padding: 16px; display: grid; grid-template-columns: 1fr 1fr; gap: 16px;">
                            <div style="background: #eff6ff; border-radius: 12px; padding: 16px;">
                                <div style="font-size: 2em; font-weight: bold; color: #2563eb;">$891.48</div>
                                <div style="font-size: 0.9em; color: #64748b;">Total Expenses</div>
                            </div>
                            <div style="background: #fef3c7; border-radius: 12px; padding: 16px;">
                                <div style="font-size: 2em; font-weight: bold; color: #f59e0b;">3</div>
                                <div style="font-size: 0.9em; color: #64748b;">Pending Review</div>
                            </div>
                            <div style="background: #d1fae5; border-radius: 12px; padding: 16px;">
                                <div style="font-size: 2em; font-weight: bold; color: #10b981;">5</div>
                                <div style="font-size: 0.9em; color: #64748b;">Approved</div>
                            </div>
                            <div style="background: #e9d5ff; border-radius: 12px; padding: 16px;">
                                <div style="font-size: 2em; font-weight: bold; color: #a855f7;">8</div>
                                <div style="font-size: 0.9em; color: #64748b;">OCR Processed</div>
                            </div>
                        </div>

                        <!-- Quick Actions -->
                        <div style="padding: 16px;">
                            <h2 style="font-size: 1.2em; font-weight: 600; margin-bottom: 12px;">Quick Actions</h2>
                            <button onclick="newExpense()" style="width: 100%; background: linear-gradient(135deg, #667eea, #764ba2); color: white; border: none; border-radius: 12px; padding: 16px; font-size: 1em; font-weight: 500; cursor: pointer; margin-bottom: 12px; display: flex; align-items: center; justify-content: center;">
                                📸 New Expense with OCR
                            </button>
                            <button onclick="syncToERP()" style="width: 100%; background: #10b981; color: white; border: none; border-radius: 12px; padding: 16px; font-size: 1em; font-weight: 500; cursor: pointer; display: flex; align-items: center; justify-content: center;">
                                🔄 Sync to ERP
                            </button>
                        </div>

                        <!-- Recent Expenses -->
                        <div style="padding: 16px;">
                            <h2 style="font-size: 1.2em; font-weight: 600; margin-bottom: 12px;">Recent Expenses</h2>
                            <div style="background: white; border: 1px solid #e5e7eb; border-radius: 12px; padding: 16px; margin-bottom: 12px;">
                                <div style="display: flex; justify-content: space-between;">
                                    <div>
                                        <div style="font-weight: 500;">Marriott Downtown</div>
                                        <div style="font-size: 0.9em; color: #64748b;">Lodging • Dec 15, 2024</div>
                                    </div>
                                    <div style="text-align: right;">
                                        <div style="font-weight: 600;">$127.50</div>
                                        <div style="background: #d1fae5; color: #065f46; padding: 2px 8px; border-radius: 12px; font-size: 0.8em; margin-top: 4px;">Synced to NetSuite</div>
                                    </div>
                                </div>
                            </div>
                            <div style="background: white; border: 1px solid #e5e7eb; border-radius: 12px; padding: 16px; margin-bottom: 12px;">
                                <div style="display: flex; justify-content: space-between;">
                                    <div>
                                        <div style="font-weight: 500;">Uber</div>
                                        <div style="font-size: 0.9em; color: #64748b;">Transportation • Dec 14, 2024</div>
                                    </div>
                                    <div style="text-align: right;">
                                        <div style="font-weight: 600;">$45.23</div>
                                        <div style="background: #d1fae5; color: #065f46; padding: 2px 8px; border-radius: 12px; font-size: 0.8em; margin-top: 4px;">Synced to NetSuite</div>
                                    </div>
                                </div>
                            </div>
                            <div style="background: white; border: 1px solid #e5e7eb; border-radius: 12px; padding: 16px;">
                                <div style="display: flex; justify-content: space-between;">
                                    <div>
                                        <div style="font-weight: 500;">The Capital Grille</div>
                                        <div style="font-size: 0.9em; color: #64748b;">Meals • Dec 12, 2024</div>
                                    </div>
                                    <div style="text-align: right;">
                                        <div style="font-weight: 600;">$89.99</div>
                                        <div style="background: #fef3c7; color: #92400e; padding: 2px 8px; border-radius: 12px; font-size: 0.8em; margin-top: 4px;">Pending Sync</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        `;

        // Insert Tae App into container
        document.getElementById('taeApp').innerHTML = TaeApp;

        // Global variables
        let currentERP = 'netsuite';
        let syncQueue = [];
        let apiCallCount = 0;

        // ERP Integration Functions
        function selectERP(erp) {
            currentERP = erp;
            document.querySelectorAll('.erp-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.closest('.erp-btn').classList.add('active');
            
            addLog(`Switched to ${erp.toUpperCase()} integration`);
            updateMetrics();
        }

        function syncAllExpenses() {
            addLog('Starting batch sync to ' + currentERP.toUpperCase() + '...');
            
            // Simulate sync process
            setTimeout(() => {
                addLog('✓ Connected to ' + currentERP + ' API', 'success');
                setTimeout(() => {
                    addLog('→ Fetching pending expenses...');
                    setTimeout(() => {
                        addLog('✓ Synced 3 expenses successfully', 'success');
                        updateSyncQueue();
                        updateMetrics();
                    }, 1000);
                }, 500);
            }, 500);
        }

        function updateSyncQueue() {
            const queueHTML = `
                <div class="sync-item success">
                    <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
                        <strong>Expense #1248</strong>
                        <span style="color: #10b981;">✓ Synced</span>
                    </div>
                    <div style="color: #666; font-size: 0.85em;">
                        The Capital Grille - $89.99 → ${currentERP}
                    </div>
                </div>
            ` + document.getElementById('syncQueue').innerHTML;
            
            document.getElementById('syncQueue').innerHTML = queueHTML;
            
            // Update pending count
            const pending = parseInt(document.getElementById('pendingSync').textContent);
            document.getElementById('pendingSync').textContent = Math.max(0, pending - 1);
            
            // Update synced count
            const synced = parseInt(document.getElementById('syncedToday').textContent);
            document.getElementById('syncedToday').textContent = synced + 1;
        }

        function addLog(message, type = '') {
            const logContainer = document.getElementById('apiLog');
            const entry = document.createElement('div');
            entry.className = `log-entry ${type}`;
            entry.textContent = type === 'success' ? `✓ ${message}` : `→ ${message}`;
            
            // Remove oldest log if too many
            if (logContainer.children.length > 7) {
                logContainer.removeChild(logContainer.lastChild);
            }
            
            logContainer.insertBefore(entry, logContainer.firstChild);
        }

        function updateMetrics() {
            apiCallCount++;
            
            // Simulate real-time updates
            if (apiCallCount % 5 === 0) {
                const synced = parseInt(document.getElementById('syncedToday').textContent);
                document.getElementById('syncedToday').textContent = synced + 1;
            }
            
            document.getElementById('lastSync').textContent = 'Just now';
            setTimeout(() => {
                document.getElementById('lastSync').textContent = '1m';
            }, 60000);
        }

        // Tae App Functions
        function showDashboard() {
            console.log('Showing dashboard');
        }

        function showExpenses() {
            console.log('Showing expenses');
        }

        function showTravel() {
            console.log('Showing travel');
        }

        function showReports() {
            console.log('Showing reports');
        }

        function showProfile() {
            console.log('Showing profile');
        }

        function newExpense() {
            addLog('New expense created in Tae');
            const pending = parseInt(document.getElementById('pendingSync').textContent);
            document.getElementById('pendingSync').textContent = pending + 1;
        }

        function syncToERP() {
            syncAllExpenses();
        }

        // Simulate real-time activity
        setInterval(() => {
            const random = Math.random();
            if (random < 0.3) {
                const messages = [
                    'Checking for new expenses...',
                    'Validating field mappings...',
                    'Maintaining API connection...',
                    'Refreshing authentication token...'
                ];
                addLog(messages[Math.floor(Math.random() * messages.length)]);
            }
        }, 15000);

        // Initialize
        addLog('System initialized', 'success');
        addLog('Connected to ' + currentERP.toUpperCase() + ' API', 'success');
    </script>
</body>
</html>
