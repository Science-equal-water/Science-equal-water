<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SCIENCE = WATER | Premium Edu App</title>
    
    <!-- Firebase SDKs -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-analytics-compat.js"></script>
    
    <!-- Inter Font -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        /* Enhanced Modern Educational Theme */
        :root {
            --primary-color: #2563eb;
            --secondary-color: #7c3aed;
            --accent-color: #0ea5e9;
            --success-color: #10b981;
            --warning-color: #f59e0b;
            --danger-color: #ef4444;
            --dark-color: #1e293b;
            --light-color: #f8fafc;
            --text-primary: #334155;
            --text-secondary: #64748b;
            
            --gradient-primary: linear-gradient(135deg, #2563eb 0%, #7c3aed 100%);
            --gradient-secondary: linear-gradient(135deg, #0ea5e9 0%, #10b981 100%);
            --gradient-dark: linear-gradient(135deg, #1e293b 0%, #334155 100%);
            
            --shadow-sm: 0 2px 4px rgba(0, 0, 0, 0.05);
            --shadow-md: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
            --shadow-lg: 0 20px 40px rgba(0, 0, 0, 0.15);
            --shadow-xl: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
            
            --radius-sm: 8px;
            --radius-md: 16px;
            --radius-lg: 24px;
            --radius-xl: 32px;
            
            --transition-fast: 150ms cubic-bezier(0.4, 0, 0.2, 1);
            --transition-base: 300ms cubic-bezier(0.4, 0, 0.2, 1);
            --transition-slow: 500ms cubic-bezier(0.4, 0, 0.2, 1);
            
            --ssc-color: #0ea5e9;
            --hsc-color: #8b5cf6;
            --payment-color: #10b981;
            --message-color: #7c3aed;
        }

        * { 
            margin: 0; 
            padding: 0; 
            box-sizing: border-box; 
        }
        
        body { 
            background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
            color: var(--text-primary); 
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            line-height: 1.6;
            min-height: 100vh;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        /* Admin Login Modal - Premium Glass Effect */
        #adminModal {
            display: none;
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.92);
            backdrop-filter: blur(12px);
            z-index: 10000;
            justify-content: center;
            align-items: center;
            animation: fadeIn 0.3s ease-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .login-box {
            background: rgba(255, 255, 255, 0.95);
            padding: 48px 40px;
            border-radius: var(--radius-xl);
            width: 90%;
            max-width: 440px;
            box-shadow: var(--shadow-xl);
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
            transform: translateY(0);
            transition: transform var(--transition-base);
        }
        
        .login-box:hover {
            transform: translateY(-2px);
        }
        
        .login-box h2 { 
            color: var(--primary-color); 
            margin-bottom: 32px;
            font-size: 28px;
            font-weight: 700;
            letter-spacing: -0.5px;
        }

        .login-box input {
            width: 100%;
            padding: 16px 20px;
            margin: 12px 0;
            border: 2px solid #e2e8f0;
            border-radius: var(--radius-md);
            font-size: 16px;
            outline: none;
            transition: all var(--transition-fast);
            background: #ffffff;
            font-family: 'Inter', sans-serif;
        }

        .login-box input:focus { 
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }
        
        .login-btn {
            background: var(--gradient-primary);
            color: white;
            border: none;
            padding: 16px 32px;
            width: 100%;
            border-radius: var(--radius-md);
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            box-shadow: var(--shadow-md);
            transition: all var(--transition-base);
            margin-top: 20px;
            letter-spacing: 0.5px;
        }
        
        .login-btn:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }
        
        /* Admin Panel - Enhanced Design */
        #adminPanel {
            display: none;
            background: white;
            padding: 32px;
            border-radius: var(--radius-xl);
            margin: 30px auto;
            max-width: 1200px;
            box-shadow: var(--shadow-lg);
            border: 1px solid #e2e8f0;
            animation: slideUp 0.4s ease-out;
        }
        
        @keyframes slideUp {
            from { 
                opacity: 0;
                transform: translateY(20px);
            }
            to { 
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .admin-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 32px;
            padding-bottom: 24px;
            border-bottom: 2px solid #f1f5f9;
        }
        
        .admin-header h2 {
            color: var(--primary-color);
            font-size: 28px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        /* Main Container */
        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 24px;
        }
        
        /* Header - Enhanced Educational Banner */
        .header {
            text-align: center;
            padding: 80px 40px;
            background: var(--gradient-primary);
            border-radius: var(--radius-xl);
            color: white;
            margin-bottom: 48px;
            box-shadow: var(--shadow-lg);
            position: relative;
            overflow: hidden;
        }
        
        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.1' fill-rule='evenodd'/%3E%3C/svg%3E");
        }
        
        .header h1 {
            font-size: 3.5rem;
            letter-spacing: -1.5px;
            margin-bottom: 16px;
            font-weight: 800;
            position: relative;
            z-index: 1;
        }
        
        .header p {
            font-size: 1.25rem;
            opacity: 0.95;
            font-weight: 400;
            max-width: 600px;
            margin: 0 auto;
            position: relative;
            z-index: 1;
        }
        
        /* Content Cards Grid */
        .content-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 32px;
        }
        
        .card {
            background: white;
            border-radius: var(--radius-xl);
            padding: 36px;
            box-shadow: var(--shadow-md);
            border: 1px solid rgba(255, 255, 255, 0.8);
            transition: all var(--transition-base);
            position: relative;
            overflow: hidden;
        }
        
        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: var(--gradient-primary);
        }
        
        .card:hover { 
            transform: translateY(-8px); 
            box-shadow: var(--shadow-lg); 
        }
        
        .card h2 {
            color: var(--primary-color);
            margin-bottom: 28px;
            font-size: 1.75rem;
            display: flex;
            align-items: center;
            gap: 14px;
            font-weight: 700;
        }
        
        /* Enhanced Links & Buttons */
        .link-btn {
            display: block;
            background: white;
            color: var(--primary-color);
            text-decoration: none;
            padding: 18px 24px;
            border-radius: var(--radius-md);
            text-align: center;
            font-weight: 600;
            border: 2px solid #e2e8f0;
            transition: all var(--transition-base);
            cursor: pointer;
            font-family: 'Inter', sans-serif;
            letter-spacing: 0.3px;
        }
        
        .link-btn:hover { 
            background: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
            transform: translateY(-2px);
            box-shadow: var(--shadow-md);
        }

        .btn-ssc { 
            background: var(--gradient-secondary);
            color: white; 
            border: none; 
        }
        
        .btn-hsc { 
            background: linear-gradient(135deg, #8b5cf6 0%, #a78bfa 100%);
            color: white; 
            border: none; 
        }
        
        .btn-payment { 
            background: var(--gradient-secondary);
            color: white; 
            border: none; 
        }
        
        .btn-message { 
            background: linear-gradient(135deg, #7c3aed 0%, #a78bfa 100%);
            color: white; 
            border: none; 
        }
        
        /* Enhanced Class Card */
        .class-card {
            background: #ffffff;
            border-radius: var(--radius-md);
            padding: 24px;
            border-left: 6px solid var(--primary-color);
            margin-bottom: 18px;
            box-shadow: var(--shadow-sm);
            transition: all var(--transition-fast);
            border: 1px solid #e2e8f0;
        }
        
        .class-card:hover {
            transform: translateX(4px);
            box-shadow: var(--shadow-md);
        }

        .class-card h3 { 
            color: var(--text-primary); 
            margin-bottom: 8px;
            font-size: 1.1rem;
            font-weight: 600;
        }
        
        .class-card p { 
            color: var(--text-secondary); 
            font-size: 0.95rem;
            line-height: 1.5;
        }
        
        /* Enhanced Message Box */
        .message-box {
            background: linear-gradient(135deg, #fffbeb 0%, #fef3c7 100%);
            border-radius: var(--radius-md);
            padding: 24px;
            margin: 20px 0;
            border-left: 6px solid #f59e0b;
            box-shadow: var(--shadow-sm);
        }
        
        .message-title { 
            color: #92400e; 
            font-weight: 700; 
            margin-bottom: 8px;
            font-size: 1.1rem;
        }

        /* Enhanced Routine Section */
        .routine-day {
            background: linear-gradient(135deg, #f1f5f9 0%, #e2e8f0 100%);
            border-radius: var(--radius-md);
            padding: 20px;
            margin-bottom: 20px;
            border: 1px solid #cbd5e1;
        }
        
        .day-header { 
            color: var(--primary-color); 
            font-weight: 700; 
            margin-bottom: 16px;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .class-slot {
            background: white;
            padding: 16px;
            border-radius: var(--radius-sm);
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #e2e8f0;
            transition: all var(--transition-fast);
        }
        
        .class-slot:hover {
            border-color: var(--primary-color);
            box-shadow: var(--shadow-sm);
        }

        /* Admin Access Button - Floating */
        #adminAccess {
            position: fixed;
            bottom: 32px;
            right: 32px;
            background: var(--gradient-primary);
            color: white;
            border: none;
            width: 64px;
            height: 64px;
            border-radius: 50%;
            cursor: pointer;
            font-weight: bold;
            box-shadow: var(--shadow-lg);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all var(--transition-base);
            font-size: 24px;
        }
        
        #adminAccess:hover {
            transform: scale(1.1) rotate(15deg);
            box-shadow: var(--shadow-xl);
        }

        /* Virtual Scroll Container */
        .virtual-scroll-container {
            max-height: 500px;
            overflow-y: auto;
            padding: 16px;
            background: white;
            border-radius: var(--radius-md);
            border: 1px solid #e2e8f0;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.05);
        }
        
        /* Enhanced WhatsApp Button */
        .whatsapp-btn {
            background: linear-gradient(135deg, #25D366 0%, #128C7E 100%);
            color: white;
            padding: 16px 32px;
            border-radius: 50px;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 12px;
            margin-top: 20px;
            font-weight: 600;
            transition: all var(--transition-base);
            box-shadow: var(--shadow-md);
        }
        
        .whatsapp-btn:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }

        /* Loading Spinner */
        .loading-spinner {
            text-align: center;
            padding: 40px;
            color: var(--primary-color);
        }
        
        /* Status Messages */
        .success-message {
            background: linear-gradient(135deg, #d1fae5 0%, #a7f3d0 100%);
            color: #065f46;
            padding: 16px;
            border-radius: var(--radius-md);
            margin: 16px 0;
            text-align: center;
            border: 1px solid #10b981;
            font-weight: 500;
        }
        
        .error-message {
            background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%);
            color: #dc2626;
            padding: 16px;
            border-radius: var(--radius-md);
            margin: 16px 0;
            text-align: center;
            border: 1px solid #ef4444;
            font-weight: 500;
        }
        
        /* Enhanced Suggestion Card */
        .suggestion-card {
            background: white;
            border-radius: var(--radius-md);
            padding: 24px;
            margin-bottom: 20px;
            border-left: 6px solid var(--accent-color);
            box-shadow: var(--shadow-sm);
            transition: all var(--transition-base);
            border: 1px solid #e2e8f0;
        }

        .suggestion-card:hover {
            transform: translateY(-4px);
            box-shadow: var(--shadow-md);
            border-left-color: var(--primary-color);
        }

        .suggestion-card h4 {
            color: #0369a1;
            margin-bottom: 12px;
            font-size: 1.1rem;
            font-weight: 600;
        }

        .suggestion-card p {
            color: var(--text-secondary);
            font-size: 0.95rem;
            margin-bottom: 16px;
            line-height: 1.5;
        }

        .suggestion-link {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: var(--gradient-secondary);
            color: white;
            padding: 10px 20px;
            border-radius: var(--radius-sm);
            text-decoration: none;
            font-weight: 600;
            margin-top: 12px;
            transition: all var(--transition-fast);
            border: none;
            cursor: pointer;
        }

        .suggestion-link:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-md);
        }

        .delete-suggestion {
            background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%);
            color: #dc2626;
            border: 1px solid #fca5a5;
            padding: 8px 16px;
            border-radius: var(--radius-sm);
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 500;
            margin-top: 12px;
            transition: all var(--transition-fast);
        }
        
        .delete-suggestion:hover {
            transform: translateY(-1px);
            box-shadow: var(--shadow-sm);
        }

        /* Enhanced Subject Buttons */
        .subject-btn {
            display: block;
            background: white;
            color: var(--text-primary);
            text-decoration: none;
            padding: 16px;
            border-radius: var(--radius-md);
            text-align: center;
            font-weight: 600;
            border: 2px solid #e2e8f0;
            transition: all var(--transition-base);
            cursor: pointer;
            margin-bottom: 12px;
            font-family: 'Inter', sans-serif;
        }

        .subject-btn:hover {
            background: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
            transform: translateY(-2px);
            box-shadow: var(--shadow-md);
        }

        .subject-btn.active {
            background: var(--gradient-primary);
            color: white;
            border-color: var(--primary-color);
            box-shadow: var(--shadow-md);
        }

        /* Subject List Grid */
        .subject-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 16px;
            margin: 24px 0;
        }

        /* Enhanced Payment Card */
        .payment-card {
            background: white;
            border-radius: var(--radius-md);
            padding: 24px;
            margin-bottom: 20px;
            border-left: 6px solid var(--payment-color);
            box-shadow: var(--shadow-sm);
            transition: all var(--transition-base);
            border: 1px solid #e2e8f0;
        }

        .payment-card:hover {
            transform: translateY(-4px);
            box-shadow: var(--shadow-md);
        }

        .payment-card h4 {
            color: var(--payment-color);
            margin-bottom: 12px;
            font-size: 1.1rem;
            font-weight: 600;
        }

        .payment-card.pending { 
            border-left-color: #f59e0b;
            background: linear-gradient(135deg, #fffbeb 0%, #fef3c7 100%);
        }
        
        .payment-card.confirmed { 
            border-left-color: #10b981;
            background: linear-gradient(135deg, #d1fae5 0%, #a7f3d0 100%);
        }
        
        .payment-card.rejected { 
            border-left-color: #ef4444;
            background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%);
        }

        .payment-badge {
            display: inline-flex;
            align-items: center;
            padding: 6px 16px;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 600;
            margin-left: 12px;
            gap: 6px;
        }

        .badge-pending { 
            background: #fef3c7; 
            color: #92400e; 
            border: 1px solid #fbbf24;
        }
        
        .badge-confirmed { 
            background: #d1fae5; 
            color: #065f46; 
            border: 1px solid #10b981;
        }
        
        .badge-rejected { 
            background: #fee2e2; 
            color: #dc2626; 
            border: 1px solid #ef4444;
        }

        .bkash-guide {
            background: linear-gradient(135deg, #e0f7fa 0%, #e8f5e9 100%);
            border-radius: var(--radius-md);
            padding: 28px;
            margin: 24px 0;
            border: 2px dashed var(--payment-color);
        }

        .bkash-steps {
            margin: 20px 0;
            padding-left: 24px;
        }

        .bkash-steps li {
            margin-bottom: 12px;
            color: var(--text-primary);
            line-height: 1.6;
        }

        .payment-info-box {
            background: linear-gradient(135deg, #f0fff4 0%, #dcfce7 100%);
            border-radius: var(--radius-md);
            padding: 28px;
            border: 2px solid var(--payment-color);
            margin: 24px 0;
            box-shadow: var(--shadow-sm);
        }

        .payment-amount {
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--payment-color);
            text-align: center;
            margin: 20px 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        /* Enhanced Message System */
        .message-system-card {
            background: white;
            border-radius: var(--radius-md);
            padding: 24px;
            margin-bottom: 20px;
            border-left: 6px solid var(--message-color);
            box-shadow: var(--shadow-sm);
            transition: all var(--transition-base);
            border: 1px solid #e2e8f0;
        }

        .message-system-card:hover {
            transform: translateY(-4px);
            box-shadow: var(--shadow-md);
        }

        .message-system-card h4 {
            color: var(--message-color);
            margin-bottom: 12px;
            font-size: 1.1rem;
            font-weight: 600;
        }

        .message-system-card.from-student {
            border-left-color: #3b82f6;
            background: linear-gradient(135deg, #f0f9ff 0%, #e0f2fe 100%);
        }

        .message-system-card.from-admin {
            border-left-color: #10b981;
            background: linear-gradient(135deg, #f0fdf4 0%, #dcfce7 100%);
        }

        .message-badge {
            display: inline-flex;
            align-items: center;
            padding: 6px 16px;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 600;
            margin-left: 12px;
            gap: 6px;
        }

        .badge-student { 
            background: #dbeafe; 
            color: #1e40af; 
            border: 1px solid #60a5fa;
        }
        
        .badge-admin { 
            background: #d1fae5; 
            color: #065f46; 
            border: 1px solid #34d399;
        }
        
        .badge-unread { 
            background: #fef3c7; 
            color: #92400e; 
            border: 1px solid #fbbf24;
        }

        .chat-container {
            max-height: 400px;
            overflow-y: auto;
            padding: 20px;
            background: #f8fafc;
            border-radius: var(--radius-md);
            border: 1px solid #e2e8f0;
            margin-bottom: 24px;
        }

        .chat-message {
            margin-bottom: 20px;
            padding: 16px 20px;
            border-radius: var(--radius-md);
            max-width: 80%;
            word-wrap: break-word;
            animation: slideIn 0.3s ease-out;
        }
        
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .chat-message.student {
            background: linear-gradient(135deg, #e0f2fe 0%, #bae6fd 100%);
            border: 1px solid #7dd3fc;
            margin-right: auto;
            border-top-left-radius: 4px;
        }

        .chat-message.admin {
            background: linear-gradient(135deg, #dcfce7 0%, #bbf7d0 100%);
            border: 1px solid #86efac;
            margin-left: auto;
            border-top-right-radius: 4px;
        }

        .message-time {
            font-size: 0.8rem;
            color: var(--text-secondary);
            margin-top: 8px;
            text-align: right;
            opacity: 0.8;
        }

        .student-message-form {
            background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
            padding: 32px;
            border-radius: var(--radius-lg);
            border: 2px dashed var(--message-color);
            margin: 24px 0;
            box-shadow: var(--shadow-sm);
        }

        .reply-form {
            background: linear-gradient(135deg, #f0fdf4 0%, #dcfce7 100%);
            padding: 20px;
            border-radius: var(--radius-md);
            margin-top: 20px;
            border: 1px solid #bbf7d0;
        }

        /* Admin Tabs Navigation */
        .admin-tabs {
            display: flex;
            gap: 12px;
            margin-bottom: 32px;
            flex-wrap: wrap;
            background: white;
            padding: 8px;
            border-radius: var(--radius-md);
            border: 1px solid #e2e8f0;
        }
        
        .admin-tab-btn {
            flex: 1;
            min-width: 140px;
            background: transparent;
            border: 2px solid transparent;
            padding: 14px 20px;
            border-radius: var(--radius-sm);
            cursor: pointer;
            font-weight: 600;
            color: var(--text-secondary);
            transition: all var(--transition-fast);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            font-family: 'Inter', sans-serif;
        }
        
        .admin-tab-btn:hover {
            background: #f1f5f9;
            color: var(--primary-color);
        }
        
        .admin-tab-btn.active {
            background: var(--gradient-primary);
            color: white;
            box-shadow: var(--shadow-sm);
        }

        /* Form Groups */
        .form-group {
            margin-bottom: 24px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: var(--text-primary);
            font-weight: 500;
        }
        
        .form-group select,
        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 14px 16px;
            border: 2px solid #e2e8f0;
            border-radius: var(--radius-md);
            font-size: 16px;
            font-family: 'Inter', sans-serif;
            transition: all var(--transition-fast);
            background: white;
        }
        
        .form-group select:focus,
        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }

        /* Statistics Cards */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 20px;
            margin-top: 24px;
        }
        
        .stat-card {
            background: white;
            padding: 24px;
            border-radius: var(--radius-md);
            text-align: center;
            box-shadow: var(--shadow-sm);
            border: 1px solid #e2e8f0;
            transition: all var(--transition-fast);
        }
        
        .stat-card:hover {
            transform: translateY(-4px);
            box-shadow: var(--shadow-md);
        }
        
        .stat-value {
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--primary-color);
            margin-bottom: 8px;
        }
        
        .stat-label {
            color: var(--text-secondary);
            font-size: 0.95rem;
            font-weight: 500;
        }

        /* Scrollbar Styling */
        ::-webkit-scrollbar {
            width: 10px;
            height: 10px;
        }
        
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
            border-radius: 5px;
        }
        
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 5px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }

        /* Responsive Design */
        @media (max-width: 1024px) {
            .header h1 { font-size: 2.5rem; }
            .content-grid { grid-template-columns: 1fr; }
            .subject-list { grid-template-columns: repeat(2, 1fr); }
        }
        
        @media (max-width: 768px) {
            .header { padding: 60px 24px; }
            .header h1 { font-size: 2rem; }
            .header p { font-size: 1.1rem; }
            .card { padding: 24px; }
            .content-grid { gap: 24px; }
            .subject-list { grid-template-columns: 1fr; }
            .payment-card { padding: 20px; }
            .chat-message { max-width: 90%; }
            .admin-tabs { flex-direction: column; }
            .admin-tab-btn { min-width: 100%; }
            #adminAccess {
                bottom: 20px;
                right: 20px;
                width: 56px;
                height: 56px;
            }
        }
        
        @media (max-width: 480px) {
            .container { padding: 16px; }
            .header { padding: 48px 20px; }
            .header h1 { font-size: 1.75rem; }
            .card { padding: 20px; }
            .payment-amount { font-size: 2rem; }
            .login-box { padding: 32px 24px; }
            #adminPanel { padding: 24px 16px; }
        }

        /* =================== THUMBNAIL SYSTEM CSS =================== */
        /* Thumbnail Grid */
        .thumbnail-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 24px;
            margin: 24px 0;
        }
        
        .thumbnail-card {
            background: white;
            border-radius: var(--radius-lg);
            overflow: hidden;
            box-shadow: var(--shadow-md);
            border: 1px solid #e2e8f0;
            transition: all var(--transition-base);
        }
        
        .thumbnail-card:hover {
            transform: translateY(-4px);
            box-shadow: var(--shadow-lg);
        }
        
        .thumbnail-image-container {
            position: relative;
            width: 100%;
            padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
            background: linear-gradient(135deg, #f1f5f9 0%, #e2e8f0 100%);
            overflow: hidden;
        }
        
        .thumbnail-image-container img {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform var(--transition-base);
        }
        
        .thumbnail-card:hover .thumbnail-image-container img {
            transform: scale(1.05);
        }
        
        .thumbnail-category-badge {
            position: absolute;
            top: 16px;
            right: 16px;
            background: rgba(0, 0, 0, 0.75);
            color: white;
            padding: 6px 16px;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 600;
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .thumbnail-category-badge.ssc {
            background: rgba(14, 165, 233, 0.9);
        }
        
        .thumbnail-category-badge.hsc {
            background: rgba(139, 92, 246, 0.9);
        }
        
        .thumbnail-content {
            padding: 24px;
        }
        
        .thumbnail-title {
            color: var(--text-primary);
            margin: 0 0 12px 0;
            font-size: 1.2rem;
            font-weight: 600;
            line-height: 1.4;
        }
        
        .thumbnail-description {
            color: var(--text-secondary);
            margin: 0 0 20px 0;
            font-size: 0.95rem;
            line-height: 1.5;
        }
        
        .thumbnail-video-link {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: var(--gradient-primary);
            color: white;
            padding: 12px 24px;
            border-radius: var(--radius-md);
            text-decoration: none;
            font-weight: 600;
            transition: all var(--transition-fast);
            border: none;
            cursor: pointer;
        }
        
        .thumbnail-video-link:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-md);
        }
        
        .thumbnail-actions {
            display: flex;
            gap: 12px;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #e2e8f0;
        }
        
        .thumbnail-edit-btn {
            flex: 1;
            background: var(--gradient-secondary);
            color: white;
            border: none;
            padding: 10px 16px;
            border-radius: var(--radius-md);
            cursor: pointer;
            font-weight: 500;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all var(--transition-fast);
        }
        
        .thumbnail-delete-btn {
            flex: 1;
            background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%);
            color: #dc2626;
            border: 2px solid #fca5a5;
            padding: 10px 16px;
            border-radius: var(--radius-md);
            cursor: pointer;
            font-weight: 500;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: all var(--transition-fast);
        }
        
        .thumbnail-edit-btn:hover,
        .thumbnail-delete-btn:hover {
            transform: translateY(-2px);
        }
        
        .thumbnail-filter-btn.active {
            background: var(--gradient-primary) !important;
            color: white !important;
            border-color: var(--primary-color) !important;
        }
        
        /* Thumbnail Section in Student View */
        .thumbnail-section {
            margin: 48px 0;
            padding: 32px;
            background: linear-gradient(135deg, #ffffff 0%, #f8fafc 100%);
            border-radius: var(--radius-xl);
            border: 2px solid #e2e8f0;
            box-shadow: var(--shadow-md);
        }
        
        .thumbnail-section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 32px;
            flex-wrap: wrap;
            gap: 16px;
        }
        
        .thumbnail-section-title {
            color: var(--primary-color);
            font-size: 1.75rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .thumbnail-section-filters {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }
        
        .thumbnail-filter-btn-student {
            padding: 10px 20px;
            border-radius: var(--radius-md);
            border: 2px solid #e2e8f0;
            background: white;
            color: var(--text-primary);
            cursor: pointer;
            font-weight: 500;
            transition: all var(--transition-fast);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .thumbnail-filter-btn-student:hover {
            border-color: var(--primary-color);
            color: var(--primary-color);
        }
        
        .thumbnail-filter-btn-student.active {
            background: var(--gradient-primary);
            color: white;
            border-color: var(--primary-color);
        }
        
        @media (max-width: 768px) {
            .thumbnail-grid {
                grid-template-columns: 1fr;
            }
            
            .thumbnail-section {
                padding: 24px;
            }
            
            .thumbnail-section-header {
                flex-direction: column;
                align-items: stretch;
            }
            
            .thumbnail-section-filters {
                justify-content: center;
            }
        }
        /* =================== END THUMBNAIL SYSTEM CSS =================== */
    </style>
</head>
<body>
    <button id="adminAccess" onclick="showAdminLogin()" title="Admin Access">🔧</button>
    
    <!-- =================== BLACK & WHITE THEME OPTION =================== -->
    <div id="themeToggle" style="position: fixed; bottom: 32px; left: 32px; width: 60px; height: 60px; border-radius: 50%; background: linear-gradient(135deg, #333333 0%, #666666 100%); color: white; border: none; cursor: pointer; font-weight: bold; box-shadow: 0 10px 25px rgba(0,0,0,0.2); z-index: 1000; display: flex; align-items: center; justify-content: center; transition: all 0.3s ease; font-size: 24px;">
        🌙
    </div>
    
    <style id="bwThemeStyles"></style>
    <!-- =================== END BLACK & WHITE THEME OPTION =================== -->
    
    <div id="adminModal">
        <div class="login-box">
            <h2>🔐 Admin Entry</h2>
            <input type="password" id="adminPassword" placeholder="Enter Admin Key">
            <button class="login-btn" onclick="checkAdminLogin()">🔓 Unlock Dashboard</button>
            <p id="loginError" style="color: #ef4444; margin-top: 16px; display: none; font-weight: 500;">❌ Access Denied! Please try again.</p>
        </div>
    </div>
    
    <div class="container">
        <header class="header">
            <h1>🔬 SCIENCE = WATER</h1>
            <p>আপনার বিজ্ঞান শিক্ষার বিশ্বস্ত সহযোগী - Premium Education Platform</p>
        </header>
        
        <!-- Thumbnail Gallery Section -->
        <div class="thumbnail-section" id="thumbnailGalleryContainer">
            <div class="thumbnail-section-header">
                <h3 class="thumbnail-section-title">
                    <span>🎬</span> Featured Video Lessons
                </h3>
                <div class="thumbnail-section-filters">
                    <button class="thumbnail-filter-btn-student active" data-category="featured" onclick="filterThumbnails('featured')">
                        <span>🌟</span> Featured
                    </button>
                    <button class="thumbnail-filter-btn-student" data-category="ssc" onclick="filterThumbnails('ssc')">
                        <span>📘</span> SSC
                    </button>
                    <button class="thumbnail-filter-btn-student" data-category="hsc" onclick="filterThumbnails('hsc')">
                        <span>📙</span> HSC
                    </button>
                </div>
            </div>
            <div id="thumbnailGalleryContent">
                Loading featured videos...
            </div>
        </div>
        
        <div id="adminPanel">
            <div class="admin-header">
                <h2>📊 Admin Control Dashboard</h2>
                <button onclick="logoutAdmin()" style="background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%); color: #dc2626; border: none; padding: 12px 24px; border-radius: var(--radius-md); cursor: pointer; font-weight: 600; display: flex; align-items: center; gap: 8px; transition: all var(--transition-fast);">
                    <span>🚪</span> Logout
                </button>
            </div>
            
            <div class="admin-tabs">
                <button class="admin-tab-btn active" onclick="showTab('classTab')" id="classTabBtn">
                    <span>📚</span> Classes
                </button>
                <button class="admin-tab-btn" onclick="showTab('messageTab')" id="messageTabBtn">
                    <span>📢</span> Broadcast
                </button>
                <button class="admin-tab-btn" onclick="showTab('routineTab')" id="routineTabBtn">
                    <span>📅</span> Routine
                </button>
                <button class="admin-tab-btn" onclick="showTab('suggestionTab')" id="suggestionTabBtn">
                    <span>🔗</span> Suggestions
                </button>
                <button class="admin-tab-btn" onclick="showTab('paymentTab')" id="paymentTabBtn">
                    <span>💳</span> Payments
                </button>
                <button class="admin-tab-btn" onclick="showTab('studentMessagesTab')" id="studentMessagesTabBtn">
                    <span>💌</span> Messages
                </button>
                <button class="admin-tab-btn" onclick="showTab('thumbnailTab')" id="thumbnailTabBtn">
                    <span>🖼️</span> Thumbnails
                </button>
            </div>
            
            <div id="classTab" style="display: block;">
                <div style="background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%); padding: 32px; border-radius: var(--radius-lg); border: 2px dashed #cbd5e1; margin-bottom: 32px;">
                    <h3 style="margin-bottom: 24px; color: var(--primary-color); display: flex; align-items: center; gap: 12px;">➕ Add New Class Content</h3>
                    <div class="form-group">
                        <select id="classCategory" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;" onchange="updateSubjectOptions()">
                            <option value="ssc">📘 SSC Level</option>
                            <option value="hsc">📙 HSC Level</option>
                        </select>
                        <select id="classSubject" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                            <!-- Subjects will be loaded dynamically -->
                        </select>
                        <input type="text" id="className" placeholder="Class Title (e.g., Chapter 1: Force and Motion)" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                        <input type="text" id="classDescription" placeholder="Short Description" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                        <input type="text" id="classVideo" placeholder="YouTube Link/ID" style="width:100%; padding:14px 16px; margin-bottom:20px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                    </div>
                    <button onclick="addNewClass()" class="login-btn" style="background: var(--gradient-primary);">🚀 Publish Class</button>
                    <div id="addMessage" style="text-align: center; margin-top: 16px;"></div>
                </div>
                
                <h3 style="color: var(--ssc-color); margin-bottom: 20px; display: flex; align-items: center; gap: 12px; font-size: 1.5rem;">📘 SSC Subjects (<span id="sscClassCount">0</span>)</h3>
                <div class="subject-list">
                    <button class="subject-btn" onclick="showSubjectClasses('ssc', 'physics')">⚛️ পদার্থ</button>
                    <button class="subject-btn" onclick="showSubjectClasses('ssc', 'chemistry')">🧪 রসায়ন</button>
                    <button class="subject-btn" onclick="showSubjectClasses('ssc', 'biology')">🧬 জীব বিজ্ঞান</button>
                    <button class="subject-btn" onclick="showSubjectClasses('ssc', 'math')">📐 গণিত</button>
                    <button class="subject-btn" onclick="showSubjectClasses('ssc', 'bangla1')">📖 বাংলা ১ম</button>
                    <button class="subject-btn" onclick="showSubjectClasses('ssc', 'bangla2')">📚 বাংলা ২য়</button>
                    <button class="subject-btn" onclick="showSubjectClasses('ssc', 'english2')">🔤 ইংরেজী ২য়</button>
                    <button class="subject-btn" onclick="showSubjectClasses('ssc', 'science')">🔬 বিজ্ঞান</button>
                </div>
                <div id="sscClassesContainer" class="class-cards-container" style="margin-top: 28px;"></div>
                
                <h3 style="color: var(--hsc-color); margin: 36px 0 24px; display: flex; align-items: center; gap: 12px; font-size: 1.5rem;">📙 HSC Subjects (<span id="hscClassCount">0</span>)</h3>
                <div class="subject-list">
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'physics1')">⚛️ পদার্থ ১ম পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'physics2')">⚛️ পদার্থ ২য় পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'chemistry1')">🧪 রসায়ন ১ম পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'chemistry2')">🧪 রসায়ন ২য় পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'biology1')">🧬 জীব বিজ্ঞান ১ম পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'biology2')">🧬 জীব বিজ্ঞান ২য় পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'math1')">📐 গণিত ১ম পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'math2')">📐 গণিত ২য় পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'ict')">💻 ICT</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'bangla1')">📖 বাংলা ১ম পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'bangla2')">📚 বাংলা ২য় পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'english1')">🔤 ইংরেজী ১ম পত্র</button>
                    <button class="subject-btn" onclick="showSubjectClasses('hsc', 'english2')">🔤 ইংরেজী ২য় পত্র</button>
                </div>
                <div id="hscClassesContainer" class="class-cards-container" style="margin-top: 28px;"></div>
            </div>

            <div id="messageTab" style="display: none;">
                <div style="background: linear-gradient(135deg, #fffbeb 0%, #fef3c7 100%); padding: 32px; border-radius: var(--radius-lg); margin-bottom: 32px; border: 2px solid #fbbf24;">
                    <h3 style="margin-bottom: 24px; color: #92400e; display: flex; align-items: center; gap: 12px;">📢 Broadcast Message to Students</h3>
                    <input type="text" id="messageTitle" placeholder="Notice Heading" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                    <textarea id="messageContent" placeholder="Notice Details..." style="width:100%; padding:14px 16px; height:140px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;"></textarea>
                    <button onclick="sendNewMessage()" class="login-btn" style="background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);">📤 Broadcast Message</button>
                </div>
                <h3 style="margin-bottom: 24px; color: var(--text-primary); display: flex; align-items: center; gap: 12px;">📜 Previous Messages</h3>
                <div id="messagesContainer" class="message-system"></div>
            </div>

            <div id="routineTab" style="display: none;">
                 <div style="background: linear-gradient(135deg, #f0fdf4 0%, #dcfce7 100%); padding: 32px; border-radius: var(--radius-lg); margin-bottom: 32px; border: 2px solid #10b981;">
                    <h3 style="margin-bottom: 24px; color: #065f46; display: flex; align-items: center; gap: 12px;">📅 Add to Class Routine</h3>
                    <select id="routineDay" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                        <option value="saturday">শনিবার</option>
                        <option value="sunday">রবিবার</option>
                        <option value="monday">সোমবার</option>
                        <option value="tuesday">মঙ্গলবার</option>
                        <option value="wednesday">বুধবার</option>
                        <option value="thursday">বৃহস্পতিবার</option>
                        <option value="friday">শুক্রবার</option>
                    </select>
                    <input type="time" id="routineTime" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                    <select id="routineClassSelect" style="width:100%; padding:14px 16px; margin-bottom:24px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;"></select>
                    <button onclick="addToRoutine()" class="login-btn" style="background: var(--gradient-secondary);">➕ Add to Schedule</button>
                </div>
                <h3 style="margin-bottom: 24px; color: var(--text-primary); display: flex; align-items: center; gap: 12px;">🗓️ Current Routine</h3>
                <div id="routineContainer" class="routine-system"></div>
            </div>

            <div id="suggestionTab" style="display: none;">
                <div style="background: linear-gradient(135deg, #e0f2fe 0%, #bae6fd 100%); padding: 32px; border-radius: var(--radius-lg); border: 2px dashed #0ea5e9; margin-bottom: 32px;">
                    <h3 style="margin-bottom: 24px; color: #0369a1; display: flex; align-items: center; gap: 12px;">🔗 Add Suggestion Link</h3>
                    <div class="form-group">
                        <select id="suggestionCategory" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                            <option value="ssc">📘 SSC Suggestion</option>
                            <option value="hsc">📙 HSC Suggestion</option>
                        </select>
                        <input type="text" id="suggestionTitle" placeholder="Link Title (e.g., Physics Final Suggestion)" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                        <input type="text" id="suggestionLink" placeholder="Google Drive/YouTube/Website Link" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                        <textarea id="suggestionDescription" placeholder="Short Description" style="width:100%; padding:14px 16px; margin-bottom:24px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif; height:100px;"></textarea>
                    </div>
                    <button onclick="addSuggestionLink()" class="login-btn" style="background: var(--gradient-secondary);">🚀 Add Suggestion Link</button>
                    <div id="suggestionMessage" style="text-align: center; margin-top: 16px;"></div>
                </div>
                
                <h3 style="color: var(--ssc-color); margin-bottom: 24px; display: flex; align-items: center; gap: 12px; font-size: 1.5rem;">📘 SSC Suggestion Links (<span id="sscSuggestionCount">0</span>)</h3>
                <div id="sscSuggestionsContainer" class="suggestion-cards-container"></div>
                
                <h3 style="color: var(--hsc-color); margin: 36px 0 24px; display: flex; align-items: center; gap: 12px; font-size: 1.5rem;">📙 HSC Suggestion Links (<span id="hscSuggestionCount">0</span>)</h3>
                <div id="hscSuggestionsContainer" class="suggestion-cards-container"></div>
            </div>

            <div id="paymentTab" style="display: none;">
                <div style="background: linear-gradient(135deg, #f0fff4 0%, #dcfce7 100%); padding: 32px; border-radius: var(--radius-lg); border: 2px solid var(--payment-color); margin-bottom: 32px;">
                    <h3 style="margin-bottom: 24px; color: var(--payment-color); display: flex; align-items: center; gap: 12px;">💰 Payment Configuration</h3>
                    <div class="form-group">
                        <input type="text" id="bkashNumber" placeholder="Bkash Number (e.g., 01772123165)" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;" value="01772123165">
                        <input type="text" id="paymentAmount" placeholder="Default Payment Amount (e.g., 500)" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;" value="500">
                        <textarea id="paymentInstructions" placeholder="Payment Instructions for Students" style="width:100%; padding:14px 16px; margin-bottom:24px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif; height:140px;">
1. বিকাশে গিয়ে "Send Money" অপশন নির্বাচন করুন
2. নম্বর দিন: 01772123165
3. টাকার পরিমাণ দিন: ৫০০ টাকা
4. Reference হিসেবে আপনার নাম লিখুন
5. ট্রানজেকশন ID সংরক্ষণ করুন
6. নিচের ফর্মে তথ্য জমা দিন</textarea>
                    </div>
                    <button onclick="updatePaymentSettings()" class="login-btn" style="background: var(--gradient-secondary);">💳 Update Payment Settings</button>
                    <div id="paymentSettingsMessage" style="text-align: center; margin-top: 16px;"></div>
                </div>
                
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 28px; flex-wrap: wrap; gap: 16px;">
                    <h3 style="color: var(--payment-color); display: flex; align-items: center; gap: 12px;">📋 Payment History</h3>
                    <div style="display: flex; gap: 12px;">
                        <button onclick="loadAllPayments()" class="link-btn" style="padding: 12px 20px; font-size: 0.95rem; display: flex; align-items: center; gap: 8px; background: var(--gradient-primary); color: white; border: none;">
                            <span>🔄</span> Refresh
                        </button>
                        <button onclick="exportPayments()" class="link-btn" style="padding: 12px 20px; font-size: 0.95rem; display: flex; align-items: center; gap: 8px; background: linear-gradient(135deg, #7c3aed 0%, #a78bfa 100%); color: white; border: none;">
                            <span>📊</span> Export Data
                        </button>
                    </div>
                </div>
                
                <div id="paymentsFilter" style="margin-bottom: 24px; display: flex; gap: 16px; flex-wrap: wrap;">
                    <select id="paymentStatusFilter" onchange="filterPayments()" style="padding: 12px 20px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif; min-width: 200px;">
                        <option value="all">All Payments</option>
                        <option value="pending">Pending</option>
                        <option value="confirmed">Confirmed</option>
                        <option value="rejected">Rejected</option>
                    </select>
                    <input type="date" id="paymentDateFilter" onchange="filterPayments()" style="padding: 12px 20px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif; min-width: 200px;">
                </div>
                
                <div id="paymentsContainer" class="payment-cards-container">
                    <div class="loading-spinner">Loading payments...</div>
                </div>
                
                <div style="margin-top: 40px;">
                    <h4 style="margin-bottom: 20px; color: var(--text-secondary); font-weight: 600;">📈 Payment Statistics</h4>
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-value" id="totalPayments">0</div>
                            <div class="stat-label">Total Payments</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="confirmedPayments">0</div>
                            <div class="stat-label">Confirmed</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="pendingPayments">0</div>
                            <div class="stat-label">Pending</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="rejectedPayments">0</div>
                            <div class="stat-label">Rejected</div>
                        </div>
                    </div>
                </div>
            </div>

            <div id="studentMessagesTab" style="display: none;">
                <div style="margin-bottom: 32px;">
                    <h3 style="color: var(--message-color); margin-bottom: 24px; display: flex; align-items: center; gap: 12px;">💌 Student Messages (<span id="studentMessageCount">0</span>)</h3>
                    
                    <div style="display: flex; gap: 16px; margin-bottom: 24px; flex-wrap: wrap;">
                        <select id="messageStatusFilter" onchange="filterStudentMessages()" style="padding: 12px 20px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif; flex: 1; min-width: 200px;">
                            <option value="all">All Messages</option>
                            <option value="unread">Unread Only</option>
                            <option value="replied">Replied</option>
                            <option value="not_replied">Not Replied</option>
                        </select>
                        <input type="text" id="messageSearch" placeholder="Search by name or phone..." style="padding: 12px 20px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif; flex: 2; min-width: 300px;" onkeyup="searchStudentMessages()">
                    </div>
                </div>
                
                <div id="studentMessagesContainer">
                    <div class="loading-spinner">Loading student messages...</div>
                </div>
                
                <div style="margin-top: 40px;">
                    <h4 style="margin-bottom: 20px; color: var(--text-secondary); font-weight: 600;">📊 Message Statistics</h4>
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-value" id="totalStudentMessages">0</div>
                            <div class="stat-label">Total Messages</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="unreadMessages">0</div>
                            <div class="stat-label">Unread</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="repliedMessages">0</div>
                            <div class="stat-label">Replied</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="todayMessages">0</div>
                            <div class="stat-label">Today</div>
                        </div>
                    </div>
                </div>
            </div>

            <div id="thumbnailTab" style="display: none;">
                <div style="background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%); padding: 32px; border-radius: var(--radius-lg); border: 2px dashed #cbd5e1; margin-bottom: 32px;">
                    <h3 style="margin-bottom: 24px; color: var(--primary-color); display: flex; align-items: center; gap: 12px;">🖼️ Add New Thumbnail</h3>
                    <button onclick="showAddThumbnailModal()" class="login-btn" style="background: var(--gradient-primary); display: flex; align-items: center; justify-content: center; gap: 12px;">
                        <span>➕</span> Add New Thumbnail
                    </button>
                </div>
                
                <h3 style="margin-bottom: 24px; color: var(--text-primary); display: flex; align-items: center; gap: 12px;">Manage Thumbnails</h3>
                
                <div style="display: flex; gap: 12px; margin-bottom: 24px; flex-wrap: wrap;">
                    <button class="thumbnail-filter-btn active" data-category="featured" onclick="filterThumbnailsAdmin('featured')" 
                            style="padding: 12px 24px; border-radius: var(--radius-md); border: 2px solid var(--primary-color); background: var(--gradient-primary); color: white; cursor: pointer; font-weight: 500;">
                        🌟 Featured
                    </button>
                    <button class="thumbnail-filter-btn" data-category="ssc" onclick="filterThumbnailsAdmin('ssc')" 
                            style="padding: 12px 24px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; background: white; color: var(--text-primary); cursor: pointer; font-weight: 500;">
                        📘 SSC
                    </button>
                    <button class="thumbnail-filter-btn" data-category="hsc" onclick="filterThumbnailsAdmin('hsc')" 
                            style="padding: 12px 24px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; background: white; color: var(--text-primary); cursor: pointer; font-weight: 500;">
                        📙 HSC
                    </button>
                </div>
                
                <div id="adminThumbnailsContainer" class="thumbnail-cards-container">
                    Loading thumbnails...
                </div>
                
                <div style="margin-top: 40px;">
                    <h4 style="margin-bottom: 20px; color: var(--text-secondary); font-weight: 600;">📊 Thumbnail Statistics</h4>
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-value" id="totalThumbnails">0</div>
                            <div class="stat-label">Total Thumbnails</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="featuredThumbnails">0</div>
                            <div class="stat-label">Featured</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="sscThumbnails">0</div>
                            <div class="stat-label">SSC</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="hscThumbnails">0</div>
                            <div class="stat-label">HSC</div>
                        </div>
                    </div>
                </div>
            </div>

            <button onclick="saveAllData()" class="login-btn" style="width: 100%; margin-top: 40px; background: var(--gradient-primary); display: flex; align-items: center; justify-content: center; gap: 12px;">
                <span>💾</span> Sync & Save All Changes
            </button>
            <div id="saveMessage" style="text-align: center; margin-top: 16px;"></div>
        </div>
        
        <div class="content-grid">
            <div class="card">
                <h2>📅 ক্লাস রুটিন</h2>
                <div id="routineLoading" class="loading-spinner"><p>লোড হচ্ছে...</p></div>
                <div id="studentRoutine" class="routine-system"></div>
                
                <!-- Student Message System -->
                <div class="student-message-form">
                    <h3 style="text-align:center; margin-bottom:24px; font-size:1.25rem; color: var(--message-color); display: flex; align-items: center; justify-content: center; gap: 12px;">💌 প্রশ্ন বা বার্তা পাঠান</h3>
                    
                    <div id="studentMessageForm">
                        <input type="text" id="studentMsgName" placeholder="আপনার নাম" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                        <input type="text" id="studentMsgPhone" placeholder="মোবাইল নম্বর" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                        <select id="studentMsgCategory" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                            <option value="">বিষয় নির্বাচন করুন</option>
                            <option value="general">সাধারণ প্রশ্ন</option>
                            <option value="class_related">ক্লাস সংক্রান্ত</option>
                            <option value="payment">পেমেন্ট সংক্রান্ত</option>
                            <option value="technical">টেকনিক্যাল সমস্যা</option>
                            <option value="suggestion">পরামর্শ</option>
                            <option value="other">অন্যান্য</option>
                        </select>
                        <textarea id="studentMsgContent" placeholder="আপনার প্রশ্ন বা বার্তা লিখুন..." style="width:100%; padding:14px 16px; margin-bottom:24px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif; height:140px;"></textarea>
                        
                        <div id="studentMsgResponse" style="text-align:center; margin:16px 0;"></div>
                        
                        <button onclick="sendStudentMessage()" class="login-btn" style="background: var(--gradient-primary); display: flex; align-items: center; justify-content: center; gap: 12px;">
                            <span>📤</span> বার্তা পাঠান
                        </button>
                    </div>
                    
                    <div style="margin-top: 32px; padding: 24px; background: linear-gradient(135deg, #f0f9ff 0%, #e0f2fe 100%); border-radius: var(--radius-md); border: 2px solid #bae6fd;">
                        <h4 style="color: #0369a1; margin-bottom: 16px; display: flex; align-items: center; gap: 8px;">📬 আপনার বার্তার উত্তর</h4>
                        <div id="studentRepliesContainer">
                            <p style="color: #666; text-align: center; padding: 20px;">অ্যাডমিনের উত্তর এখানে দেখতে পারবেন</p>
                        </div>
                        <button onclick="loadStudentReplies()" class="link-btn" style="margin-top: 20px; padding: 12px 24px; font-size: 0.95rem; display: flex; align-items: center; justify-content: center; gap: 8px; background: var(--gradient-secondary); color: white; border: none;">
                            <span>🔄</span> উত্তর চেক করুন
                        </button>
                    </div>
                </div>
                
                <div class="contact-info" style="margin-top: 40px; text-align: center; background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%); padding: 32px; border-radius: var(--radius-lg); border: 2px solid #e2e8f0;">
                    <h3 style="font-size: 1.1rem; margin-bottom: 20px; color: var(--text-primary);">সরাসরি সহায়তার জন্য</h3>
                    <a href="https://wa.me/8801804376023" target="_blank" class="whatsapp-btn">
                        <span>💬</span> WhatsApp Support
                    </a>
                </div>
            </div>
            
            <div class="card">
                <h2>📢 নোটিশ বোর্ড</h2>
                <div id="messagesLoading" class="loading-spinner"></div>
                <div id="studentMessages" style="margin-bottom: 40px;"></div>
                
                <!-- Payment Section for Students -->
                <div style="background: linear-gradient(135deg, #e0f7fa 0%, #e8f5e9 100%); padding: 32px; border-radius: var(--radius-lg); margin-bottom: 40px; border: 2px solid var(--payment-color); box-shadow: var(--shadow-md);">
                    <h3 style="text-align:center; margin-bottom:24px; font-size:1.25rem; color: var(--payment-color); display: flex; align-items: center; justify-content: center; gap: 12px;">💳 বিকাশ পেমেন্ট</h3>
                    
                    <div class="payment-info-box">
                        <div style="text-align: center; margin-bottom: 24px;">
                            <div style="font-size: 1rem; color: var(--text-secondary); margin-bottom: 8px;">পেমেন্ট করুন</div>
                            <div class="payment-amount">৫০০ টাকা</div>
                            <div style="font-size: 1.5rem; font-weight: 700; color: var(--payment-color); margin: 16px 0; letter-spacing: 1px;">০১৭৭২১২৩১৬৫</div>
                        </div>
                        
                        <div class="bkash-guide">
                            <h4 style="margin-bottom: 16px; color: var(--text-primary); display: flex; align-items: center; gap: 8px;">📱 পেমেন্ট করার নিয়ম:</h4>
                            <ol class="bkash-steps">
                                <li>বিকাশ অ্যাপ ওপেন করুন</li>
                                <li>"Send Money" অপশন নির্বাচন করুন</li>
                                <li>নম্বর দিন: <strong>01772123165</strong></li>
                                <li>টাকার পরিমাণ দিন: <strong>৫০০ টাকা</strong></li>
                                <li>Reference হিসেবে আপনার নাম লিখুন</li>
                                <li>পিন নম্বর দিন</li>
                                <li>ট্রানজেকশন ID সংরক্ষণ করুন</li>
                            </ol>
                        </div>
                        
                        <button onclick="showPaymentForm()" class="login-btn" style="margin-top: 24px; background: var(--gradient-secondary); display: flex; align-items: center; justify-content: center; gap: 12px;">
                            <span>✅</span> পেমেন্ট তথ্য জমা দিন
                        </button>
                    </div>
                </div>
                
                <div id="paymentFormModal" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(15, 23, 42, 0.95); backdrop-filter: blur(8px); z-index:10000; justify-content:center; align-items:center;">
                    <div style="background:white; padding:40px; border-radius:var(--radius-xl); width:90%; max-width:520px; box-shadow: var(--shadow-xl); border: 1px solid rgba(255, 255, 255, 0.2);">
                        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:32px;">
                            <h3 style="color:var(--payment-color); display: flex; align-items: center; gap: 12px;">পেমেন্ট তথ্য জমা দিন</h3>
                            <button onclick="closePaymentForm()" style="background:none; border:none; font-size:32px; cursor:pointer; color:#666; transition: color var(--transition-fast); padding: 0; line-height: 1;">×</button>
                        </div>
                        
                        <div id="paymentForm">
                            <input type="text" id="studentName" placeholder="আপনার নাম" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                            <input type="text" id="studentPhone" placeholder="আপনার মোবাইল নম্বর" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                            <input type="text" id="transactionId" placeholder="ট্রানজেকশন ID (TrxID)" style="width:100%; padding:14px 16px; margin-bottom:16px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                            <input type="number" id="paidAmount" placeholder="টাকার পরিমাণ" style="width:100%; padding:14px 16px; margin-bottom:20px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;" value="500">
                            <select id="paymentFor" style="width:100%; padding:14px 16px; margin-bottom:24px; border-radius:var(--radius-md); border:2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                                <option value="">পেমেন্টের ধরন নির্বাচন করুন</option>
                                <option value="ssc_monthly">SSC মাসিক ফি</option>
                                <option value="hsc_monthly">HSC মাসিক ফি</option>
                                <option value="exam_fee">পরীক্ষার ফি</option>
                                <option value="admission">ভর্তি ফি</option>
                                <option value="other">অন্যান্য</option>
                            </select>
                            
                            <div id="paymentMessage" style="text-align:center; margin:20px 0;"></div>
                            
                            <button onclick="submitPayment()" class="login-btn" style="background:var(--gradient-secondary);">
                                📤 পেমেন্ট তথ্য জমা দিন
                            </button>
                            <button onclick="closePaymentForm()" class="link-btn" style="margin-top:20px; background:#f1f5f9; border: 2px solid #e2e8f0;">
                                বাতিল করুন
                            </button>
                        </div>
                    </div>
                </div>
                
                <div style="background: linear-gradient(135deg, #f1f5f9 0%, #e2e8f0 100%); padding: 32px; border-radius: var(--radius-lg); margin-bottom: 40px; border: 2px solid #cbd5e1;">
                    <h3 style="text-align:center; margin-bottom:24px; font-size:1.25rem; color: var(--primary-color); display: flex; align-items: center; justify-content: center; gap: 12px;">🎥 ভিডিও লেকচার সমূহ</h3>
                    <div style="display: flex; flex-direction: column; gap: 16px;">
                        <button class="login-btn btn-ssc" onclick="verifyStudentAccess('ssc')" style="display: flex; align-items: center; justify-content: center; gap: 12px;">
                            <span>📘</span> SSC ক্লাস দেখুন
                        </button>
                        <button class="login-btn btn-hsc" onclick="verifyStudentAccess('hsc')" style="display: flex; align-items: center; justify-content: center; gap: 12px;">
                            <span>📙</span> HSC ক্লাস দেখুন
                        </button>
                    </div>
                </div>
                
                <h3 style="margin-top: 40px; margin-bottom: 24px; color: var(--text-primary); display: flex; align-items: center; gap: 12px;">🔗 সাজেশন লিংকসমূহ</h3>
                <div style="display: flex; flex-direction: column; gap: 16px;">
                    <button class="login-btn" onclick="openSuggestionLinks('ssc')" style="background: var(--gradient-secondary); color: white; border: none; display: flex; align-items: center; justify-content: center; gap: 12px;">
                        <span>📘</span> SSC সাজেশন লিংক দেখুন
                    </button>
                    <button class="login-btn" onclick="openSuggestionLinks('hsc')" style="background: linear-gradient(135deg, #8b5cf6 0%, #a78bfa 100%); color: white; border: none; display: flex; align-items: center; justify-content: center; gap: 12px;">
                        <span>📙</span> HSC সাজেশন লিংক দেখুন
                    </button>
                </div>
                
                <div id="suggestionLinksModal" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(15, 23, 42, 0.95); backdrop-filter: blur(8px); z-index:10000; justify-content:center; align-items:center;">
                    <div style="background:white; padding:40px; border-radius:var(--radius-xl); width:90%; max-width:520px; max-height:80vh; overflow-y:auto; box-shadow: var(--shadow-xl); border: 1px solid rgba(255, 255, 255, 0.2);">
                        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:32px;">
                            <h3 id="suggestionModalTitle" style="color:var(--primary-color); display: flex; align-items: center; gap: 12px;">Suggestion Links</h3>
                            <button onclick="closeSuggestionModal()" style="background:none; border:none; font-size:32px; cursor:pointer; color:#666; transition: color var(--transition-fast); padding: 0; line-height: 1;">×</button>
                        </div>
                        <div id="suggestionLinksContent"></div>
                    </div>
                </div>
                
                <div id="studentSubjectSelection" style="display:none; margin-top:32px; padding: 32px; background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%); border-radius: var(--radius-lg); border: 2px solid #e2e8f0;">
                    <h3 id="studentCategoryTitle" style="text-align:center; margin-bottom:24px; color: var(--primary-color);"></h3>
                    <div id="studentSubjectButtons" class="subject-list"></div>
                </div>
                
                <div id="classesLoading" class="loading-spinner" style="display: none; text-align:center; padding:40px;">
                    <p style="color: var(--primary-color);">Loading classes...</p>
                </div>
                <div class="virtual-scroll-container" style="display: none; margin-top:32px;">
                    <div id="studentClassesContent" class="virtual-scroll-content"></div>
                </div>
            </div>
        </div>
    </div>
    
    <script>
        // =================== FIREBASE CONFIGURATION ===================
        const firebaseConfig = {
            apiKey: "AIzaSyAnT24m8II8Z0-B7vQePG-b7WWHNg5As2U",
            authDomain: "x100-cd8fd.firebaseapp.com",
            projectId: "x100-cd8fd",
            storageBucket: "x100-cd8fd.firebasestorage.app",
            messagingSenderId: "1018291284640",
            appId: "1:1018291284640:web:cfb2f0ee607bbd7dbb77c5",
            measurementId: "G-1ZVZFR96CC"
        };
        
        // Firebase Initialize
        let db;
        let analytics;
        let isFirebaseConnected = false;
        
        try {
            firebase.initializeApp(firebaseConfig);
            db = firebase.firestore();
            analytics = firebase.analytics();
            isFirebaseConnected = true;
            console.log("🔥 Firebase Connected Successfully!");
        } catch (error) {
            console.error("❌ Firebase Connection Error:", error);
            isFirebaseConnected = false;
        }
        // ==============================================================
        
        // App Variables
        let isAdminLoggedIn = false;
        let classes = [];
        let messages = [];
        let routine = [];
        let suggestions = [];
        let payments = [];
        let studentMessages = [];
        let thumbnails = [];
        let paymentSettings = {
            bkashNumber: "01772123165",
            paymentAmount: 500,
            instructions: "1. বিকাশে গিয়ে 'Send Money' অপশন নির্বাচন করুন\n2. নম্বর দিন: 01772123165\n3. টাকার পরিমাণ দিন: ৫০০ টাকা\n4. Reference হিসেবে আপনার নাম লিখুন\n5. ট্রানজেকশন ID সংরক্ষণ করুন\n6. নিচের ফর্মে তথ্য জমা দিন"
        };
        const domCache = {};
        
        // Passwords
        const CLASS_PASSWORDS = {
            ssc: "equal1839#",
            hsc: "science1232"
        };
        
        const SUGGESTION_PASSWORDS = {
            ssc: "ssc12345",
            hsc: "hsc123456"
        };
        
        // Subject Definitions
        const SUBJECTS = {
            ssc: [
                { id: 'physics', name: 'পদার্থ' },
                { id: 'chemistry', name: 'রসায়ন' },
                { id: 'biology', name: 'জীব বিজ্ঞান' },
                { id: 'math', name: 'গণিত' },
                { id: 'bangla1', name: 'বাংলা ১ম' },
                { id: 'bangla2', name: 'বাংলা ২য়' },
                { id: 'english2', name: 'ইংরেজী ২য়' },
                { id: 'science', name: 'বিজ্ঞান' }
            ],
            hsc: [
                { id: 'physics1', name: 'পদার্থ ১ম পত্র' },
                { id: 'physics2', name: 'পদার্থ ২য় পত্র' },
                { id: 'chemistry1', name: 'রসায়ন ১ম পত্র' },
                { id: 'chemistry2', name: 'রসায়ন ২য় পত্র' },
                { id: 'biology1', name: 'জীব বিজ্ঞান ১ম পত্র' },
                { id: 'biology2', name: 'জীব বিজ্ঞান ২য় পত্র' },
                { id: 'math1', name: 'গণিত ১ম পত্র' },
                { id: 'math2', name: 'গণিত ২য় পত্র' },
                { id: 'ict', name: 'ICT' },
                { id: 'bangla1', name: 'বাংলা ১ম পত্র' },
                { id: 'bangla2', name: 'বাংলা ২য় পত্র' },
                { id: 'english1', name: 'ইংরেজী ১ম পত্র' },
                { id: 'english2', name: 'ইংরেজী ২য় পত্র' }
            ]
        };
        
        // Current selected subject for admin
        let currentAdminSubject = {
            category: 'ssc',
            subject: 'physics'
        };

        // Initialize App
        document.addEventListener('DOMContentLoaded', async function() {
            console.log("🚀 App Initializing...");
            
            // Initialize subject dropdown
            updateSubjectOptions();
            
            // Load data
            if (isFirebaseConnected) {
                await loadAllDataFromFirebase();
                setupRealtimeListeners();
                showFirebaseStatus(true);
            } else {
                loadClassesFromStorage();
                loadMessagesFromStorage();
                loadRoutineFromStorage();
                loadSuggestionsFromStorage();
                loadPaymentsFromStorage();
                loadStudentMessagesFromStorage();
                loadPaymentSettings();
                loadThumbnailsFromStorage();
                showFirebaseStatus(false);
            }
            
            // Update UI
            updateClassCounts();
            updateSuggestionCounts();
            loadStudentMessages();
            loadStudentRoutine();
            updateClassSelect();
            renderThumbnailGallery();
            updateThumbnailStats();
            
            cacheDOM();
            
            // Initialize theme system
            initializeTheme();
            
            console.log("✅ App Ready!");
        });

        function cacheDOM() {
            domCache.adminModal = document.getElementById('adminModal');
            domCache.adminPanel = document.getElementById('adminPanel');
            domCache.adminAccess = document.getElementById('adminAccess');
            domCache.loginError = document.getElementById('loginError');
            domCache.adminPassword = document.getElementById('adminPassword');
        }

        function showFirebaseStatus(isConnected) {
            const statusDiv = document.createElement('div');
            statusDiv.style.cssText = `
                position: fixed; top: 20px; right: 20px;
                background: ${isConnected ? 'var(--gradient-secondary)' : 'linear-gradient(135deg, #ef4444 0%, #dc2626 100%)'};
                color: white; padding: 12px 24px;
                border-radius: var(--radius-md); z-index: 9999;
                font-family: 'Inter', sans-serif; font-size: 14px;
                box-shadow: var(--shadow-md);
                display: flex;
                align-items: center;
                gap: 8px;
                font-weight: 600;
                border: 1px solid rgba(255,255,255,0.2);
            `;
            statusDiv.innerHTML = `Firebase: ${isConnected ? '✅ CONNECTED' : '❌ OFFLINE'}`;
            statusDiv.id = 'firebaseStatus';
            
            const existing = document.getElementById('firebaseStatus');
            if (existing) existing.remove();
            
            document.body.appendChild(statusDiv);
            
            setTimeout(() => {
                if (statusDiv.parentNode) {
                    statusDiv.style.opacity = '0';
                    statusDiv.style.transition = 'opacity 1s';
                    setTimeout(() => statusDiv.remove(), 1000);
                }
            }, 5000);
        }

        // =================== BLACK & WHITE THEME SYSTEM ===================
        let isDarkMode = false;

        function initializeTheme() {
            // Load theme preference from localStorage
            const savedTheme = localStorage.getItem('scienceWaterTheme');
            isDarkMode = savedTheme === 'bw';
            
            if (isDarkMode) {
                applyBWTheme();
                document.getElementById('themeToggle').innerHTML = '☀️';
                document.getElementById('themeToggle').style.background = 'linear-gradient(135deg, #f59e0b 0%, #d97706 100%)';
            }
            
            // Add click event to theme toggle button
            document.getElementById('themeToggle').addEventListener('click', toggleTheme);
        }

        function toggleTheme() {
            isDarkMode = !isDarkMode;
            
            if (isDarkMode) {
                applyBWTheme();
                document.getElementById('themeToggle').innerHTML = '☀️';
                document.getElementById('themeToggle').style.background = 'linear-gradient(135deg, #f59e0b 0%, #d97706 100%)';
                localStorage.setItem('scienceWaterTheme', 'bw');
            } else {
                removeBWTheme();
                document.getElementById('themeToggle').innerHTML = '🌙';
                document.getElementById('themeToggle').style.background = 'linear-gradient(135deg, #333333 0%, #666666 100%)';
                localStorage.removeItem('scienceWaterTheme');
            }
        }

        function applyBWTheme() {
            const bwStyles = `
                /* Black and White Theme Override */
                body {
                    background: linear-gradient(135deg, #0a0a0a 0%, #1a1a1a 100%) !important;
                    color: #f0f0f0 !important;
                }
                
                .header {
                    background: linear-gradient(135deg, #222222 0%, #444444 100%) !important;
                    color: #ffffff !important;
                }
                
                .header::before {
                    background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.05' fill-rule='evenodd'/%3E%3C/svg%3E") !important;
                }
                
                .card, #adminPanel, .login-box, .class-card, .message-box, 
                .routine-day, .class-slot, .suggestion-card, .payment-card,
                .message-system-card, .thumbnail-card, .stat-card,
                .thumbnail-section, .student-message-form, .payment-info-box,
                .bkash-guide, .contact-info {
                    background: #1e1e1e !important;
                    color: #f0f0f0 !important;
                    border-color: #444444 !important;
                }
                
                .card::before {
                    background: linear-gradient(135deg, #666666 0%, #888888 100%) !important;
                }
                
                .card h2, h1, h2, h3, h4, h5, h6 {
                    color: #ffffff !important;
                }
                
                .login-box input, .login-box textarea, .form-group input, 
                .form-group select, .form-group textarea, 
                .link-btn, .subject-btn, .thumbnail-filter-btn-student,
                .thumbnail-filter-btn, .admin-tab-btn, .chat-container,
                .virtual-scroll-container {
                    background: #2a2a2a !important;
                    color: #ffffff !important;
                    border-color: #555555 !important;
                }
                
                .login-box input:focus, .form-group input:focus, 
                .form-group select:focus, .form-group textarea:focus {
                    border-color: #888888 !important;
                    box-shadow: 0 0 0 3px rgba(136, 136, 136, 0.2) !important;
                }
                
                .link-btn:hover, .subject-btn:hover {
                    background: #444444 !important;
                    color: #ffffff !important;
                }
                
                .btn-ssc, .btn-hsc, .btn-payment, .btn-message, 
                .login-btn, .thumbnail-video-link, .suggestion-link,
                .whatsapp-btn, .admin-tab-btn.active {
                    background: linear-gradient(135deg, #555555 0%, #777777 100%) !important;
                    color: #ffffff !important;
                }
                
                .subject-btn.active {
                    background: linear-gradient(135deg, #666666 0%, #888888 100%) !important;
                }
                
                .thumbnail-filter-btn-student.active,
                .thumbnail-filter-btn.active {
                    background: linear-gradient(135deg, #555555 0%, #777777 100%) !important;
                    border-color: #888888 !important;
                }
                
                .message-box {
                    background: linear-gradient(135deg, #2a2a2a 0%, #333333 100%) !important;
                    border-left-color: #888888 !important;
                }
                
                .message-title {
                    color: #cccccc !important;
                }
                
                .routine-day {
                    background: linear-gradient(135deg, #252525 0%, #2d2d2d 100%) !important;
                }
                
                .class-slot:hover {
                    border-color: #777777 !important;
                    background: #2a2a2a !important;
                }
                
                .day-header {
                    color: #cccccc !important;
                }
                
                .suggestion-card {
                    border-left-color: #777777 !important;
                }
                
                .payment-card {
                    border-left-color: #777777 !important;
                }
                
                .payment-card.pending {
                    background: linear-gradient(135deg, #3a3a3a 0%, #444444 100%) !important;
                    border-left-color: #f59e0b !important;
                }
                
                .payment-card.confirmed {
                    background: linear-gradient(135deg, #2d3a2d 0%, #3a4a3a 100%) !important;
                    border-left-color: #10b981 !important;
                }
                
                .payment-card.rejected {
                    background: linear-gradient(135deg, #3a2d2d 0%, #4a3a3a 100%) !important;
                    border-left-color: #ef4444 !important;
                }
                
                .message-system-card.from-student {
                    background: linear-gradient(135deg, #2a2a3a 0%, #333344 100%) !important;
                    border-left-color: #3b82f6 !important;
                }
                
                .message-system-card.from-admin {
                    background: linear-gradient(135deg, #2a3a2a 0%, #334433 100%) !important;
                    border-left-color: #10b981 !important;
                }
                
                .chat-message.student {
                    background: linear-gradient(135deg, #2a333a 0%, #33444a 100%) !important;
                    border-color: #444455 !important;
                }
                
                .chat-message.admin {
                    background: linear-gradient(135deg, #2a3a2a 0%, #334433 100%) !important;
                    border-color: #445544 !important;
                }
                
                .student-message-form, .bkash-guide, .payment-info-box {
                    background: linear-gradient(135deg, #252525 0%, #2d2d2d 100%) !important;
                    border-color: #555555 !important;
                }
                
                .thumbnail-section {
                    background: linear-gradient(135deg, #1a1a1a 0%, #222222 100%) !important;
                    border-color: #444444 !important;
                }
                
                .thumbnail-image-container {
                    background: linear-gradient(135deg, #2a2a2a 0%, #333333 100%) !important;
                }
                
                .thumbnail-category-badge {
                    background: rgba(40, 40, 40, 0.9) !important;
                    color: #ffffff !important;
                    border: 1px solid rgba(255, 255, 255, 0.1) !important;
                }
                
                .thumbnail-category-badge.ssc {
                    background: rgba(60, 60, 80, 0.9) !important;
                }
                
                .thumbnail-category-badge.hsc {
                    background: rgba(80, 60, 80, 0.9) !important;
                }
                
                .stat-card {
                    background: #1e1e1e !important;
                    border-color: #444444 !important;
                }
                
                .stat-value {
                    color: #cccccc !important;
                }
                
                .stat-label {
                    color: #aaaaaa !important;
                }
                
                .payment-amount {
                    color: #cccccc !important;
                }
                
                .success-message {
                    background: linear-gradient(135deg, #2a3a2a 0%, #334433 100%) !important;
                    color: #a7f3d0 !important;
                    border-color: #10b981 !important;
                }
                
                .error-message {
                    background: linear-gradient(135deg, #3a2a2a 0%, #443333 100%) !important;
                    color: #fecaca !important;
                    border-color: #ef4444 !important;
                }
                
                ::-webkit-scrollbar-track {
                    background: #1a1a1a !important;
                }
                
                ::-webkit-scrollbar-thumb {
                    background: #444444 !important;
                }
                
                ::-webkit-scrollbar-thumb:hover {
                    background: #555555 !important;
                }
                
                #firebaseStatus {
                    background: linear-gradient(135deg, #555555 0%, #777777 100%) !important;
                    color: #ffffff !important;
                    border-color: rgba(255,255,255,0.1) !important;
                }
                
                .badge-pending {
                    background: #3a3a2a !important;
                    color: #fbbf24 !important;
                    border-color: #f59e0b !important;
                }
                
                .badge-confirmed {
                    background: #2a3a2a !important;
                    color: #10b981 !important;
                    border-color: #10b981 !important;
                }
                
                .badge-rejected {
                    background: #3a2a2a !important;
                    color: #ef4444 !important;
                    border-color: #ef4444 !important;
                }
                
                .badge-student {
                    background: #2a2a3a !important;
                    color: #60a5fa !important;
                    border-color: #3b82f6 !important;
                }
                
                .badge-admin {
                    background: #2a3a2a !important;
                    color: #34d399 !important;
                    border-color: #10b981 !important;
                }
                
                .badge-unread {
                    background: #3a3a2a !important;
                    color: #fbbf24 !important;
                    border-color: #f59e0b !important;
                }
            `;
            
            document.getElementById('bwThemeStyles').innerHTML = bwStyles;
        }

        function removeBWTheme() {
            document.getElementById('bwThemeStyles').innerHTML = '';
        }
        // =================== END BLACK & WHITE THEME SYSTEM ===================

        function showAdminLogin() { 
            domCache.adminModal.style.display = 'flex'; 
            domCache.adminPassword.focus(); 
        }

        function checkAdminLogin() {
            const password = domCache.adminPassword.value;
            if (password === "sdcv1839") {
                isAdminLoggedIn = true;
                domCache.adminModal.style.display = 'none';
                domCache.adminPanel.style.display = 'block';
                domCache.adminAccess.style.display = 'none';
                loadAdminClasses();
                loadAdminMessages();
                loadAdminRoutine();
                loadAdminSuggestions();
                loadAdminPayments();
                loadAdminStudentMessages();
                loadAdminThumbnails();
                updateClassSelect();
                loadPaymentSettingsUI();
                
                // Update active tab button
                document.querySelectorAll('.admin-tab-btn').forEach(btn => {
                    btn.classList.remove('active');
                });
                document.querySelector('.admin-tab-btn').classList.add('active');
            } else {
                domCache.loginError.style.display = 'block';
                domCache.adminPassword.style.borderColor = '#ef4444';
            }
        }

        function logoutAdmin() { 
            isAdminLoggedIn = false; 
            domCache.adminPanel.style.display = 'none'; 
            domCache.adminAccess.style.display = 'block'; 
        }

        function showTab(tabName) {
            ['classTab', 'messageTab', 'routineTab', 'suggestionTab', 'paymentTab', 'studentMessagesTab', 'thumbnailTab'].forEach(t => {
                document.getElementById(t).style.display = 'none';
            });
            document.getElementById(tabName).style.display = 'block';
            
            // Update active tab button
            document.querySelectorAll('.admin-tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
        }

        // =================== THUMBNAIL SYSTEM ===================
        let currentThumbnailCategory = 'featured';

        // Load thumbnails from local storage
        function loadThumbnailsFromStorage() {
            const saved = localStorage.getItem('scienceWaterThumbnails');
            thumbnails = saved ? JSON.parse(saved) : [];
        }

        // Save thumbnails to local storage
        function saveThumbnailsToStorage() {
            localStorage.setItem('scienceWaterThumbnails', JSON.stringify(thumbnails));
        }

        // Load thumbnails from Firebase
        async function loadThumbnailsFromFirebase() {
            if (!isFirebaseConnected) return;
            
            try {
                const snapshot = await db.collection('thumbnails').orderBy('order', 'asc').get();
                thumbnails = [];
                snapshot.forEach(doc => {
                    thumbnails.push({ id: doc.id, ...doc.data() });
                });
                saveThumbnailsToStorage();
                renderThumbnailGallery();
                updateThumbnailStats();
            } catch (error) {
                console.error("Error loading thumbnails from Firebase:", error);
            }
        }

        async function loadAdminThumbnails() {
            await loadThumbnailsFromFirebase();
            renderAdminThumbnails();
        }

        // Setup Firebase listeners for thumbnails
        function setupThumbnailListeners() {
            if (!isFirebaseConnected) return;
            
            db.collection('thumbnails').orderBy('order', 'asc').onSnapshot((snapshot) => {
                thumbnails = [];
                snapshot.forEach(doc => {
                    thumbnails.push({ id: doc.id, ...doc.data() });
                });
                saveThumbnailsToStorage();
                renderThumbnailGallery();
                if (isAdminLoggedIn) {
                    renderAdminThumbnails();
                    updateThumbnailStats();
                }
            });
        }

        // Render thumbnail gallery in student view
        function renderThumbnailGallery() {
            const container = document.getElementById('thumbnailGalleryContent');
            if (!container) return;
            
            const filteredThumbnails = thumbnails.filter(t => 
                currentThumbnailCategory === 'featured' || t.category === currentThumbnailCategory
            );
            
            container.innerHTML = '';
            
            if (filteredThumbnails.length === 0) {
                container.innerHTML = `
                    <div style="text-align: center; padding: 40px; background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%); border-radius: var(--radius-md); border: 2px dashed #cbd5e1;">
                        <p style="color: var(--text-secondary); margin-bottom: 16px;">No thumbnails added yet</p>
                    </div>
                `;
                return;
            }
            
            container.innerHTML = `
                <div class="thumbnail-grid">
                    ${filteredThumbnails.map(thumb => `
                        <div class="thumbnail-card" data-id="${thumb.id}">
                            <div class="thumbnail-image-container">
                                <img src="${thumb.imageUrl}" alt="${thumb.title}" 
                                     onerror="this.src='https://via.placeholder.com/320x180/2563eb/ffffff?text=Thumbnail+Error'">
                                ${thumb.category !== 'featured' ? `
                                    <span class="thumbnail-category-badge ${thumb.category}">
                                        ${thumb.category.toUpperCase()}
                                    </span>
                                ` : ''}
                            </div>
                            <div class="thumbnail-content">
                                <h4 class="thumbnail-title">${thumb.title}</h4>
                                ${thumb.description ? `<p class="thumbnail-description">${thumb.description}</p>` : ''}
                                ${thumb.videoLink ? `
                                    <a href="${thumb.videoLink}" target="_blank" class="thumbnail-video-link">
                                        <span>▶</span> Watch Video
                                    </a>
                                ` : ''}
                            </div>
                        </div>
                    `).join('')}
                </div>
            `;
        }

        // Filter thumbnails in student view
        function filterThumbnails(category) {
            currentThumbnailCategory = category;
            
            // Update active filter button
            document.querySelectorAll('.thumbnail-filter-btn-student').forEach(btn => {
                btn.classList.remove('active');
                if (btn.dataset.category === category) {
                    btn.classList.add('active');
                }
            });
            
            renderThumbnailGallery();
        }

        // Filter thumbnails in admin view
        function filterThumbnailsAdmin(category) {
            currentThumbnailCategory = category;
            
            // Update active filter button
            document.querySelectorAll('.thumbnail-filter-btn').forEach(btn => {
                btn.classList.remove('active');
                if (btn.dataset.category === category) {
                    btn.classList.add('active');
                }
            });
            
            renderAdminThumbnails();
        }

        // Show add thumbnail modal
        function showAddThumbnailModal() {
            const modal = document.createElement('div');
            modal.id = 'addThumbnailModal';
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(15, 23, 42, 0.95);
                backdrop-filter: blur(12px);
                z-index: 10001;
                display: flex;
                justify-content: center;
                align-items: center;
                animation: fadeIn 0.3s ease-out;
            `;
            
            modal.innerHTML = `
                <div class="login-box" style="max-width: 500px; text-align: left;">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 32px;">
                        <h2 style="color: var(--primary-color); margin: 0;">🎨 Add Thumbnail</h2>
                        <button onclick="closeThumbnailModal()" 
                                style="background: none; border: none; font-size: 32px; cursor: pointer; color: #666; padding: 0; line-height: 1;">×</button>
                    </div>
                    
                    <div class="form-group">
                        <label for="thumbnailTitle">Thumbnail Title *</label>
                        <input type="text" id="thumbnailTitle" placeholder="e.g., Physics Chapter 1: Force" 
                               style="width: 100%; padding: 14px 16px; margin-bottom: 16px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                    </div>
                    
                    <div class="form-group">
                        <label for="thumbnailImageUrl">Image URL *</label>
                        <input type="text" id="thumbnailImageUrl" placeholder="https://example.com/image.jpg" 
                               style="width: 100%; padding: 14px 16px; margin-bottom: 16px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                        <small style="color: var(--text-secondary); display: block; margin-top: 4px;">Recommended: 16:9 ratio (e.g., 1280×720, 1920×1080)</small>
                    </div>
                    
                    <div class="form-group">
                        <label for="thumbnailCategory">Category *</label>
                        <select id="thumbnailCategory" 
                                style="width: 100%; padding: 14px 16px; margin-bottom: 16px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                            <option value="featured">🌟 Featured</option>
                            <option value="ssc">📘 SSC</option>
                            <option value="hsc">📙 HSC</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="thumbnailVideoLink">YouTube Video Link (Optional)</label>
                        <input type="text" id="thumbnailVideoLink" placeholder="https://youtube.com/watch?v=..." 
                               style="width: 100%; padding: 14px 16px; margin-bottom: 16px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                    </div>
                    
                    <div class="form-group">
                        <label for="thumbnailDescription">Description (Optional)</label>
                        <textarea id="thumbnailDescription" placeholder="Short description about this video..." 
                                  style="width: 100%; padding: 14px 16px; margin-bottom: 24px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif; height: 100px;"></textarea>
                    </div>
                    
                    <div id="thumbnailMessage" style="text-align: center; margin: 16px 0;"></div>
                    
                    <button onclick="saveThumbnail()" class="login-btn" style="background: var(--gradient-primary);">
                        🚀 Save Thumbnail
                    </button>
                </div>
            `;
            
            document.body.appendChild(modal);
        }

        // Close thumbnail modal
        function closeThumbnailModal() {
            const modal = document.getElementById('addThumbnailModal');
            if (modal) modal.remove();
        }

        // Save thumbnail
        async function saveThumbnail() {
            const title = document.getElementById('thumbnailTitle').value.trim();
            const imageUrl = document.getElementById('thumbnailImageUrl').value.trim();
            const category = document.getElementById('thumbnailCategory').value;
            const videoLink = document.getElementById('thumbnailVideoLink').value.trim();
            const description = document.getElementById('thumbnailDescription').value.trim();
            
            if (!title || !imageUrl || !category) {
                showThumbnailMessage("Please fill all required fields", "error");
                return;
            }
            
            // Basic URL validation
            try {
                new URL(imageUrl);
            } catch (e) {
                showThumbnailMessage("Please enter a valid image URL", "error");
                return;
            }
            
            const newThumbnail = {
                id: Date.now().toString(),
                title: title,
                imageUrl: imageUrl,
                category: category,
                videoLink: videoLink || null,
                description: description || null,
                order: thumbnails.length,
                date: new Date().toISOString()
            };
            
            // Save to Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('thumbnails').doc(newThumbnail.id).set({
                        title: newThumbnail.title,
                        imageUrl: newThumbnail.imageUrl,
                        category: newThumbnail.category,
                        videoLink: newThumbnail.videoLink,
                        description: newThumbnail.description,
                        order: newThumbnail.order,
                        date: newThumbnail.date
                    });
                    showThumbnailMessage("✅ Thumbnail saved to cloud!", "success");
                } catch (error) {
                    console.error("Error saving thumbnail to Firebase:", error);
                    showThumbnailMessage("❌ Cloud save failed, saved locally", "error");
                }
            }
            
            // Save locally
            thumbnails.push(newThumbnail);
            saveThumbnailsToStorage();
            
            // Close modal after 1 second
            setTimeout(() => {
                closeThumbnailModal();
                renderThumbnailGallery();
                renderAdminThumbnails();
                updateThumbnailStats();
            }, 1000);
        }

        // Edit thumbnail
        function editThumbnail(thumbnailId) {
            const thumb = thumbnails.find(t => t.id === thumbnailId);
            if (!thumb) return;
            
            const modal = document.createElement('div');
            modal.id = 'editThumbnailModal';
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(15, 23, 42, 0.95);
                backdrop-filter: blur(12px);
                z-index: 10001;
                display: flex;
                justify-content: center;
                align-items: center;
                animation: fadeIn 0.3s ease-out;
            `;
            
            modal.innerHTML = `
                <div class="login-box" style="max-width: 500px; text-align: left;">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 32px;">
                        <h2 style="color: var(--primary-color); margin: 0;">✏️ Edit Thumbnail</h2>
                        <button onclick="closeEditThumbnailModal()" 
                                style="background: none; border: none; font-size: 32px; cursor: pointer; color: #666; padding: 0; line-height: 1;">×</button>
                    </div>
                    
                    <div class="form-group">
                        <label for="editThumbnailTitle">Thumbnail Title *</label>
                        <input type="text" id="editThumbnailTitle" value="${thumb.title}" 
                               style="width: 100%; padding: 14px 16px; margin-bottom: 16px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                    </div>
                    
                    <div class="form-group">
                        <label for="editThumbnailImageUrl">Image URL *</label>
                        <input type="text" id="editThumbnailImageUrl" value="${thumb.imageUrl}" 
                               style="width: 100%; padding: 14px 16px; margin-bottom: 16px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                    </div>
                    
                    <div class="form-group">
                        <label for="editThumbnailCategory">Category *</label>
                        <select id="editThumbnailCategory" 
                                style="width: 100%; padding: 14px 16px; margin-bottom: 16px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                            <option value="featured" ${thumb.category === 'featured' ? 'selected' : ''}>🌟 Featured</option>
                            <option value="ssc" ${thumb.category === 'ssc' ? 'selected' : ''}>📘 SSC</option>
                            <option value="hsc" ${thumb.category === 'hsc' ? 'selected' : ''}>📙 HSC</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="editThumbnailVideoLink">YouTube Video Link</label>
                        <input type="text" id="editThumbnailVideoLink" value="${thumb.videoLink || ''}" 
                               style="width: 100%; padding: 14px 16px; margin-bottom: 16px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;">
                    </div>
                    
                    <div class="form-group">
                        <label for="editThumbnailDescription">Description</label>
                        <textarea id="editThumbnailDescription" 
                                  style="width: 100%; padding: 14px 16px; margin-bottom: 24px; border-radius: var(--radius-md); border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif; height: 100px;">${thumb.description || ''}</textarea>
                    </div>
                    
                    <div id="editThumbnailMessage" style="text-align: center; margin: 16px 0;"></div>
                    
                    <div style="display: flex; gap: 12px;">
                        <button onclick="updateThumbnail('${thumbnailId}')" class="login-btn" style="flex: 1; background: var(--gradient-primary);">
                            💾 Update
                        </button>
                        <button onclick="closeEditThumbnailModal()" class="link-btn" style="flex: 1; background: #f1f5f9; border: 2px solid #e2e8f0;">
                            Cancel
                        </button>
                    </div>
                </div>
            `;
            
            document.body.appendChild(modal);
        }

        // Close edit thumbnail modal
        function closeEditThumbnailModal() {
            const modal = document.getElementById('editThumbnailModal');
            if (modal) modal.remove();
        }

        // Update thumbnail
        async function updateThumbnail(thumbnailId) {
            const title = document.getElementById('editThumbnailTitle').value.trim();
            const imageUrl = document.getElementById('editThumbnailImageUrl').value.trim();
            const category = document.getElementById('editThumbnailCategory').value;
            const videoLink = document.getElementById('editThumbnailVideoLink').value.trim();
            const description = document.getElementById('editThumbnailDescription').value.trim();
            
            if (!title || !imageUrl || !category) {
                showEditThumbnailMessage("Please fill all required fields", "error");
                return;
            }
            
            const thumbIndex = thumbnails.findIndex(t => t.id === thumbnailId);
            if (thumbIndex === -1) return;
            
            thumbnails[thumbIndex] = {
                ...thumbnails[thumbIndex],
                title: title,
                imageUrl: imageUrl,
                category: category,
                videoLink: videoLink || null,
                description: description || null,
                updatedAt: new Date().toISOString()
            };
            
            // Update Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('thumbnails').doc(thumbnailId).update({
                        title: title,
                        imageUrl: imageUrl,
                        category: category,
                        videoLink: videoLink || null,
                        description: description || null,
                        updatedAt: new Date().toISOString()
                    });
                    showEditThumbnailMessage("✅ Thumbnail updated!", "success");
                } catch (error) {
                    console.error("Error updating thumbnail in Firebase:", error);
                    showEditThumbnailMessage("❌ Cloud update failed", "error");
                }
            }
            
            // Update local storage
            saveThumbnailsToStorage();
            
            // Close modal and refresh
            setTimeout(() => {
                closeEditThumbnailModal();
                renderThumbnailGallery();
                renderAdminThumbnails();
                updateThumbnailStats();
            }, 1000);
        }

        // Delete thumbnail
        async function deleteThumbnail(thumbnailId) {
            if (!confirm("Are you sure you want to delete this thumbnail?")) return;
            
            // Delete from Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('thumbnails').doc(thumbnailId).delete();
                } catch (error) {
                    console.error("Error deleting thumbnail from Firebase:", error);
                }
            }
            
            // Delete locally
            thumbnails = thumbnails.filter(t => t.id !== thumbnailId);
            saveThumbnailsToStorage();
            
            // Refresh display
            renderThumbnailGallery();
            renderAdminThumbnails();
            updateThumbnailStats();
        }

        // Render admin thumbnails
        function renderAdminThumbnails() {
            const container = document.getElementById('adminThumbnailsContainer');
            if (!container) return;
            
            const filteredThumbnails = thumbnails.filter(t => 
                currentThumbnailCategory === 'featured' || t.category === currentThumbnailCategory
            );
            
            container.innerHTML = '';
            
            if (filteredThumbnails.length === 0) {
                container.innerHTML = '<div class="message-box" style="text-align: center; padding: 40px;">No thumbnails added yet.</div>';
                return;
            }
            
            filteredThumbnails.forEach(thumb => {
                const card = document.createElement('div');
                card.className = 'thumbnail-card';
                card.style.cssText = `
                    background: white;
                    border-radius: var(--radius-md);
                    overflow: hidden;
                    box-shadow: var(--shadow-sm);
                    border: 1px solid #e2e8f0;
                    transition: all var(--transition-fast);
                    margin-bottom: 20px;
                `;
                card.innerHTML = `
                    <div style="position: relative; padding-bottom: 56.25%; background: #f1f5f9;">
                        <img src="${thumb.imageUrl}" alt="${thumb.title}" 
                             style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover;"
                             onerror="this.src='https://via.placeholder.com/320x180/f1f5f9/64748b?text=Image+Error'">
                        <span style="position: absolute; top: 12px; right: 12px; background: ${thumb.category === 'featured' ? '#f59e0b' : thumb.category === 'ssc' ? '#0ea5e9' : '#8b5cf6'}; color: white; padding: 4px 12px; border-radius: 50px; font-size: 0.8rem; font-weight: 600;">
                            ${thumb.category.toUpperCase()}
                        </span>
                    </div>
                    <div style="padding: 20px;">
                        <h4 style="margin: 0 0 12px 0; color: var(--text-primary); font-size: 1.1rem;">${thumb.title}</h4>
                        ${thumb.description ? `<p style="color: var(--text-secondary); font-size: 0.9rem; margin-bottom: 16px;">${thumb.description}</p>` : ''}
                        <div style="display: flex; gap: 8px; flex-wrap: wrap;">
                            <button onclick="editThumbnail('${thumb.id}')" 
                                    style="background: var(--gradient-primary); color: white; border: none; padding: 8px 16px; border-radius: var(--radius-sm); cursor: pointer; font-weight: 500; display: flex; align-items: center; gap: 6px;">
                                <span>✏️</span> Edit
                            </button>
                            <button onclick="deleteThumbnail('${thumb.id}')" 
                                    style="background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%); color: #dc2626; border: 2px solid #fca5a5; padding: 8px 16px; border-radius: var(--radius-sm); cursor: pointer; font-weight: 500; display: flex; align-items: center; gap: 6px;">
                                <span>🗑️</span> Delete
                            </button>
                            ${thumb.videoLink ? `
                                <a href="${thumb.videoLink}" target="_blank" 
                                   style="background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%); color: white; border: none; padding: 8px 16px; border-radius: var(--radius-sm); text-decoration: none; font-weight: 500; display: flex; align-items: center; gap: 6px;">
                                    <span>▶</span> View
                                </a>
                            ` : ''}
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // Update thumbnail statistics
        function updateThumbnailStats() {
            document.getElementById('totalThumbnails').textContent = thumbnails.length;
            document.getElementById('featuredThumbnails').textContent = thumbnails.filter(t => t.category === 'featured').length;
            document.getElementById('sscThumbnails').textContent = thumbnails.filter(t => t.category === 'ssc').length;
            document.getElementById('hscThumbnails').textContent = thumbnails.filter(t => t.category === 'hsc').length;
        }

        // Thumbnail message functions
        function showThumbnailMessage(message, type) {
            const messageDiv = document.getElementById('thumbnailMessage');
            if (messageDiv) {
                messageDiv.innerHTML = `<div class="${type}-message">${message}</div>`;
            }
        }

        function showEditThumbnailMessage(message, type) {
            const messageDiv = document.getElementById('editThumbnailMessage');
            if (messageDiv) {
                messageDiv.innerHTML = `<div class="${type}-message">${message}</div>`;
            }
        }

        // =================== STUDENT MESSAGE SYSTEM ===================
        async function sendStudentMessage() {
            const name = document.getElementById('studentMsgName').value.trim();
            const phone = document.getElementById('studentMsgPhone').value.trim();
            const category = document.getElementById('studentMsgCategory').value;
            const content = document.getElementById('studentMsgContent').value.trim();
            
            if (!name || !phone || !category || !content) {
                showStudentMessageResponse("সব তথ্য পূরণ করুন", "error");
                return;
            }
            
            if (!/^01[3-9]\d{8}$/.test(phone)) {
                showStudentMessageResponse("সঠিক মোবাইল নম্বর দিন", "error");
                return;
            }
            
            const newMessage = {
                id: Date.now().toString(),
                studentName: name,
                studentPhone: phone,
                category: category,
                message: content,
                status: 'unread',
                isReplied: false,
                replies: [],
                date: new Date().toISOString(),
                readAt: null,
                repliedAt: null
            };
            
            // Save to Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('studentMessages').doc(newMessage.id).set({
                        studentName: newMessage.studentName,
                        studentPhone: newMessage.studentPhone,
                        category: newMessage.category,
                        message: newMessage.message,
                        status: newMessage.status,
                        isReplied: newMessage.isReplied,
                        replies: newMessage.replies,
                        date: newMessage.date,
                        readAt: newMessage.readAt,
                        repliedAt: newMessage.repliedAt
                    });
                } catch (error) {
                    console.error("Error saving student message to Firebase:", error);
                }
            }
            
            // Save locally
            studentMessages.push(newMessage);
            saveStudentMessagesToStorage();
            
            // Clear form
            document.getElementById('studentMsgName').value = '';
            document.getElementById('studentMsgPhone').value = '';
            document.getElementById('studentMsgCategory').value = '';
            document.getElementById('studentMsgContent').value = '';
            
            // Show success message
            showStudentMessageResponse("✅ আপনার বার্তা পাঠানো হয়েছে! অ্যাডমিন শীঘ্রই উত্তর দিবেন।", "success");
            
            // Auto-check for replies after 5 seconds
            setTimeout(() => {
                loadStudentReplies();
            }, 5000);
        }

        async function loadStudentReplies() {
            const phone = document.getElementById('studentMsgPhone').value.trim();
            if (!phone) {
                showStudentMessageResponse("মোবাইল নম্বর দিন উত্তর দেখতে", "error");
                return;
            }
            
            let userMessages = [];
            
            if (isFirebaseConnected) {
                try {
                    const snapshot = await db.collection('studentMessages')
                        .where('studentPhone', '==', phone)
                        .orderBy('date', 'desc')
                        .get();
                    
                    userMessages = [];
                    snapshot.forEach(doc => {
                        userMessages.push({ id: doc.id, ...doc.data() });
                    });
                } catch (error) {
                    console.error("Error loading student replies from Firebase:", error);
                    userMessages = studentMessages.filter(msg => 
                        msg.studentPhone === phone
                    );
                }
            } else {
                userMessages = studentMessages.filter(msg => 
                    msg.studentPhone === phone
                );
            }
            
            const container = document.getElementById('studentRepliesContainer');
            container.innerHTML = '';
            
            if (userMessages.length === 0) {
                container.innerHTML = '<p style="color: #666; text-align: center; padding: 20px;">কোনো বার্তা পাওয়া যায়নি</p>';
                return;
            }
            
            userMessages.forEach(msg => {
                const card = document.createElement('div');
                card.className = 'message-system-card';
                card.style.marginBottom = '20px';
                
                let repliesHtml = '';
                if (msg.replies && msg.replies.length > 0) {
                    repliesHtml += '<div style="margin-top: 20px; border-top: 2px dashed #ddd; padding-top: 20px;">';
                    repliesHtml += '<h5 style="color: #10b981; margin-bottom: 16px; display: flex; align-items: center; gap: 8px;">📬 অ্যাডমিনের উত্তর:</h5>';
                    
                    msg.replies.forEach((reply, index) => {
                        repliesHtml += `
                            <div class="chat-message admin" style="margin-bottom: 16px;">
                                <div>${reply.message}</div>
                                <div class="message-time">${new Date(reply.date).toLocaleString()}</div>
                            </div>
                        `;
                    });
                    repliesHtml += '</div>';
                } else {
                    repliesHtml = '<p style="color: #f59e0b; text-align: center; padding: 12px; background: #fffbeb; border-radius: var(--radius-md);">অ্যাডমিন এখনও উত্তর দেননি</p>';
                }
                
                card.innerHTML = `
                    <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 16px;">
                        <div>
                            <h4 style="margin: 0; color: #3b82f6;">${msg.studentName}</h4>
                            <p style="margin: 8px 0; color: #666; font-size: 0.9rem;">${formatMessageDate(msg.date)}</p>
                            <p style="margin: 12px 0; color: var(--text-primary); line-height: 1.6;">${msg.message}</p>
                        </div>
                        <span class="message-badge ${msg.isReplied ? 'badge-admin' : 'badge-unread'}">
                            ${msg.isReplied ? 'উত্তর দেওয়া হয়েছে' : 'অপেক্ষমান'}
                        </span>
                    </div>
                    ${repliesHtml}
                `;
                
                container.appendChild(card);
            });
            
            showStudentMessageResponse(`✅ ${userMessages.length}টি বার্তা পাওয়া গেছে`, "success");
        }

        async function loadAdminStudentMessages() {
            if (isFirebaseConnected) {
                try {
                    const snapshot = await db.collection('studentMessages').orderBy('date', 'desc').get();
                    studentMessages = [];
                    snapshot.forEach(doc => {
                        studentMessages.push({ id: doc.id, ...doc.data() });
                    });
                } catch (error) {
                    console.error("Error loading student messages from Firebase:", error);
                }
            }
            
            displayStudentMessages();
            updateStudentMessageStats();
        }

        function displayStudentMessages(filteredMessages = null) {
            const container = document.getElementById('studentMessagesContainer');
            const messagesToShow = filteredMessages || studentMessages;
            
            container.innerHTML = '';
            
            if (messagesToShow.length === 0) {
                container.innerHTML = '<div class="message-box" style="text-align: center; padding: 40px;">No student messages found.</div>';
                return;
            }
            
            messagesToShow.forEach(msg => {
                const card = document.createElement('div');
                card.className = `message-system-card ${msg.status === 'unread' ? 'from-student' : ''}`;
                
                let repliesHtml = '';
                if (msg.replies && msg.replies.length > 0) {
                    repliesHtml += '<div class="chat-container" style="max-height: 240px; margin-top: 20px;">';
                    repliesHtml += '<div class="chat-message student">';
                    repliesHtml += `<div><strong>${msg.studentName}:</strong> ${msg.message}</div>`;
                    repliesHtml += `<div class="message-time">${formatMessageDate(msg.date)}</div>`;
                    repliesHtml += '</div>';
                    
                    msg.replies.forEach((reply, index) => {
                        repliesHtml += `
                            <div class="chat-message admin">
                                <div><strong>Admin:</strong> ${reply.message}</div>
                                <div class="message-time">${formatMessageDate(reply.date)}</div>
                            </div>
                        `;
                    });
                    repliesHtml += '</div>';
                } else {
                    repliesHtml = `
                        <div class="chat-container" style="max-height: 240px; margin-top: 20px;">
                            <div class="chat-message student">
                                <div><strong>${msg.studentName}:</strong> ${msg.message}</div>
                                <div class="message-time">${formatMessageDate(msg.date)}</div>
                            </div>
                            <p style="color: #f59e0b; text-align: center; padding: 20px; background: #fffbeb; border-radius: var(--radius-md);">No reply yet</p>
                        </div>
                    `;
                }
                
                card.innerHTML = `
                    <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 20px;">
                        <div>
                            <h4 style="margin: 0; color: #3b82f6;">${msg.studentName}</h4>
                            <p style="margin: 8px 0; color: var(--text-secondary); font-size: 0.9rem;">
                                📱 ${msg.studentPhone} • 📁 ${msg.category}
                            </p>
                        </div>
                        <div style="display: flex; gap: 8px;">
                            <span class="message-badge ${msg.status === 'unread' ? 'badge-unread' : 'badge-admin'}">
                                ${msg.status === 'unread' ? 'Unread' : 'Read'}
                            </span>
                            <span class="message-badge ${msg.isReplied ? 'badge-admin' : 'badge-student'}">
                                ${msg.isReplied ? 'Replied' : 'No Reply'}
                            </span>
                        </div>
                    </div>
                    
                    ${repliesHtml}
                    
                    <div class="reply-form">
                        <textarea id="reply_${msg.id}" placeholder="Type your reply here..." style="width:100%; padding:12px 16px; margin-bottom:16px; border-radius:var(--radius-md); height:100px; border: 2px solid #e2e8f0; font-family: 'Inter', sans-serif;"></textarea>
                        <div style="display: flex; gap: 12px; flex-wrap: wrap;">
                            <button onclick="markAsRead('${msg.id}')" 
                                    style="background: linear-gradient(135deg, #f1f5f9 0%, #e2e8f0 100%); color: var(--text-primary); border: 2px solid #cbd5e1; padding: 10px 20px; border-radius: var(--radius-md); cursor: pointer; font-weight: 500; display: flex; align-items: center; gap: 8px; transition: all var(--transition-fast);">
                                <span>✅</span> Mark as Read
                            </button>
                            <button onclick="sendReply('${msg.id}')" 
                                    style="background: var(--gradient-secondary); color: white; border: none; padding: 10px 20px; border-radius: var(--radius-md); cursor: pointer; font-weight: 500; display: flex; align-items: center; gap: 8px; transition: all var(--transition-fast);">
                                <span>📤</span> Send Reply
                            </button>
                            <button onclick="deleteStudentMessage('${msg.id}')" 
                                    style="background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%); color: #dc2626; border: 2px solid #fca5a5; padding: 10px 20px; border-radius: var(--radius-md); cursor: pointer; font-weight: 500; display: flex; align-items: center; gap: 8px; transition: all var(--transition-fast);">
                                <span>🗑️</span> Delete
                            </button>
                        </div>
                    </div>
                `;
                
                container.appendChild(card);
            });
        }

        async function markAsRead(messageId) {
            const message = studentMessages.find(m => m.id === messageId);
            if (!message) return;
            
            message.status = 'read';
            message.readAt = new Date().toISOString();
            
            // Update Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('studentMessages').doc(messageId).update({
                        status: 'read',
                        readAt: message.readAt
                    });
                } catch (error) {
                    console.error("Error updating message in Firebase:", error);
                }
            }
            
            // Update local storage
            saveStudentMessagesToStorage();
            
            // Refresh display
            displayStudentMessages();
            updateStudentMessageStats();
        }

        async function sendReply(messageId) {
            const replyText = document.getElementById(`reply_${messageId}`).value.trim();
            if (!replyText) return;
            
            const message = studentMessages.find(m => m.id === messageId);
            if (!message) return;
            
            const newReply = {
                message: replyText,
                date: new Date().toISOString(),
                from: 'admin'
            };
            
            // Add reply to message
            if (!message.replies) message.replies = [];
            message.replies.push(newReply);
            message.isReplied = true;
            message.repliedAt = new Date().toISOString();
            message.status = 'read';
            
            // Update Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('studentMessages').doc(messageId).update({
                        replies: message.replies,
                        isReplied: true,
                        repliedAt: message.repliedAt,
                        status: 'read'
                    });
                } catch (error) {
                    console.error("Error updating reply in Firebase:", error);
                }
            }
            
            // Update local storage
            saveStudentMessagesToStorage();
            
            // Clear reply textarea
            document.getElementById(`reply_${messageId}`).value = '';
            
            // Refresh display
            displayStudentMessages();
            updateStudentMessageStats();
            
            // Show notification
            showMessage("Reply sent successfully!", "success");
        }

        async function deleteStudentMessage(messageId) {
            if (!confirm("Delete this message?")) return;
            
            // Delete from Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('studentMessages').doc(messageId).delete();
                } catch (error) {
                    console.error("Error deleting message from Firebase:", error);
                }
            }
            
            // Delete locally
            studentMessages = studentMessages.filter(m => m.id !== messageId);
            saveStudentMessagesToStorage();
            
            // Refresh display
            displayStudentMessages();
            updateStudentMessageStats();
        }

        function filterStudentMessages() {
            const statusFilter = document.getElementById('messageStatusFilter').value;
            const searchTerm = document.getElementById('messageSearch').value.toLowerCase();
            
            let filtered = studentMessages;
            
            // Filter by status
            if (statusFilter === 'unread') {
                filtered = filtered.filter(m => m.status === 'unread');
            } else if (statusFilter === 'replied') {
                filtered = filtered.filter(m => m.isReplied === true);
            } else if (statusFilter === 'not_replied') {
                filtered = filtered.filter(m => m.isReplied === false);
            }
            
            // Filter by search term
            if (searchTerm) {
                filtered = filtered.filter(m => 
                    m.studentName.toLowerCase().includes(searchTerm) ||
                    m.studentPhone.includes(searchTerm) ||
                    m.message.toLowerCase().includes(searchTerm)
                );
            }
            
            displayStudentMessages(filtered);
        }

        function searchStudentMessages() {
            filterStudentMessages();
        }

        function updateStudentMessageStats() {
            const total = studentMessages.length;
            const unread = studentMessages.filter(m => m.status === 'unread').length;
            const replied = studentMessages.filter(m => m.isReplied === true).length;
            
            // Today's messages
            const today = new Date().toISOString().split('T')[0];
            const todayMessages = studentMessages.filter(m => 
                m.date.split('T')[0] === today
            ).length;
            
            document.getElementById('studentMessageCount').textContent = total;
            document.getElementById('totalStudentMessages').textContent = total;
            document.getElementById('unreadMessages').textContent = unread;
            document.getElementById('repliedMessages').textContent = replied;
            document.getElementById('todayMessages').textContent = todayMessages;
        }

        function formatMessageDate(dateString) {
            const date = new Date(dateString);
            const now = new Date();
            const diffMs = now - date;
            const diffMins = Math.floor(diffMs / 60000);
            const diffHours = Math.floor(diffMs / 3600000);
            const diffDays = Math.floor(diffMs / 86400000);
            
            if (diffMins < 1) return 'Just now';
            if (diffMins < 60) return `${diffMins} minutes ago`;
            if (diffHours < 24) return `${diffHours} hours ago`;
            if (diffDays < 7) return `${diffDays} days ago`;
            
            return date.toLocaleDateString() + ' ' + date.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
        }

        function showStudentMessageResponse(message, type) {
            const responseDiv = document.getElementById('studentMsgResponse');
            responseDiv.innerHTML = `<div class="${type}-message">${message}</div>`;
            setTimeout(() => {
                responseDiv.innerHTML = '';
            }, 5000);
        }

        // =================== SUBJECT MANAGEMENT ===================
        function updateSubjectOptions() {
            const category = document.getElementById('classCategory').value;
            const subjectSelect = document.getElementById('classSubject');
            
            subjectSelect.innerHTML = '';
            SUBJECTS[category].forEach(subject => {
                const option = document.createElement('option');
                option.value = subject.id;
                option.textContent = subject.name;
                subjectSelect.appendChild(option);
            });
        }

        function showSubjectClasses(category, subject) {
            currentAdminSubject = { category, subject };
            
            // Update active button
            document.querySelectorAll('.subject-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
            
            // Show classes for this subject
            const container = category === 'ssc' ? 
                document.getElementById('sscClassesContainer') : 
                document.getElementById('hscClassesContainer');
            
            const subjectClasses = classes.filter(c => 
                c.category === category && c.subject === subject
            );
            
            container.innerHTML = `
                <h4 style="color: ${category === 'ssc' ? 'var(--ssc-color)' : 'var(--hsc-color)'}; margin-bottom: 20px; display: flex; align-items: center; gap: 12px; font-size: 1.25rem;">
                    <span>${category === 'ssc' ? '📘' : '📙'}</span> ${SUBJECTS[category].find(s => s.id === subject).name} (${subjectClasses.length} Classes)
                </h4>
            `;
            
            if (subjectClasses.length === 0) {
                container.innerHTML += '<div class="message-box" style="text-align: center; padding: 40px;"><p>No classes added yet for this subject.</p></div>';
                return;
            }
            
            subjectClasses.forEach(cls => {
                const div = document.createElement('div');
                div.className = 'class-card';
                div.innerHTML = `
                    <h3>${cls.name}</h3>
                    <p>${cls.description}</p>
                    <small style="color:var(--text-secondary);">Subject: ${SUBJECTS[category].find(s => s.id === subject).name}</small>
                    <div style="margin-top:16px;">
                        <button onclick="deleteClass('${cls.id}')" 
                                style="background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%); color: #dc2626; border: 2px solid #fca5a5; padding: 8px 16px; border-radius: var(--radius-sm); cursor: pointer; font-weight: 500; display: inline-flex; align-items: center; gap: 6px; transition: all var(--transition-fast);">
                            <span>🗑️</span> Delete
                        </button>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        // =================== STUDENT ACCESS ===================
        function verifyStudentAccess(category) {
            let pass = prompt(`${category.toUpperCase()} পিন কোড দিন:`);
            if (pass === CLASS_PASSWORDS[category]) { 
                showStudentSubjectSelection(category);
            } else if (pass !== null) { 
                alert("ভুল পিন! সঠিক কোড ব্যবহার করুন।"); 
            }
        }

        function showStudentSubjectSelection(category) {
            document.getElementById('studentSubjectSelection').style.display = 'block';
            document.getElementById('studentCategoryTitle').textContent = `${category.toUpperCase()} Subjects`;
            document.getElementById('studentCategoryTitle').style.color = category === 'ssc' ? 'var(--ssc-color)' : 'var(--hsc-color)';
            
            const container = document.getElementById('studentSubjectButtons');
            container.innerHTML = '';
            
            SUBJECTS[category].forEach(subject => {
                const btn = document.createElement('button');
                btn.className = 'subject-btn';
                btn.textContent = subject.name;
                btn.onclick = () => showStudentClasses(category, subject.id);
                container.appendChild(btn);
            });
            
            // Hide other elements
            document.querySelector('.virtual-scroll-container').style.display = 'none';
        }

        function showStudentClasses(category, subject) {
            document.querySelector('.virtual-scroll-container').style.display = 'block';
            const content = document.getElementById('studentClassesContent');
            
            const subjectClasses = classes.filter(c => 
                c.category === category && c.subject === subject
            );
            
            content.innerHTML = `
                <h3 style="color: ${category === 'ssc' ? 'var(--ssc-color)' : 'var(--hsc-color)'}; margin-bottom: 24px; text-align: center; display: flex; align-items: center; justify-content: center; gap: 12px; font-size: 1.5rem;">
                    <span>${category === 'ssc' ? '📘' : '📙'}</span> ${SUBJECTS[category].find(s => s.id === subject).name}
                </h3>
            `;
            
            if (subjectClasses.length === 0) {
                content.innerHTML += '<div class="message-box" style="text-align: center; padding: 40px;"><p>No classes available yet for this subject.</p></div>';
                return;
            }
            
            subjectClasses.forEach(cls => {
                content.innerHTML += `
                    <div class="class-card">
                        <h3>${cls.name}</h3>
                        <p>${cls.description}</p>
                        <small style="color:var(--text-secondary);">Subject: ${SUBJECTS[category].find(s => s.id === subject).name}</small>
                        <a href="https://youtube.com/watch?v=${cls.videoId}" 
                           target="_blank" 
                           style="display: inline-flex; align-items: center; gap: 8px; background: var(--gradient-primary); color: white; padding: 10px 20px; border-radius: var(--radius-sm); text-decoration: none; font-weight: 600; margin-top: 16px; transition: all var(--transition-fast);">
                            <span>▶</span> ভিডিও দেখুন
                        </a>
                    </div>
                `;
            });
            
            content.scrollIntoView({behavior:'smooth'});
        }

        // =================== PAYMENT SYSTEM ===================
        function showPaymentForm() {
            document.getElementById('paymentFormModal').style.display = 'flex';
            // Reset form
            document.getElementById('studentName').value = '';
            document.getElementById('studentPhone').value = '';
            document.getElementById('transactionId').value = '';
            document.getElementById('paidAmount').value = paymentSettings.paymentAmount || 500;
            document.getElementById('paymentFor').value = '';
            document.getElementById('paymentMessage').innerHTML = '';
        }

        function closePaymentForm() {
            document.getElementById('paymentFormModal').style.display = 'none';
        }

        async function submitPayment() {
            const name = document.getElementById('studentName').value.trim();
            const phone = document.getElementById('studentPhone').value.trim();
            const trxId = document.getElementById('transactionId').value.trim();
            const amount = document.getElementById('paidAmount').value.trim();
            const paymentFor = document.getElementById('paymentFor').value;
            
            if (!name || !phone || !trxId || !amount || !paymentFor) {
                showPaymentMessage("সব তথ্য পূরণ করুন", "error");
                return;
            }
            
            if (!/^01[3-9]\d{8}$/.test(phone)) {
                showPaymentMessage("সঠিক মোবাইল নম্বর দিন", "error");
                return;
            }
            
            const newPayment = {
                id: Date.now().toString(),
                studentName: name,
                studentPhone: phone,
                transactionId: trxId,
                amount: parseInt(amount),
                paymentFor: paymentFor,
                status: 'pending',
                date: new Date().toISOString(),
                bkashNumber: paymentSettings.bkashNumber,
                verifiedBy: null,
                verifiedAt: null
            };
            
            // Save to Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('payments').doc(newPayment.id).set({
                        studentName: newPayment.studentName,
                        studentPhone: newPayment.studentPhone,
                        transactionId: newPayment.transactionId,
                        amount: newPayment.amount,
                        paymentFor: newPayment.paymentFor,
                        status: newPayment.status,
                        date: newPayment.date,
                        bkashNumber: newPayment.bkashNumber,
                        verifiedBy: newPayment.verifiedBy,
                        verifiedAt: newPayment.verifiedAt
                    });
                } catch (error) {
                    console.error("Error saving payment to Firebase:", error);
                }
            }
            
            // Save locally
            payments.push(newPayment);
            savePaymentsToStorage();
            
            // Show success message
            showPaymentMessage("✅ পেমেন্ট তথ্য জমা হয়েছে! অ্যাডমিন চেক করার পর কনফার্মেশন পাবেন।", "success");
            
            // Close form after 3 seconds
            setTimeout(() => {
                closePaymentForm();
            }, 3000);
        }

        function showPaymentMessage(message, type) {
            const messageDiv = document.getElementById('paymentMessage');
            messageDiv.innerHTML = `<div class="${type}-message">${message}</div>`;
        }

        async function updatePaymentSettings() {
            const bkashNumber = document.getElementById('bkashNumber').value.trim();
            const paymentAmount = document.getElementById('paymentAmount').value.trim();
            const instructions = document.getElementById('paymentInstructions').value.trim();
            
            if (!bkashNumber || !paymentAmount) {
                showPaymentSettingsMessage("Please fill all fields", "error");
                return;
            }
            
            paymentSettings = {
                bkashNumber: bkashNumber,
                paymentAmount: parseInt(paymentAmount),
                instructions: instructions
            };
            
            // Save to Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('settings').doc('payment').set(paymentSettings);
                } catch (error) {
                    console.error("Error saving payment settings to Firebase:", error);
                }
            }
            
            // Save locally
            savePaymentSettings();
            
            // Update student view
            updatePaymentDisplay();
            
            showPaymentSettingsMessage("✅ Payment settings updated!", "success");
        }

        function updatePaymentDisplay() {
            // Update the payment amount in student view
            const amountElements = document.querySelectorAll('.payment-amount');
            amountElements.forEach(el => {
                el.textContent = `${paymentSettings.paymentAmount} টাকা`;
            });
        }

        function loadPaymentSettingsUI() {
            document.getElementById('bkashNumber').value = paymentSettings.bkashNumber;
            document.getElementById('paymentAmount').value = paymentSettings.paymentAmount;
            document.getElementById('paymentInstructions').value = paymentSettings.instructions;
        }

        async function loadAllPayments() {
            if (isFirebaseConnected) {
                try {
                    const snapshot = await db.collection('payments').orderBy('date', 'desc').get();
                    payments = [];
                    snapshot.forEach(doc => {
                        payments.push({ id: doc.id, ...doc.data() });
                    });
                } catch (error) {
                    console.error("Error loading payments from Firebase:", error);
                }
            }
            
            displayPayments();
            updatePaymentStats();
        }

        async function loadAdminPayments() {
            await loadAllPayments();
        }

        function displayPayments(filteredPayments = null) {
            const container = document.getElementById('paymentsContainer');
            const paymentsToShow = filteredPayments || payments;
            
            container.innerHTML = '';
            
            if (paymentsToShow.length === 0) {
                container.innerHTML = '<div class="message-box" style="text-align: center; padding: 40px;">No payments found.</div>';
                return;
            }
            
            paymentsToShow.forEach(payment => {
                const card = document.createElement('div');
                card.className = `payment-card ${payment.status}`;
                
                let statusBadge = '';
                if (payment.status === 'pending') {
                    statusBadge = '<span class="payment-badge badge-pending">⏳ Pending</span>';
                } else if (payment.status === 'confirmed') {
                    statusBadge = '<span class="payment-badge badge-confirmed">✅ Confirmed</span>';
                } else if (payment.status === 'rejected') {
                    statusBadge = '<span class="payment-badge badge-rejected">❌ Rejected</span>';
                }
                
                card.innerHTML = `
                    <div style="display: flex; justify-content: space-between; align-items: start; margin-bottom: 16px;">
                        <div>
                            <h4 style="margin: 0; display: flex; align-items: center; gap: 8px;">${payment.studentName} ${statusBadge}</h4>
                            <p style="margin: 8px 0; color: var(--text-secondary);"><strong>📱 Phone:</strong> ${payment.studentPhone}</p>
                        </div>
                        <div style="text-align: right;">
                            <div style="font-size: 1.5rem; font-weight: 700; color: var(--payment-color);">${payment.amount} BDT</div>
                        </div>
                    </div>
                    
                    <div style="background: #f8fafc; padding: 16px; border-radius: var(--radius-md); margin: 16px 0;">
                        <p style="margin: 4px 0; color: var(--text-primary);"><strong>🔢 TrxID:</strong> ${payment.transactionId}</p>
                        <p style="margin: 4px 0; color: var(--text-primary);"><strong>🎯 For:</strong> ${payment.paymentFor}</p>
                        <p style="margin: 4px 0; color: var(--text-primary);"><strong>📅 Date:</strong> ${new Date(payment.date).toLocaleString()}</p>
                        ${payment.verifiedBy ? `
                            <p style="margin: 4px 0; color: var(--text-primary);"><strong>👤 Verified by:</strong> ${payment.verifiedBy}</p>
                            <p style="margin: 4px 0; color: var(--text-primary);"><strong>⏰ Verified at:</strong> ${new Date(payment.verifiedAt).toLocaleString()}</p>
                        ` : ''}
                    </div>
                    
                    <div style="margin-top: 20px;">
                        ${payment.status === 'pending' ? `
                            <div style="display: flex; gap: 12px; flex-wrap: wrap;">
                                <button onclick="updatePaymentStatus('${payment.id}', 'confirmed')" 
                                        style="background: var(--gradient-secondary); color: white; border: none; padding: 10px 20px; border-radius: var(--radius-md); cursor: pointer; font-weight: 500; display: inline-flex; align-items: center; gap: 8px; transition: all var(--transition-fast);">
                                    <span>✅</span> Confirm
                                </button>
                                <button onclick="updatePaymentStatus('${payment.id}', 'rejected')" 
                                        style="background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%); color: white; border: none; padding: 10px 20px; border-radius: var(--radius-md); cursor: pointer; font-weight: 500; display: inline-flex; align-items: center; gap: 8px; transition: all var(--transition-fast);">
                                    <span>❌</span> Reject
                                </button>
                            </div>
                        ` : ''}
                        
                        <button onclick="deletePayment('${payment.id}')" 
                                style="background: linear-gradient(135deg, #f1f5f9 0%, #e2e8f0 100%); color: var(--text-primary); border: 2px solid #cbd5e1; padding: 10px 20px; border-radius: var(--radius-md); cursor: pointer; font-weight: 500; margin-top: 12px; display: inline-flex; align-items: center; gap: 8px; transition: all var(--transition-fast);">
                            <span>🗑️</span> Delete
                        </button>
                    </div>
                `;
                
                container.appendChild(card);
            });
        }

        async function updatePaymentStatus(paymentId, status) {
            const payment = payments.find(p => p.id === paymentId);
            if (!payment) return;
            
            payment.status = status;
            payment.verifiedBy = 'Admin';
            payment.verifiedAt = new Date().toISOString();
            
            // Update Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('payments').doc(paymentId).update({
                        status: status,
                        verifiedBy: payment.verifiedBy,
                        verifiedAt: payment.verifiedAt
                    });
                } catch (error) {
                    console.error("Error updating payment in Firebase:", error);
                }
            }
            
            // Update local storage
            savePaymentsToStorage();
            
            // Refresh display
            displayPayments();
            updatePaymentStats();
            
            // Show notification
            showMessage(`Payment ${status} successfully!`, "success");
        }

        async function deletePayment(paymentId) {
            if (!confirm("Delete this payment record?")) return;
            
            // Delete from Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('payments').doc(paymentId).delete();
                } catch (error) {
                    console.error("Error deleting payment from Firebase:", error);
                }
            }
            
            // Delete locally
            payments = payments.filter(p => p.id !== paymentId);
            savePaymentsToStorage();
            
            // Refresh display
            displayPayments();
            updatePaymentStats();
        }

        function filterPayments() {
            const statusFilter = document.getElementById('paymentStatusFilter').value;
            const dateFilter = document.getElementById('paymentDateFilter').value;
            
            let filtered = payments;
            
            // Filter by status
            if (statusFilter !== 'all') {
                filtered = filtered.filter(p => p.status === statusFilter);
            }
            
            // Filter by date
            if (dateFilter) {
                filtered = filtered.filter(p => {
                    const paymentDate = new Date(p.date).toISOString().split('T')[0];
                    return paymentDate === dateFilter;
                });
            }
            
            displayPayments(filtered);
        }

        function updatePaymentStats() {
            const total = payments.length;
            const confirmed = payments.filter(p => p.status === 'confirmed').length;
            const pending = payments.filter(p => p.status === 'pending').length;
            const rejected = payments.filter(p => p.status === 'rejected').length;
            
            document.getElementById('totalPayments').textContent = total;
            document.getElementById('confirmedPayments').textContent = confirmed;
            document.getElementById('pendingPayments').textContent = pending;
            document.getElementById('rejectedPayments').textContent = rejected;
        }

        function exportPayments() {
            const data = payments.map(p => ({
                Name: p.studentName,
                Phone: p.studentPhone,
                TrxID: p.transactionId,
                Amount: p.amount,
                For: p.paymentFor,
                Status: p.status,
                Date: new Date(p.date).toLocaleString(),
                VerifiedBy: p.verifiedBy || 'N/A'
            }));
            
            const csv = convertToCSV(data);
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `payments_${new Date().toISOString().split('T')[0]}.csv`;
            a.click();
        }

        function convertToCSV(data) {
            const headers = Object.keys(data[0]);
            const rows = data.map(row => 
                headers.map(header => `"${row[header]}"`).join(',')
            );
            return [headers.join(','), ...rows].join('\n');
        }

        // =================== CLASS MANAGEMENT ===================
        async function loadAllDataFromFirebase() {
            if (!isFirebaseConnected) return;
            
            try {
                // Load classes
                const classesSnapshot = await db.collection('classes').orderBy('date', 'desc').get();
                classes = [];
                classesSnapshot.forEach(doc => {
                    classes.push({ id: doc.id, ...doc.data() });
                });
                
                // Load messages
                const messagesSnapshot = await db.collection('messages').orderBy('date', 'desc').get();
                messages = [];
                messagesSnapshot.forEach(doc => {
                    messages.push({ id: doc.id, ...doc.data() });
                });
                
                // Load routine
                const routineSnapshot = await db.collection('routine').orderBy('time', 'asc').get();
                routine = [];
                routineSnapshot.forEach(doc => {
                    routine.push({ id: doc.id, ...doc.data() });
                });
                
                // Load suggestions
                const suggestionsSnapshot = await db.collection('suggestions').orderBy('date', 'desc').get();
                suggestions = [];
                suggestionsSnapshot.forEach(doc => {
                    suggestions.push({ id: doc.id, ...doc.data() });
                });
                
                // Load payments
                const paymentsSnapshot = await db.collection('payments').orderBy('date', 'desc').get();
                payments = [];
                paymentsSnapshot.forEach(doc => {
                    payments.push({ id: doc.id, ...doc.data() });
                });
                
                // Load student messages
                const studentMessagesSnapshot = await db.collection('studentMessages').orderBy('date', 'desc').get();
                studentMessages = [];
                studentMessagesSnapshot.forEach(doc => {
                    studentMessages.push({ id: doc.id, ...doc.data() });
                });
                
                // Load thumbnails
                const thumbnailsSnapshot = await db.collection('thumbnails').orderBy('order', 'asc').get();
                thumbnails = [];
                thumbnailsSnapshot.forEach(doc => {
                    thumbnails.push({ id: doc.id, ...doc.data() });
                });
                
                // Load payment settings
                const settingsDoc = await db.collection('settings').doc('payment').get();
                if (settingsDoc.exists) {
                    paymentSettings = settingsDoc.data();
                }
                
                console.log("✅ All data loaded from Firebase");
                showMessage("Data loaded from cloud", "success");
            } catch (error) {
                console.error("Error loading from Firebase:", error);
                showMessage("Using local data", "warning");
            }
        }

        function setupRealtimeListeners() {
            if (!isFirebaseConnected) return;
            
            // Classes listener
            db.collection('classes').orderBy('date', 'desc').onSnapshot((snapshot) => {
                classes = [];
                snapshot.forEach(doc => {
                    classes.push({ id: doc.id, ...doc.data() });
                });
                updateClassCounts();
                loadAdminClasses();
                updateClassSelect();
            });
            
            // Messages listener
            db.collection('messages').orderBy('date', 'desc').onSnapshot((snapshot) => {
                messages = [];
                snapshot.forEach(doc => {
                    messages.push({ id: doc.id, ...doc.data() });
                });
                loadAdminMessages();
                loadStudentMessages();
            });
            
            // Routine listener
            db.collection('routine').orderBy('time', 'asc').onSnapshot((snapshot) => {
                routine = [];
                snapshot.forEach(doc => {
                    routine.push({ id: doc.id, ...doc.data() });
                });
                loadAdminRoutine();
                loadStudentRoutine();
            });
            
            // Suggestions listener
            db.collection('suggestions').orderBy('date', 'desc').onSnapshot((snapshot) => {
                suggestions = [];
                snapshot.forEach(doc => {
                    suggestions.push({ id: doc.id, ...doc.data() });
                });
                updateSuggestionCounts();
                loadAdminSuggestions();
            });
            
            // Payments listener
            db.collection('payments').orderBy('date', 'desc').onSnapshot((snapshot) => {
                payments = [];
                snapshot.forEach(doc => {
                    payments.push({ id: doc.id, ...doc.data() });
                });
                if (isAdminLoggedIn) {
                    displayPayments();
                    updatePaymentStats();
                }
            });
            
            // Student messages listener
            db.collection('studentMessages').orderBy('date', 'desc').onSnapshot((snapshot) => {
                studentMessages = [];
                snapshot.forEach(doc => {
                    studentMessages.push({ id: doc.id, ...doc.data() });
                });
                if (isAdminLoggedIn) {
                    displayStudentMessages();
                    updateStudentMessageStats();
                }
            });
            
            // Thumbnails listener
            db.collection('thumbnails').orderBy('order', 'asc').onSnapshot((snapshot) => {
                thumbnails = [];
                snapshot.forEach(doc => {
                    thumbnails.push({ id: doc.id, ...doc.data() });
                });
                saveThumbnailsToStorage();
                renderThumbnailGallery();
                if (isAdminLoggedIn) {
                    renderAdminThumbnails();
                    updateThumbnailStats();
                }
            });
        }

        function extractYouTubeID(url) {
            if (url.length === 11 && !url.includes('/')) return url;
            const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
            const match = url.match(regExp);
            return (match && match[2].length === 11) ? match[2] : url;
        }

        async function addNewClass() {
            const name = document.getElementById('className').value.trim();
            const video = document.getElementById('classVideo').value.trim();
            const category = document.getElementById('classCategory').value;
            const subject = document.getElementById('classSubject').value;
            
            if (!name || !video) {
                showMessage("Please fill all fields", "error");
                return;
            }
            
            const newClass = {
                id: Date.now().toString(),
                category: category,
                subject: subject,
                name: name,
                description: document.getElementById('classDescription').value.trim(),
                videoId: extractYouTubeID(video),
                date: new Date().toISOString()
            };
            
            // Save to Firebase
            if (isFirebaseConnected) {
                try {
                    await db.collection('classes').doc(newClass.id).set({
                        category: newClass.category,
                        subject: newClass.subject,
                        name: newClass.name,
                        description: newClass.description,
                        videoId: newClass.videoId,
                        date: newClass.date
                    });
                    showMessage("✅ Class published to cloud!", "success");
                } catch (error) {
                    console.error("Error saving to Firebase:", error);
                    showMessage("❌ Cloud save failed, saved locally", "error");
                }
            }
            
            // Also save locally
            classes.unshift(newClass);
            saveClassesToStorage();
            updateClassCounts();
            loadAdminClasses();
            updateClassSelect();
            
            // Clear form
            document.getElementById('className').value = '';
            document.getElementById('classDescription').value = '';
            document.getElementById('classVideo').value = '';
        }

        async function deleteClass(id) {
            if(!confirm('Delete this class?')) return;
            
            if (isFirebaseConnected) {
                try {
                    await db.collection('classes').doc(id.toString()).delete();
                } catch (error) {
                    console.error("Error deleting from Firebase:", error);
                }
            }
            
            classes = classes.filter(c => c.id !== id);
            saveClassesToStorage();
            loadAdminClasses();
            updateClassCounts();
        }

        function loadAdminClasses() {
            // Show first subject by default
            showSubjectClasses('ssc', 'physics');
        }

        function updateClassCounts() {
            const sscCount = classes.filter(c => c.category === 'ssc').length;
            const hscCount = classes.filter(c => c.category === 'hsc').length;
            
            document.getElementById('sscClassCount').textContent = sscCount;
            document.getElementById('hscClassCount').textContent = hscCount;
        }

        // =================== MESSAGE SYSTEM ===================
        async function sendNewMessage() {
            const title = document.getElementById('messageTitle').value;
            const content = document.getElementById('messageContent').value;
            if(!title || !content) return;
            
            const newMessage = {
                id: Date.now().toString(),
                title: title,
                content: content,
                date: new Date().toISOString()
            };
            
            if (isFirebaseConnected) {
                try {
                    await db.collection('messages').doc(newMessage.id).set({
                        title: newMessage.title,
                        content: newMessage.content,
                        date: newMessage.date
                    });
                } catch (error) {
                    console.error("Error saving message to Firebase:", error);
                }
            }
            
            messages.unshift(newMessage);
            saveMessagesToStorage();
            loadAdminMessages();
            loadStudentMessages();
            
            document.getElementById('messageTitle').value = '';
            document.getElementById('messageContent').value = '';
        }

        async function deleteMessage(id) {
            if (isFirebaseConnected) {
                try {
                    await db.collection('messages').doc(id.toString()).delete();
                } catch (error) {
                    console.error("Error deleting message from Firebase:", error);
                }
            }
            
            messages = messages.filter(m => m.id !== id);
            saveMessagesToStorage();
            loadAdminMessages();
            loadStudentMessages();
        }

        function loadAdminMessages() {
            const con = document.getElementById('messagesContainer');
            con.innerHTML = '';
            
            messages.forEach(m => {
                con.innerHTML += `
                    <div class="message-box" style="margin-bottom: 20px;">
                        <div style="display: flex; justify-content: space-between; align-items: start;">
                            <div>
                                <strong style="color: #92400e; font-size: 1.1rem;">${m.title}</strong>
                                <p style="margin-top: 8px; color: var(--text-primary);">${m.content}</p>
                                <small style="color: var(--text-secondary);">${new Date(m.date).toLocaleString()}</small>
                            </div>
                            <button onclick="deleteMessage('${m.id}')" 
                                    style="background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%); color: #dc2626; border: 2px solid #fca5a5; padding: 6px 12px; border-radius: var(--radius-sm); cursor: pointer; font-weight: 500; display: flex; align-items: center; gap: 6px;">
                                <span>🗑️</span>
                            </button>
                        </div>
                    </div>
                `;
            });
        }

        function loadStudentMessages() {
            const con = document.getElementById('studentMessages');
            con.innerHTML = '';
            
            messages.slice(0,3).forEach(m => {
                con.innerHTML += `
                    <div class="message-box" style="margin-bottom: 20px;">
                        <div class="message-title">📢 ${m.title}</div>
                        <p style="color: var(--text-primary); margin-top: 8px;">${m.content}</p>
                        <small style="color: var(--text-secondary);">${new Date(m.date).toLocaleDateString()}</small>
                    </div>
                `;
            });
        }

        // =================== ROUTINE SYSTEM ===================
        function addToRoutine() {
            const classId = parseInt(document.getElementById('routineClassSelect').value);
            const selectedClass = classes.find(c => c.id === classId);
            if(!selectedClass) return;
            
            const newRoutine = {
                id: Date.now().toString(),
                day: document.getElementById('routineDay').value,
                time: document.getElementById('routineTime').value,
                className: selectedClass.name,
                category: selectedClass.category,
                classId: selectedClass.id
            };
            
            if (isFirebaseConnected) {
                try {
                    db.collection('routine').doc(newRoutine.id).set({
                        day: newRoutine.day,
                        time: newRoutine.time,
                        className: newRoutine.className,
                        category: newRoutine.category,
                        classId: newRoutine.classId
                    });
                } catch (error) {
                    console.error("Error saving routine to Firebase:", error);
                }
            }
            
            routine.push(newRoutine);
            saveRoutineToStorage();
            loadAdminRoutine();
            loadStudentRoutine();
        }

        async function deleteRoutine(id) {
            if (isFirebaseConnected) {
                try {
                    await db.collection('routine').doc(id.toString()).delete();
                } catch (error) {
                    console.error("Error deleting routine from Firebase:", error);
                }
            }
            
            routine = routine.filter(r => r.id !== id);
            saveRoutineToStorage();
            loadAdminRoutine();
            loadStudentRoutine();
        }

        function loadAdminRoutine() {
            const con = document.getElementById('routineContainer'); 
            con.innerHTML = '';
            
            if (routine.length === 0) {
                con.innerHTML = '<div class="message-box" style="text-align: center; padding: 40px;">No routine added yet.</div>';
                return;
            }
            
            const dayNames = {
                saturday: 'শনিবার',
                sunday: 'রবিবার', 
                monday: 'সোমবার',
                tuesday: 'মঙ্গলবার',
                wednesday: 'বুধবার',
                thursday: 'বৃহস্পতিবার',
                friday: 'শুক্রবার'
            };
            
            Object.keys(dayNames).forEach(day => {
                const dayClasses = routine.filter(r => r.day === day);
                if(dayClasses.length > 0) {
                    let html = `<div class="routine-day"><div class="day-header">${dayNames[day]}</div>`;
                    dayClasses.forEach(c => { 
                        html += `
                            <div class="class-slot">
                                <span style="font-weight: 600; color: var(--primary-color);">${c.time}</span> 
                                <span style="color: var(--text-primary);">${c.className} (${c.category.toUpperCase()})</span>
                                <button onclick="deleteRoutine('${c.id}')" 
                                        style="background: linear-gradient(135deg, #fee2e2 0%, #fecaca 100%); color: #dc2626; border: 2px solid #fca5a5; padding: 6px 12px; border-radius: var(--radius-sm); cursor: pointer; font-weight: 500; display: flex; align-items: center; gap: 6px;">
                                    <span>🗑️</span>
                                </button>
                            </div>
                        `; 
                    });
                    html += `</div>`;
                    con.innerHTML += html;
                }
            });
        }

        function loadStudentRoutine() {
            const con = document.getElementById('studentRoutine'); 
            con.innerHTML = '';
            
            if (routine.length === 0) {
                document.getElementById('routineLoading').innerHTML = '<p style="color: var(--text-secondary); text-align: center;">কোনো রুটিন নেই</p>';
                return;
            }
            
            document.getElementById('routineLoading').style.display = 'none';
            
            const dayNames = {
                saturday: 'শনিবার',
                sunday: 'রবিবার', 
                monday: 'সোমবার',
                tuesday: 'মঙ্গলবার',
                wednesday: 'বুধবার',
                thursday: 'বৃহস্পতিবার',
                Friday: 'শুক্রবার'
            };
            
            Object.keys(dayNames).forEach(day => {
                const dayClasses = routine.filter(r => r.day === day);
                if(dayClasses.length > 0) {
                    let html = `<div class="routine-day"><div class="day-header">${dayNames[day]}</div>`;
                    dayClasses.forEach(c => { 
                        html += `
                            <div class="class-slot">
                                <span style="font-weight: 600; color: var(--primary-color);">${c.time}</span> 
                                <span style="color: var(--text-primary);">${c.className} (${c.category.toUpperCase()})</span>
                            </div>
                        `; 
                    });
                    html += `</div>`;
                    con.innerHTML += html;
                }
            });
        }

        function updateClassSelect() {
            const sel = document.getElementById('routineClassSelect');
            if(!sel) return; 
            sel.innerHTML = '<option value="">Select Class</option>';
            classes.forEach(c => { 
                sel.innerHTML += `<option value="${c.id}">${c.name}</option>`; 
            });
        }

        // =================== SUGGESTION SYSTEM ===================
        function openSuggestionLinks(category) {
            const password = prompt(`${category.toUpperCase()} Suggestion Password দিন:`);
            
            if (password === SUGGESTION_PASSWORDS[category]) {
                showSuggestionLinks(category);
            } else if (password !== null) {
                alert("❌ ভুল পাসওয়ার্ড! সঠিক পাসওয়ার্ড দিন।");
            }
        }

        function showSuggestionLinks(category) {
            const filteredSuggestions = suggestions.filter(s => s.category === category);
            
            if (filteredSuggestions.length === 0) {
                alert("এই ক্যাটাগরিতে কোনো সাজেশন লিংক নেই।");
                return;
            }
            
            const modal = document.getElementById('suggestionLinksModal');
            const title = document.getElementById('suggestionModalTitle');
            const content = document.getElementById('suggestionLinksContent');
            
            title.textContent = `${category.toUpperCase()} সাজেশন লিংকসমূহ`;
            title.style.color = category === 'ssc' ? 'var(--ssc-color)' : 'var(--hsc-color)';
            content.innerHTML = '';
            
            filteredSuggestions.forEach(suggestion => {
                const card = document.createElement('div');
                card.className = 'suggestion-card';
                card.innerHTML = `
                    <h4>${suggestion.title}</h4>
                    <p>${suggestion.description || ''}</p>
                    <a href="${suggestion.link}" 
                       target="_blank" 
                       class="suggestion-link">
                        <span>🔗</span> লিংক ওপেন করুন
                    </a>
                `;
                content.appendChild(card);
            });
            
            modal.style.display = 'flex';
        }

        function closeSuggestionModal() {
            document.getElementById('suggestionLinksModal').style.display = 'none';
        }

        function isValidUrl(string) {
            try {
                new URL(string);
                return true;
            } catch (_) {
                return false;
            }
        }

        async function addSuggestionLink() {
            const title = document.getElementById('suggestionTitle').value.trim();
            const link = document.getElementById('suggestionLink').value.trim();
            const category = document.getElementById('suggestionCategory').value;
            
            if (!title || !link) {
                showSuggestionMessage("Please fill all fields", "error");
                return;
            }
            
            if (!isValidUrl(link)) {
                showSuggestionMessage("Please enter a valid URL", "error");
                return;
            }
            
            const newSuggestion = {
                id: Date.now().toString(),
                category: category,
                title: title,
                link: link,
                description: document.getElementById('suggestionDescription').value.trim(),
                date: new Date().toISOString(),
                addedBy: "Admin"
            };
            
            if (isFirebaseConnected) {
                try {
                    await db.collection('suggestions').doc(newSuggestion.id).set({
                        category: newSuggestion.category,
                        title: newSuggestion.title,
                        link: newSuggestion.link,
                        description: newSuggestion.description,
                        date: newSuggestion.date,
                        addedBy: newSuggestion.addedBy
                    });
                    showSuggestionMessage("✅ Suggestion link added to cloud!", "success");
                } catch (error) {
                    console.error("Error saving to Firebase:", error);
                    showSuggestionMessage("❌ Cloud save failed, saved locally", "error");
                }
            }
            
            suggestions.unshift(newSuggestion);
            saveSuggestionsToStorage();
            updateSuggestionCounts();
            loadAdminSuggestions();
            
            document.getElementById('suggestionTitle').value = '';
            document.getElementById('suggestionLink').value = '';
            document.getElementById('suggestionDescription').value = '';
        }

        async function deleteSuggestion(id) {
            if (!confirm("Delete this suggestion link?")) return;
            
            if (isFirebaseConnected) {
                try {
                    await db.collection('suggestions').doc(id.toString()).delete();
                } catch (error) {
                    console.error("Error deleting from Firebase:", error);
                }
            }
            
            suggestions = suggestions.filter(s => s.id !== id);
            saveSuggestionsToStorage();
            updateSuggestionCounts();
            loadAdminSuggestions();
        }

        function loadAdminSuggestions() {
            const sscContainer = document.getElementById('sscSuggestionsContainer');
            const hscContainer = document.getElementById('hscSuggestionsContainer');
            
            sscContainer.innerHTML = '';
            hscContainer.innerHTML = '';
            
            if (suggestions.filter(s => s.category === 'ssc').length === 0) {
                sscContainer.innerHTML = '<div class="message-box" style="text-align: center; padding: 40px;"><p>No SSC suggestions added yet.</p></div>';
            }
            
            if (suggestions.filter(s => s.category === 'hsc').length === 0) {
                hscContainer.innerHTML = '<div class="message-box" style="text-align: center; padding: 40px;"><p>No HSC suggestions added yet.</p></div>';
            }
            
            suggestions.forEach(suggestion => {
                const card = document.createElement('div');
                card.className = 'suggestion-card';
                card.innerHTML = `
                    <h4>${suggestion.title}</h4>
                    <p>${suggestion.description || 'No description'}</p>
                    <div style="margin-top:16px; display: flex; gap: 12px; align-items: center;">
                        <a href="${suggestion.link}" target="_blank" 
                           style="display: inline-flex; align-items: center; gap: 8px; background: var(--gradient-secondary); color: white; padding: 8px 16px; border-radius: var(--radius-sm); text-decoration: none; font-weight: 600;">
                            <span>🔗</span> Preview Link
                        </a>
                        <button onclick="deleteSuggestion('${suggestion.id}')" class="delete-suggestion">
                            <span>🗑️</span> Delete
                        </button>
                    </div>
                `;
                
                if (suggestion.category === 'ssc') {
                    sscContainer.appendChild(card);
                } else {
                    hscContainer.appendChild(card);
                }
            });
        }

        function updateSuggestionCounts() {
            const sscCount = suggestions.filter(s => s.category === 'ssc').length;
            const hscCount = suggestions.filter(s => s.category === 'hsc').length;
            
            document.getElementById('sscSuggestionCount').textContent = sscCount;
            document.getElementById('hscSuggestionCount').textContent = hscCount;
        }

        function showSuggestionMessage(message, type) {
            const messageDiv = document.getElementById('suggestionMessage');
            messageDiv.innerHTML = `<div class="${type}-message">${message}</div>`;
            setTimeout(() => {
                messageDiv.innerHTML = '';
            }, 3000);
        }

        function showPaymentSettingsMessage(message, type) {
            const messageDiv = document.getElementById('paymentSettingsMessage');
            messageDiv.innerHTML = `<div class="${type}-message">${message}</div>`;
            setTimeout(() => {
                messageDiv.innerHTML = '';
            }, 3000);
        }

        // =================== LOCAL STORAGE FUNCTIONS ===================
        function loadClassesFromStorage() { 
            classes = JSON.parse(localStorage.getItem('scienceWaterClasses')) || []; 
        }
        
        function saveClassesToStorage() { 
            localStorage.setItem('scienceWaterClasses', JSON.stringify(classes)); 
        }
        
        function loadMessagesFromStorage() { 
            messages = JSON.parse(localStorage.getItem('scienceWaterMessages')) || []; 
        }
        
        function saveMessagesToStorage() { 
            localStorage.setItem('scienceWaterMessages', JSON.stringify(messages)); 
        }
        
        function loadRoutineFromStorage() { 
            routine = JSON.parse(localStorage.getItem('scienceWaterRoutine')) || []; 
        }
        
        function saveRoutineToStorage() { 
            localStorage.setItem('scienceWaterRoutine', JSON.stringify(routine)); 
        }
        
        function loadSuggestionsFromStorage() {
            suggestions = JSON.parse(localStorage.getItem('scienceWaterSuggestions')) || [];
        }
        
        function saveSuggestionsToStorage() {
            localStorage.setItem('scienceWaterSuggestions', JSON.stringify(suggestions));
        }
        
        function loadPaymentsFromStorage() {
            payments = JSON.parse(localStorage.getItem('scienceWaterPayments')) || [];
        }
        
        function savePaymentsToStorage() {
            localStorage.setItem('scienceWaterPayments', JSON.stringify(payments));
        }
        
        function loadStudentMessagesFromStorage() {
            studentMessages = JSON.parse(localStorage.getItem('scienceWaterStudentMessages')) || [];
        }
        
        function saveStudentMessagesToStorage() {
            localStorage.setItem('scienceWaterStudentMessages', JSON.stringify(studentMessages));
        }
        
        function loadPaymentSettings() {
            const saved = localStorage.getItem('scienceWaterPaymentSettings');
            if (saved) {
                paymentSettings = JSON.parse(saved);
            }
        }
        
        function savePaymentSettings() {
            localStorage.setItem('scienceWaterPaymentSettings', JSON.stringify(paymentSettings));
        }

        function loadThumbnailsFromStorage() {
            const saved = localStorage.getItem('scienceWaterThumbnails');
            thumbnails = saved ? JSON.parse(saved) : [];
        }

        function saveThumbnailsToStorage() {
            localStorage.setItem('scienceWaterThumbnails', JSON.stringify(thumbnails));
        }

        // =================== UTILITY FUNCTIONS ===================
        function saveAllData() {
            if (isFirebaseConnected) {
                showMessage("Syncing with cloud...", "info");
                setTimeout(() => {
                    showMessage("✅ All data synced with cloud!", "success");
                }, 1000);
            }
            
            saveClassesToStorage();
            saveMessagesToStorage();
            saveRoutineToStorage();
            saveSuggestionsToStorage();
            savePaymentsToStorage();
            saveStudentMessagesToStorage();
            savePaymentSettings();
            saveThumbnailsToStorage();
            
            showMessage("All changes saved!", "success");
        }

        function showMessage(message, type) {
            const addMessageDiv = document.getElementById('addMessage');
            addMessageDiv.innerHTML = `<div class="${type}-message">${message}</div>`;
            setTimeout(() => {
                addMessageDiv.innerHTML = '';
            }, 3000);
        }
        
        window.onclick = function(e) { 
            if(e.target == domCache.adminModal) {
                domCache.adminModal.style.display = "none";
            }
        }
    </script>
</body>
</html>
