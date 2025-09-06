# project_krujeen
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no">
    <meta name="theme-color" content="#667eea">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="default">
    <meta name="apple-mobile-web-app-title" content="Eazy Work">
    <meta name="mobile-web-app-capable" content="yes">
    <title>Eazy Work - Job Search Platform</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');
        
        :root {
            --primary-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --glass-bg: rgba(255, 255, 255, 0.1);
            --glass-border: rgba(255, 255, 255, 0.2);
            --shadow-light: 0 4px 16px rgba(0, 0, 0, 0.1);
            --shadow-medium: 0 8px 32px rgba(0, 0, 0, 0.15);
            --border-radius: 20px;
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        
        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: var(--primary-gradient);
            min-height: 100vh;
            margin: 0;
            padding: 0;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            overflow-x: hidden;
            font-size: 16px;
            line-height: 1.6;
        }
        
        /* Modern mobile-first design system */
        .glass-effect {
            background: var(--glass-bg);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border);
            border-radius: var(--border-radius);
        }
        
        .card-modern {
            background: white;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow-medium);
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: var(--transition);
        }
        
        .card-modern:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
        }
        
        .gradient-text {
            background: var(--primary-gradient);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-weight: 800;
        }
        
        .floating-card {
            transform: translateY(0);
            transition: var(--transition);
            will-change: transform;
        }
        
        .floating-card:active {
            transform: translateY(1px) scale(0.99);
        }
        
        @media (hover: hover) {
            .floating-card:hover {
                transform: translateY(-3px);
            }
        }
        
        .modern-button {
            background: var(--primary-gradient);
            border: none;
            border-radius: var(--border-radius);
            color: white;
            font-weight: 600;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
            box-shadow: var(--shadow-light);
        }
        
        .modern-button:active {
            transform: scale(0.98);
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        }
        
        @media (hover: hover) {
            .modern-button:hover {
                transform: translateY(-1px);
                box-shadow: 0 8px 24px rgba(102, 126, 234, 0.3);
            }
        }
        
        .status-badge {
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            padding: 6px 12px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .job-card {
            transition: all 0.3s ease;
            transform: translateY(0);
        }
        
        @media (hover: hover) {
            .job-card:hover {
                transform: translateY(-5px);
                box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
            }
        }
        
        .job-card:active {
            transform: scale(0.98);
        }
        
        .category-btn.active {
            transform: scale(1.02);
        }
        
        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .modal-enter {
            animation: modalEnter 0.3s ease-out;
        }
        
        @keyframes modalEnter {
            from { opacity: 0; transform: scale(0.9); }
            to { opacity: 1; transform: scale(1); }
        }
        
        .salary-badge {
            background: linear-gradient(45deg, #10b981, #059669);
        }
        
        /* Mobile-first responsive system */
        .container-mobile {
            padding: clamp(16px, 4vw, 24px);
            max-width: 100vw;
            overflow-x: hidden;
            margin: 0 auto;
        }
        
        @media (min-width: 768px) {
            .container-mobile {
                max-width: 768px;
            }
        }
        
        @media (min-width: 1024px) {
            .container-mobile {
                max-width: 1024px;
                padding: 32px;
            }
        }
        
        .card-spacing {
            padding: clamp(20px, 5vw, 32px);
            margin-bottom: clamp(16px, 4vw, 24px);
        }
        
        .text-mobile {
            font-size: clamp(14px, 4vw, 16px);
            line-height: 1.6;
        }
        
        .text-mobile-lg {
            font-size: clamp(16px, 4.5vw, 18px);
            line-height: 1.5;
            font-weight: 600;
        }
        
        .text-mobile-xl {
            font-size: clamp(24px, 6vw, 32px);
            line-height: 1.3;
            font-weight: 800;
        }
        
        .button-mobile {
            min-height: clamp(48px, 12vw, 56px);
            font-size: clamp(14px, 4vw, 16px);
            padding: clamp(12px, 3vw, 16px) clamp(20px, 5vw, 24px);
            border-radius: var(--border-radius);
            font-weight: 600;
            width: 100%;
            margin-bottom: clamp(8px, 2vw, 12px);
            transition: var(--transition);
            border: none;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .input-mobile {
            font-size: 16px; /* Fixed at 16px to prevent zoom on iOS */
            min-height: clamp(48px, 12vw, 56px);
            padding: clamp(12px, 3vw, 16px);
            border-radius: var(--border-radius);
            border: 2px solid #e5e7eb;
            transition: var(--transition);
            width: 100%;
            background: white;
            -webkit-appearance: none;
            appearance: none;
        }
        
        .input-mobile:focus {
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
            outline: none;
        }
        
        .modal-mobile {
            border-radius: var(--border-radius) var(--border-radius) 0 0;
            max-height: 95vh;
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
            overscroll-behavior: contain;
        }
        
        @media (min-width: 768px) {
            .modal-mobile {
                border-radius: var(--border-radius);
                max-height: 90vh;
                max-width: 600px;
                margin: auto;
            }
        }
        
        .grid-mobile {
            display: grid;
            grid-template-columns: 1fr;
            gap: clamp(12px, 3vw, 16px);
        }
        
        @media (min-width: 640px) {
            .grid-mobile-sm {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        
        .flex-mobile {
            display: flex;
            flex-direction: column;
            gap: clamp(8px, 2vw, 12px);
        }
        
        .icon-mobile {
            font-size: clamp(20px, 5vw, 24px);
            width: clamp(40px, 10vw, 48px);
            height: clamp(40px, 10vw, 48px);
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 12px;
            background: rgba(102, 126, 234, 0.1);
            flex-shrink: 0;
        }
        
        /* Modern animations */
        .slide-up {
            animation: slideUp 0.3s cubic-bezier(0.4, 0, 0.2, 1);
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
        
        .pulse-effect {
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.8;
            }
        }
        
        /* Modern touch interactions */
        @media (hover: none) and (pointer: coarse) {
            button, .touch-target {
                min-height: 48px;
                min-width: 48px;
                padding: clamp(12px, 3vw, 16px) clamp(20px, 5vw, 24px);
            }
            
            .job-card, .floating-card {
                padding: clamp(20px, 5vw, 32px) !important;
                margin-bottom: clamp(16px, 4vw, 24px) !important;
            }
            
            input, select, textarea {
                min-height: 48px;
                padding: clamp(12px, 3vw, 16px);
                font-size: 16px; /* Prevent zoom on iOS */
            }
        }
        
        /* Enhanced touch feedback */
        .touch-ripple {
            position: relative;
            overflow: hidden;
        }
        
        .touch-ripple::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.3);
            transform: translate(-50%, -50%);
            transition: width 0.3s ease, height 0.3s ease;
            pointer-events: none;
        }
        
        .touch-ripple:active::after {
            width: 200px;
            height: 200px;
        }
        
        /* Smooth scrolling for all elements */
        * {
            scroll-behavior: smooth;
            -webkit-overflow-scrolling: touch;
        }
        
        /* Enhanced scrollable areas */
        .scrollable {
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
            scroll-behavior: smooth;
        }
        
        /* Custom scrollbar for webkit browsers */
        .scrollable::-webkit-scrollbar {
            width: 6px;
        }
        
        .scrollable::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.1);
            border-radius: 3px;
        }
        
        .scrollable::-webkit-scrollbar-thumb {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 3px;
        }
        
        .scrollable::-webkit-scrollbar-thumb:hover {
            background: rgba(0, 0, 0, 0.5);
        }
        
        /* Enhanced touch-friendly interactions */
        .touch-target {
            min-height: 56px;
            min-width: 56px;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            cursor: pointer;
        }
        
        /* Touch feedback */
        .touch-feedback {
            position: relative;
            overflow: hidden;
        }
        
        .touch-feedback::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.3);
            transform: translate(-50%, -50%);
            transition: width 0.3s, height 0.3s;
            pointer-events: none;
        }
        
        .touch-feedback:active::before {
            width: 200px;
            height: 200px;
        }
        
        /* Modern safe area and user interaction */
        .safe-area-top {
            padding-top: env(safe-area-inset-top);
        }
        
        .safe-area-bottom {
            padding-bottom: env(safe-area-inset-bottom);
        }
        
        .safe-area-left {
            padding-left: env(safe-area-inset-left);
        }
        
        .safe-area-right {
            padding-right: env(safe-area-inset-right);
        }
        
        /* Prevent text selection on interactive elements */
        button, .touch-target, .job-card, .floating-card {
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }
        
        /* Enhanced button states for touch */
        button:active, .touch-target:active {
            transform: scale(0.95);
            transition: transform 0.1s ease;
        }
        
        /* Better focus states for accessibility */
        button:focus, input:focus, select:focus, textarea:focus {
            outline: 3px solid #4F46E5;
            outline-offset: 2px;
        }
        
        /* Larger tap areas for small elements */
        .tap-area {
            position: relative;
        }
        
        .tap-area::after {
            content: '';
            position: absolute;
            top: -12px;
            left: -12px;
            right: -12px;
            bottom: -12px;
            z-index: 1;
        }
    </style>
</head>
<body>
    <div class="min-h-screen safe-area-top safe-area-bottom">
        <div class="container-mobile safe-area-left safe-area-right">
            <!-- Modern Header -->
            <div class="text-center mb-8">
                <div class="slide-up">
                    <h1 class="text-mobile-xl gradient-text mb-2">💼 Eazy Work</h1>
                    <p class="text-white/90 text-mobile mb-8">แพลตฟอร์มหางานยุคใหม่</p>
                </div>
                
                <!-- Modern Mode Toggle -->
                <div class="glass-effect p-4 mb-8 slide-up">
                    <div class="grid grid-cols-2 gap-3">
                        <button id="job-seeker-btn" onclick="switchMode('job-seeker')" class="mode-btn active button-mobile modern-button touch-ripple">
                            <span class="text-xl">🔍</span>
                            <span class="text-mobile-lg">หางาน</span>
                        </button>
                        <button id="employer-btn" onclick="switchMode('employer')" class="mode-btn button-mobile bg-white/20 text-white border-2 border-white/30 touch-ripple">
                            <span class="text-xl">👥</span>
                            <span class="text-mobile-lg">หาพนักงาน</span>
                        </button>
                    </div>
                </div>
                
                <div id="action-buttons" class="slide-up">
                    <div class="card-modern p-4 text-center">
                        <p class="text-gray-600 text-mobile">ค้นหาโอกาสใหม่ที่รอคุณอยู่</p>
                    </div>
                </div>
            </div>

            <!-- Modern Category Filter -->
            <div class="card-modern card-spacing mb-6 slide-up" id="category-filter">
                <div class="flex items-center gap-3 mb-6">
                    <div class="icon-mobile">🏷️</div>
                    <h2 class="text-mobile-lg text-gray-800">กรองตามประเภท</h2>
                </div>
                <div class="grid-mobile">
                    <button onclick="filterByCategory('all')" class="category-btn active modern-button button-mobile touch-ripple">
                        <span class="text-xl">🌟</span>
                        <span class="text-mobile-lg">ทั้งหมด</span>
                    </button>
                    <button onclick="filterByCategory('permanent')" class="category-btn button-mobile bg-gray-100 text-gray-700 border-2 border-gray-200 touch-ripple">
                        <span class="text-xl">👔</span>
                        <span class="text-mobile-lg">พนักงานประจำ</span>
                    </button>
                    <button onclick="filterByCategory('freelance')" class="category-btn button-mobile bg-gray-100 text-gray-700 border-2 border-gray-200 touch-ripple">
                        <span class="text-xl">💼</span>
                        <span class="text-mobile-lg">ฟรีแลนซ์</span>
                    </button>
                </div>
            </div>

            <!-- Modern Jobs Grid -->
            <div id="jobs-grid" class="grid-mobile">
                <!-- Job cards will be populated by JavaScript -->
            </div>

            <!-- Modern No Results -->
            <div id="no-results" class="hidden card-modern card-spacing text-center slide-up">
                <div class="text-6xl mb-4 pulse-effect">🔍</div>
                <h3 class="text-mobile-lg text-gray-700 mb-2">ไม่พบข้อมูลในประเภทนี้</h3>
                <p class="text-mobile text-gray-500">ลองเลือกประเภทอื่นหรือดูทั้งหมด</p>
            </div>
        </div>
    </div>

    <!-- Modern Job Detail Modal -->
    <div id="detail-modal" class="hidden fixed inset-0 bg-black/60 backdrop-blur-sm z-50 flex items-end justify-center safe-area-bottom">
        <div class="card-modern modal-mobile w-full slide-up">
            <div id="modal-content">
                <!-- Modal content will be populated by JavaScript -->
            </div>
        </div>
    </div>

    <!-- Modern Add/Edit Job Modal -->
    <div id="edit-modal" class="hidden fixed inset-0 bg-black/60 backdrop-blur-sm z-50 flex items-end justify-center safe-area-bottom">
        <div class="card-modern modal-mobile w-full slide-up">
            <div class="card-spacing">
                <!-- Modern handle bar -->
                <div class="w-12 h-1.5 bg-gray-300 rounded-full mx-auto mb-6"></div>
                
                <div class="flex justify-between items-center mb-8">
                    <div class="flex items-center gap-3">
                        <div class="icon-mobile">✨</div>
                        <h2 id="modal-title" class="text-mobile-lg text-gray-900">เพิ่มตำแหน่งงานใหม่</h2>
                    </div>
                    <button onclick="closeEditModal()" class="w-12 h-12 flex items-center justify-center rounded-full bg-gray-100 text-gray-500 text-2xl">×</button>
                </div>
                
                <form id="job-form" onsubmit="saveJob(event)">
                    <div class="grid-mobile">
                        <div>
                            <label class="block text-mobile font-semibold text-gray-700 mb-3">ตำแหน่งงาน</label>
                            <input type="text" id="job-title" required class="input-mobile w-full">
                        </div>
                        
                        <div>
                            <label class="block text-mobile font-semibold text-gray-700 mb-3">บริษัท</label>
                            <input type="text" id="job-company" required class="input-mobile w-full">
                        </div>
                        
                        <div>
                            <label class="block text-mobile font-semibold text-gray-700 mb-3">ประเภทงาน</label>
                            <select id="job-category" required class="input-mobile w-full">
                                <option value="permanent">👔 พนักงานประจำ</option>
                                <option value="freelance">💼 ฟรีแลนซ์</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-mobile font-semibold text-gray-700 mb-3">สถานที่ทำงาน</label>
                            <input type="text" id="job-location" required class="input-mobile w-full">
                        </div>
                        
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="block text-mobile font-semibold text-gray-700 mb-3">เงินเดือนขั้นต่ำ</label>
                                <input type="number" id="job-salary-min" min="0" required class="input-mobile w-full">
                            </div>
                            <div>
                                <label class="block text-mobile font-semibold text-gray-700 mb-3">เงินเดือนสูงสุด</label>
                                <input type="number" id="job-salary-max" min="0" required class="input-mobile w-full">
                            </div>
                        </div>
                        
                        <div>
                            <label class="block text-mobile font-semibold text-gray-700 mb-3">ประเภทการจ้างงาน</label>
                            <select id="job-type" required class="input-mobile w-full">
                                <option value="full-time">เต็มเวลา</option>
                                <option value="part-time">พาร์ทไทม์</option>
                                <option value="contract">สัญญาจ้าง</option>
                                <option value="freelance">ฟรีแลนซ์</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-mobile font-semibold text-gray-700 mb-3">รายละเอียดงาน</label>
                            <textarea id="job-description" rows="4" class="input-mobile w-full resize-none"></textarea>
                        </div>
                        
                        <div>
                            <label class="block text-mobile font-semibold text-gray-700 mb-3">ประสบการณ์ที่ต้องการ (ปี)</label>
                            <input type="number" id="job-experience" min="0" required class="input-mobile w-full">
                        </div>
                    </div>
                    
                    <div class="flex-mobile mt-8">
                        <button type="submit" class="modern-button button-mobile touch-ripple">
                            <span class="text-xl">💾</span>
                            <span class="text-mobile-lg">บันทึก</span>
                        </button>
                        <button type="button" onclick="closeEditModal()" class="button-mobile bg-gray-200 text-gray-700 border-2 border-gray-300 touch-ripple">
                            <span class="text-xl">❌</span>
                            <span class="text-mobile-lg">ยกเลิก</span>
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <script>
        // Sample jobs data
        let jobs = [
            {
                id: 1,
                title: "พนักงานบัญชี",
                company: "ABC Accounting Co.",
                category: "permanent",
                location: "กรุงเทพฯ (ออนไซต์)",
                salaryMin: 25000,
                salaryMax: 35000,
                type: "full-time",
                description: "จัดทำบัญชี ตรวจสอบเอกสาร และจัดทำงบการเงิน",
                experience: 2,
                applications: 7,
                posted: "2024-01-26"
            },
            {
                id: 2,
                title: "พนักงานขาย",
                company: "Sales Pro Ltd.",
                category: "permanent",
                location: "กรุงเทพฯ (ออนไซต์)",
                salaryMin: 20000,
                salaryMax: 30000,
                type: "full-time",
                description: "ขายสินค้าและบริการ ดูแลลูกค้า และขยายฐานลูกค้าใหม่",
                experience: 1,
                applications: 12,
                posted: "2024-01-25"
            },
            {
                id: 3,
                title: "เจ้าหน้าที่ HR",
                company: "Human Resources Co.",
                category: "permanent",
                location: "กรุงเทพฯ (ไฮบริด)",
                salaryMin: 28000,
                salaryMax: 40000,
                type: "full-time",
                description: "จัดหาบุคลากร สัมภาษณ์งาน และดูแลเรื่องสวัสดิการพนักงาน",
                experience: 2,
                applications: 15,
                posted: "2024-01-24"
            },
            {
                id: 4,
                title: "นักเขียนคอนเทนต์",
                company: "Creative Agency",
                category: "freelance",
                location: "รีโมทเวิร์ค",
                salaryMin: 15000,
                salaryMax: 25000,
                type: "freelance",
                description: "เขียนคอนเทนต์สำหรับโซเชียลมีเดีย บล็อก และเว็บไซต์",
                experience: 1,
                applications: 14,
                posted: "2024-01-27"
            },
            {
                id: 5,
                title: "นักแปลภาษา",
                company: "Translation Services",
                category: "freelance",
                location: "รีโมทเวิร์ค",
                salaryMin: 300,
                salaryMax: 500,
                type: "freelance",
                description: "แปลเอกสารและบทความจากภาษาอังกฤษเป็นภาษาไทย",
                experience: 2,
                applications: 8,
                posted: "2024-01-28"
            },
            {
                id: 6,
                title: "นักออกแบบกราฟิก",
                company: "Design Studio",
                category: "freelance",
                location: "รีโมทเวิร์ค",
                salaryMin: 20000,
                salaryMax: 35000,
                type: "freelance",
                description: "ออกแบบโลโก้ โบรชัวร์ และสื่อการตลาดต่างๆ",
                experience: 3,
                applications: 11,
                posted: "2024-01-26"
            }
        ];

        // Sample companies data for job seeker mode
        let companies = [
            {
                id: 1,
                name: "ABC Accounting Co.",
                industry: "บัญชีและการเงิน",
                category: "permanent",
                location: "กรุงเทพฯ",
                employees: "50-100 คน",
                description: "บริษัทที่ปรึกษาด้านบัญชีและการเงินชั้นนำ มีประสบการณ์กว่า 15 ปี",
                benefits: ["ประกันสุขภาพ", "โบนัสประจำปี", "วันหยุดพิเศษ", "อบรมพัฒนาทักษะ"],
                openPositions: 3,
                rating: 4.5,
                logo: "🏢",
                website: "www.abc-accounting.com",
                founded: "2008",
                culture: "เน้นการทำงานเป็นทีม สภาพแวดล้อมที่เป็นมิตร"
            },
            {
                id: 2,
                name: "Sales Pro Ltd.",
                industry: "การขายและการตลาด",
                category: "permanent",
                location: "กรุงเทพฯ",
                employees: "100-200 คน",
                description: "บริษัทชั้นนำด้านการขายและการตลาด มีเครือข่ายลูกค้าทั่วประเทศ",
                benefits: ["คอมมิชชั่นสูง", "รถประจำตำแหน่ง", "ประกันชีวิต", "ท่องเที่ยวประจำปี"],
                openPositions: 5,
                rating: 4.3,
                logo: "📈",
                website: "www.salespro.co.th",
                founded: "2010",
                culture: "มุ่งเน้นผลงาน สนับสนุนการเติบโต"
            },
            {
                id: 3,
                name: "Human Resources Co.",
                industry: "ทรัพยากรบุคคล",
                category: "permanent",
                location: "กรุงเทพฯ",
                employees: "30-50 คน",
                description: "ผู้เชี่ยวชาญด้านการจัดหาบุคลากรและพัฒนาองค์กร",
                benefits: ["Work-Life Balance", "ประกันสุขภาพครอบครัว", "ลาพักร้อน", "โบนัสผลงาน"],
                openPositions: 2,
                rating: 4.7,
                logo: "👥",
                website: "www.hr-solutions.com",
                founded: "2012",
                culture: "ใส่ใจพนักงาน สร้างสรรค์นวัตกรรม"
            },
            {
                id: 4,
                name: "Creative Agency",
                industry: "สื่อและการสื่อสาร",
                category: "freelance",
                location: "กรุงเทพฯ",
                employees: "20-30 คน",
                description: "เอเจนซี่สร้างสรรค์ที่ทำงานกับแบรนด์ชั้นนำมากมาย",
                benefits: ["ชั่วโมงทำงานยืดหยุ่น", "พื้นที่ทำงานสร้างสรรค์", "อุปกรณ์ทันสมัย", "โปรเจกต์หลากหลาย"],
                openPositions: 4,
                rating: 4.6,
                logo: "🎨",
                website: "www.creative-agency.co.th",
                founded: "2015",
                culture: "เสรีภาพในการสร้างสรรค์ ทีมเวิร์คที่แข็งแกร่ง"
            },
            {
                id: 5,
                name: "Translation Services",
                industry: "บริการแปลภาษา",
                category: "freelance",
                location: "รีโมทเวิร์ค",
                employees: "10-20 คน",
                description: "ผู้ให้บริการแปลภาษามืออาชีพ รองรับหลายภาษา",
                benefits: ["ทำงานจากที่ไหนก็ได้", "อัตราค่าแปลสูง", "โปรเจกต์น่าสนใจ", "ความยืดหยุ่นสูง"],
                openPositions: 3,
                rating: 4.4,
                logo: "🌐",
                website: "www.translation-pro.com",
                founded: "2013",
                culture: "ความแม่นยำ การเรียนรู้ตลอดชีวิต"
            },
            {
                id: 6,
                name: "Design Studio",
                industry: "ออกแบบและศิลปะ",
                category: "freelance",
                location: "กรุงเทพฯ",
                employees: "15-25 คน",
                description: "สตูดิโอออกแบบที่มีผลงานระดับสากล เชี่ยวชาญด้าน UI/UX",
                benefits: ["สภาพแวดล้อมสร้างสรรค์", "เทคโนโลยีล้ำสมัย", "โปรเจกต์ระดับโลก", "การพัฒนาทักษะ"],
                openPositions: 2,
                rating: 4.8,
                logo: "✨",
                website: "www.design-studio.co.th",
                founded: "2016",
                culture: "นวัตกรรม ความเป็นเลิศ การทำงานร่วมกัน"
            }
        ];

        // Sample people data for employer mode
        let people = [
            {
                id: 1,
                name: "สมชาย ใจดี",
                age: 28,
                position: "นักบัญชี",
                experience: 3,
                location: "กรุงเทพฯ",
                education: "ปริญญาตรี บัญชี",
                skills: ["Excel", "SAP", "การจัดทำงบการเงิน", "ภาษีอากร"],
                expectedSalary: "30,000-40,000",
                workType: "full-time",
                description: "มีประสบการณ์ในการจัดทำบัญชีและงบการเงิน ชำนาญในการใช้โปรแกรม SAP และ Excel",
                available: true,
                rating: 4.8,
                projects: 12,
                avatar: "👨‍💼"
            },
            {
                id: 2,
                name: "สุดา รักงาน",
                age: 25,
                position: "นักขาย",
                experience: 2,
                location: "กรุงเทพฯ",
                education: "ปริญญาตรี การตลาด",
                skills: ["การขาย", "การนำเสนอ", "CRM", "การเจรจาต่อรอง"],
                expectedSalary: "25,000-35,000",
                workType: "full-time",
                description: "มีทักษะการขายที่ดี สามารถปิดการขายได้เกินเป้าหมาย มีประสบการณ์ในการดูแลลูกค้า",
                available: true,
                rating: 4.6,
                projects: 8,
                avatar: "👩‍💼"
            },
            {
                id: 3,
                name: "วิชัย เก่งงาน",
                age: 32,
                position: "เจ้าหน้าที่ HR",
                experience: 5,
                location: "กรุงเทพฯ",
                education: "ปริญญาโท จิตวิทยาอุตสาหกรรม",
                skills: ["สัมภาษณ์งาน", "การจัดหาบุคลากร", "HR Analytics", "การฝึกอบรม"],
                expectedSalary: "35,000-45,000",
                workType: "full-time",
                description: "ผู้เชี่ยวชาญด้าน HR มีประสบการณ์ในการจัดหาบุคลากรและพัฒนาทีม",
                available: false,
                rating: 4.9,
                projects: 15,
                avatar: "👨‍💻"
            },
            {
                id: 4,
                name: "นิดา สร้างสรรค์",
                age: 26,
                position: "นักเขียนคอนเทนต์",
                experience: 2,
                location: "รีโมทเวิร์ค",
                education: "ปริญญาตรี นิเทศศาสตร์",
                skills: ["การเขียน", "SEO", "Social Media", "Content Strategy"],
                expectedSalary: "20,000-30,000",
                workType: "freelance",
                description: "นักเขียนคอนเทนต์ที่มีความคิดสร้างสรรค์ เชี่ยวชาญด้าน SEO และ Social Media",
                available: true,
                rating: 4.7,
                projects: 25,
                avatar: "👩‍🎨"
            },
            {
                id: 5,
                name: "ประยุทธ แปลดี",
                age: 30,
                position: "นักแปลภาษา",
                experience: 4,
                location: "รีโมทเวิร์ค",
                education: "ปริญญาโท ภาษาอังกฤษ",
                skills: ["แปลภาษา", "ล่าม", "การเขียนเทคนิค", "ภาษาญี่ปุ่น"],
                expectedSalary: "400-600 บาท/ชั่วโมง",
                workType: "freelance",
                description: "นักแปลมืออาชีพ สามารถแปลเอกสารทางเทคนิคและทางธุรกิจได้อย่างแม่นยำ",
                available: true,
                rating: 4.9,
                projects: 45,
                avatar: "👨‍🏫"
            },
            {
                id: 6,
                name: "กมลา ออกแบบ",
                age: 27,
                position: "นักออกแบบกราฟิก",
                experience: 3,
                location: "รีโมทเวิร์ค",
                education: "ปริญญาตรี ศิลปกรรม",
                skills: ["Photoshop", "Illustrator", "Branding", "UI/UX Design"],
                expectedSalary: "25,000-40,000",
                workType: "freelance",
                description: "นักออกแบบกราฟิกที่มีความเชี่ยวชาญในการสร้างแบรนด์และการออกแบบ UI/UX",
                available: true,
                rating: 4.8,
                projects: 32,
                avatar: "👩‍🎨"
            }
        ];

        let currentFilter = 'all';
        let editingId = null;
        let currentMode = 'job-seeker'; // 'job-seeker' or 'employer'

        // Category icons and names
        const categoryInfo = {
            permanent: { icon: '👔', name: 'พนักงานประจำ' },
            freelance: { icon: '💼', name: 'ฟรีแลนซ์' }
        };

        const jobTypeNames = {
            'full-time': 'เต็มเวลา',
            'part-time': 'พาร์ทไทม์',
            'contract': 'สัญญาจ้าง',
            'freelance': 'ฟรีแลนซ์'
        };

        // Initialize the app with modern features
        document.addEventListener('DOMContentLoaded', function() {
            renderJobs();
            updateModeUI();
            initializeScrolling();
            initializeTouchGestures();
            initializeModernFeatures();
        });

        // Initialize modern web features
        function initializeModernFeatures() {
            // Register service worker for PWA capabilities
            if ('serviceWorker' in navigator) {
                navigator.serviceWorker.register('/sw.js').catch(() => {
                    // Service worker registration failed, but app still works
                });
            }
            
            // Add visual viewport support
            if (window.visualViewport) {
                window.visualViewport.addEventListener('resize', handleViewportResize);
            }
            
            // Add intersection observer for animations
            if ('IntersectionObserver' in window) {
                const observer = new IntersectionObserver((entries) => {
                    entries.forEach(entry => {
                        if (entry.isIntersecting) {
                            entry.target.classList.add('fade-in');
                        }
                    });
                });
                
                document.querySelectorAll('.slide-up').forEach(el => {
                    observer.observe(el);
                });
            }
        }

        // Handle viewport resize for mobile keyboards
        function handleViewportResize() {
            const vh = window.visualViewport.height * 0.01;
            document.documentElement.style.setProperty('--vh', `${vh}px`);
        }

        // Initialize smooth scrolling and scroll indicators
        function initializeScrolling() {
            // Add scroll event listeners for better UX
            const scrollableElements = document.querySelectorAll('.scrollable');
            
            scrollableElements.forEach(element => {
                element.addEventListener('scroll', function() {
                    // Add visual feedback for scrolling
                    this.style.scrollBehavior = 'smooth';
                });
                
                // Enable momentum scrolling on iOS
                element.style.webkitOverflowScrolling = 'touch';
            });
            
            // Smooth scroll to top function
            window.scrollToTop = function() {
                window.scrollTo({
                    top: 0,
                    behavior: 'smooth'
                });
            };
        }

        // Initialize touch gestures
        function initializeTouchGestures() {
            let startY = 0;
            let startX = 0;
            
            // Add pull-to-refresh gesture
            document.addEventListener('touchstart', function(e) {
                startY = e.touches[0].clientY;
                startX = e.touches[0].clientX;
            }, { passive: true });
            
            document.addEventListener('touchmove', function(e) {
                const currentY = e.touches[0].clientY;
                const currentX = e.touches[0].clientX;
                const diffY = currentY - startY;
                const diffX = currentX - startX;
                
                // Prevent default scrolling when swiping horizontally on modals
                if (Math.abs(diffX) > Math.abs(diffY) && Math.abs(diffX) > 50) {
                    const modal = document.getElementById('detail-modal');
                    if (!modal.classList.contains('hidden')) {
                        // Swipe right to close modal
                        if (diffX > 100) {
                            closeDetailModal();
                        }
                    }
                }
            }, { passive: true });
            
            // Add haptic feedback for supported devices
            window.addHapticFeedback = function() {
                if (navigator.vibrate) {
                    navigator.vibrate(10); // Short vibration
                }
            };
            
            // Enhanced touch feedback for buttons
            document.addEventListener('touchstart', function(e) {
                if (e.target.tagName === 'BUTTON' || e.target.closest('button')) {
                    const button = e.target.tagName === 'BUTTON' ? e.target : e.target.closest('button');
                    button.style.transform = 'scale(0.95)';
                    
                    // Add haptic feedback
                    if (navigator.vibrate) {
                        navigator.vibrate(5);
                    }
                }
            }, { passive: true });
            
            document.addEventListener('touchend', function(e) {
                if (e.target.tagName === 'BUTTON' || e.target.closest('button')) {
                    const button = e.target.tagName === 'BUTTON' ? e.target : e.target.closest('button');
                    setTimeout(() => {
                        button.style.transform = 'scale(1)';
                    }, 100);
                }
            }, { passive: true });
        }

        // Switch between job seeker and employer modes
        function switchMode(mode) {
            currentMode = mode;
            currentFilter = 'all'; // Reset filter when switching modes
            
            // Update button states with modern styling
            document.querySelectorAll('.mode-btn').forEach(btn => {
                btn.classList.remove('active', 'modern-button');
                btn.classList.add('bg-white/20', 'text-white', 'border-2', 'border-white/30');
            });
            
            const activeBtn = document.getElementById(mode + '-btn');
            activeBtn.classList.add('active', 'modern-button');
            activeBtn.classList.remove('bg-white/20', 'text-white', 'border-2', 'border-white/30');
            
            updateModeUI();
        }

        // Update UI based on current mode
        function updateModeUI() {
            const actionButtons = document.getElementById('action-buttons');
            const categoryFilter = document.getElementById('category-filter');
            
            if (currentMode === 'job-seeker') {
                // Job seeker mode - show companies
                actionButtons.innerHTML = `
                    <div class="card-modern p-4 text-center">
                        <p class="text-gray-600 text-mobile">ค้นหาบริษัทที่น่าสนใจสำหรับคุณ</p>
                    </div>
                `;
                categoryFilter.style.display = 'block';
                renderCompanies();
            } else {
                // Employer mode - show people
                actionButtons.innerHTML = `
                    <div class="card-modern p-4 text-center">
                        <p class="text-gray-600 text-mobile">ค้นหาบุคลากรที่เหมาะสมกับองค์กรของคุณ</p>
                    </div>
                `;
                // Show category filter for employer mode too, but with different options
                categoryFilter.style.display = 'block';
                updateEmployerCategoryFilter();
                renderPeople();
            }
        }

        // Update employer category filter
        function updateEmployerCategoryFilter() {
            const categoryFilter = document.getElementById('category-filter');
            
            categoryFilter.innerHTML = `
                <div class="flex items-center gap-3 mb-6">
                    <div class="icon-mobile">👥</div>
                    <h2 class="text-mobile-lg text-gray-800">กรองตามประเภท</h2>
                </div>
                <div class="grid-mobile">
                    <button onclick="filterPeopleByCategory('all')" class="category-btn active modern-button button-mobile">
                        <div class="flex items-center justify-center gap-3">
                            <span class="text-xl">🌟</span>
                            <span class="text-mobile-lg">ทั้งหมด</span>
                        </div>
                    </button>
                    <button onclick="filterPeopleByCategory('available')" class="category-btn button-mobile bg-gray-100 text-gray-700 border-2 border-gray-200">
                        <div class="flex items-center justify-center gap-3">
                            <span class="text-xl">✅</span>
                            <span class="text-mobile-lg">พร้อมทำงาน</span>
                        </div>
                    </button>
                    <button onclick="filterPeopleByCategory('experience')" class="category-btn button-mobile bg-gray-100 text-gray-700 border-2 border-gray-200">
                        <div class="flex items-center justify-center gap-3">
                            <span class="text-xl">⭐</span>
                            <span class="text-mobile-lg">ประสบการณ์สูง</span>
                        </div>
                    </button>
                    <button onclick="filterPeopleByCategory('freelance')" class="category-btn button-mobile bg-gray-100 text-gray-700 border-2 border-gray-200">
                        <div class="flex items-center justify-center gap-3">
                            <span class="text-xl">💼</span>
                            <span class="text-mobile-lg">ฟรีแลนซ์</span>
                        </div>
                    </button>
                </div>
            `;
        }

        // Filter people by category
        function filterPeopleByCategory(category) {
            currentFilter = category;
            
            // Update active button with modern styling
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('active', 'modern-button');
                btn.classList.add('bg-gray-100', 'text-gray-700', 'border-2', 'border-gray-200');
            });
            
            event.target.classList.add('active', 'modern-button');
            event.target.classList.remove('bg-gray-100', 'text-gray-700', 'border-2', 'border-gray-200');
            
            renderPeople();
        }

        // Filter jobs by category (for job seeker mode)
        function filterByCategory(category) {
            currentFilter = category;
            
            // Update active button with modern styling
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('active', 'modern-button');
                btn.classList.add('bg-gray-100', 'text-gray-700', 'border-2', 'border-gray-200');
            });
            
            event.target.classList.add('active', 'modern-button');
            event.target.classList.remove('bg-gray-100', 'text-gray-700', 'border-2', 'border-gray-200');
            
            renderJobs();
        }

        // Render companies for job seeker mode
        function renderCompanies() {
            const grid = document.getElementById('jobs-grid');
            const noResults = document.getElementById('no-results');
            
            let filteredCompanies = companies;
            if (currentFilter !== 'all') {
                filteredCompanies = companies.filter(company => company.category === currentFilter);
            }
            
            if (filteredCompanies.length === 0) {
                grid.innerHTML = '';
                noResults.classList.remove('hidden');
                return;
            }
            
            noResults.classList.add('hidden');
            
            grid.innerHTML = filteredCompanies.map(company => {
                const categoryData = categoryInfo[company.category];
                const stars = '⭐'.repeat(Math.floor(company.rating));
                
                return `
                    <div class="card-modern card-spacing floating-card slide-up">
                        <div class="flex items-start gap-4 mb-6">
                            <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-indigo-100 to-purple-100 flex items-center justify-center text-2xl flex-shrink-0">
                                ${company.logo}
                            </div>
                            <div class="flex-1 min-w-0">
                                <h3 class="text-mobile-lg text-gray-900 mb-1">${company.name}</h3>
                                <p class="text-mobile text-gray-600 mb-3">${company.industry}</p>
                                <div class="flex items-center gap-2 text-sm text-gray-500">
                                    <span>${stars}</span>
                                    <span>•</span>
                                    <span>ก่อตั้ง ${company.founded}</span>
                                </div>
                            </div>
                        </div>
                        
                        <div class="flex flex-wrap gap-2 mb-6">
                            <span class="status-badge bg-indigo-100 text-indigo-700">
                                ${categoryData.name}
                            </span>
                            <span class="status-badge bg-green-100 text-green-700">
                                ${company.openPositions} ตำแหน่งเปิด
                            </span>
                        </div>
                        
                        <div class="grid-mobile mb-6">
                            <div class="flex items-center gap-3 text-mobile text-gray-600">
                                <div class="w-8 h-8 rounded-lg bg-gray-100 flex items-center justify-center">📍</div>
                                <span>${company.location}</span>
                            </div>
                            <div class="flex items-center gap-3 text-mobile text-gray-600">
                                <div class="w-8 h-8 rounded-lg bg-gray-100 flex items-center justify-center">👥</div>
                                <span>${company.employees}</span>
                            </div>
                        </div>
                        
                        <p class="text-mobile text-gray-700 mb-6 line-clamp-2">${company.description}</p>
                        
                        <div class="flex-mobile">
                            <button onclick="viewCompanyDetails(${company.id})" class="modern-button button-mobile">
                                <div class="flex items-center justify-center gap-2">
                                    <span class="text-xl">🏢</span>
                                    <span class="text-mobile-lg">ดูรายละเอียด</span>
                                </div>
                            </button>
                            <button onclick="viewCompanyJobs(${company.id})" class="button-mobile bg-green-500 text-white border-2 border-green-500">
                                <div class="flex items-center justify-center gap-2">
                                    <span class="text-xl">💼</span>
                                    <span class="text-mobile-lg">ดูตำแหน่งงาน (${company.openPositions})</span>
                                </div>
                            </button>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // Render jobs based on current filter (for backward compatibility)
        function renderJobs() {
            if (currentMode === 'job-seeker') {
                renderCompanies();
            } else {
                renderPeople();
            }
        }

        // Render people for employer mode
        function renderPeople() {
            const grid = document.getElementById('jobs-grid');
            const noResults = document.getElementById('no-results');
            
            let filteredPeople = people;
            
            // Apply filters
            if (currentFilter === 'available') {
                filteredPeople = people.filter(person => person.available);
            } else if (currentFilter === 'experience') {
                filteredPeople = people.filter(person => person.experience >= 3);
            } else if (currentFilter === 'freelance') {
                filteredPeople = people.filter(person => person.workType === 'freelance');
            }
            
            if (filteredPeople.length === 0) {
                grid.innerHTML = '';
                noResults.classList.remove('hidden');
                return;
            }
            
            noResults.classList.add('hidden');
            
            grid.innerHTML = filteredPeople.map(person => {
                const stars = '⭐'.repeat(Math.floor(person.rating));
                const availabilityBadge = person.available ? 
                    'status-badge bg-green-100 text-green-700' :
                    'status-badge bg-red-100 text-red-700';
                const availabilityText = person.available ? 'พร้อมทำงาน' : 'ไม่ว่าง';
                
                return `
                    <div class="card-modern card-spacing floating-card slide-up">
                        <div class="flex items-start gap-4 mb-6">
                            <div class="w-16 h-16 rounded-2xl bg-gradient-to-br from-blue-100 to-indigo-100 flex items-center justify-center text-2xl flex-shrink-0">
                                ${person.avatar}
                            </div>
                            <div class="flex-1 min-w-0">
                                <h3 class="text-mobile-lg text-gray-900 mb-1">${person.name}</h3>
                                <p class="text-mobile text-gray-600 mb-3">${person.position} • ${person.age} ปี</p>
                                <div class="flex items-center gap-2 text-sm text-gray-500">
                                    <span>${stars}</span>
                                    <span>•</span>
                                    <span>${person.projects} โปรเจกต์</span>
                                </div>
                            </div>
                        </div>
                        
                        <div class="flex flex-wrap gap-2 mb-6">
                            <span class="${availabilityBadge}">
                                ${availabilityText}
                            </span>
                            <span class="status-badge bg-blue-100 text-blue-700">
                                ${person.experience} ปี ประสบการณ์
                            </span>
                        </div>
                        
                        <div class="grid-mobile mb-6">
                            <div class="flex items-center gap-3 text-mobile text-gray-600">
                                <div class="w-8 h-8 rounded-lg bg-gray-100 flex items-center justify-center">📍</div>
                                <span>${person.location}</span>
                            </div>
                            <div class="flex items-center gap-3 text-mobile text-gray-600">
                                <div class="w-8 h-8 rounded-lg bg-green-100 flex items-center justify-center">💰</div>
                                <span class="font-semibold text-green-600">${person.expectedSalary} บาท</span>
                            </div>
                            <div class="flex items-center gap-3 text-mobile text-gray-600">
                                <div class="w-8 h-8 rounded-lg bg-gray-100 flex items-center justify-center">🎓</div>
                                <span class="truncate">${person.education}</span>
                            </div>
                        </div>
                        
                        <div class="mb-6">
                            <div class="flex items-center gap-2 mb-3">
                                <div class="w-6 h-6 rounded-lg bg-gray-100 flex items-center justify-center text-sm">🛠️</div>
                                <span class="text-mobile font-semibold text-gray-700">ทักษะ</span>
                            </div>
                            <div class="flex flex-wrap gap-2">
                                ${person.skills.slice(0, 3).map(skill => 
                                    `<span class="text-sm bg-indigo-100 text-indigo-700 px-3 py-1 rounded-full">${skill}</span>`
                                ).join('')}
                                ${person.skills.length > 3 ? `<span class="text-sm text-gray-500">+${person.skills.length - 3}</span>` : ''}
                            </div>
                        </div>
                        
                        <div class="flex-mobile">
                            <button onclick="viewPersonDetails(${person.id})" class="modern-button button-mobile">
                                <div class="flex items-center justify-center gap-2">
                                    <span class="text-xl">👤</span>
                                    <span class="text-mobile-lg">ดูโปรไฟล์</span>
                                </div>
                            </button>
                            <button onclick="contactPerson(${person.id})" class="button-mobile ${person.available ? 'bg-green-500 text-white border-2 border-green-500' : 'bg-gray-300 text-gray-500 border-2 border-gray-300'}" ${!person.available ? 'disabled' : ''}>
                                <div class="flex items-center justify-center gap-2">
                                    <span class="text-xl">${person.available ? '📞' : '🚫'}</span>
                                    <span class="text-mobile-lg">${person.available ? 'ติดต่อ' : 'ไม่ว่าง'}</span>
                                </div>
                            </button>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // View job details
        function viewDetails(id) {
            viewJobDetails(id, false);
        }

        // View job details with apply functionality
        function viewJobDetails(id, fromCompany = false) {
            const job = jobs.find(j => j.id === id);
            if (!job) return;
            
            const categoryData = categoryInfo[job.category];
            const salaryRange = `${job.salaryMin.toLocaleString()}-${job.salaryMax.toLocaleString()}`;
            const daysAgo = Math.floor((new Date() - new Date(job.posted)) / (1000 * 60 * 60 * 24));
            
            document.getElementById('modal-content').innerHTML = `
                <div class="p-4 sm:p-6">
                    <!-- Mobile handle bar -->
                    <div class="w-12 h-1 bg-gray-300 rounded-full mx-auto mb-4 sm:hidden"></div>
                    
                    <div class="flex justify-between items-start mb-4 sm:mb-6">
                        <div class="flex items-start gap-3 flex-1 min-w-0">
                            <span class="text-2xl sm:text-2xl flex-shrink-0">${categoryData.icon}</span>
                            <div class="flex-1 min-w-0">
                                <h2 class="text-xl sm:text-xl font-bold text-gray-900 break-words leading-tight">${job.title}</h2>
                                <p class="text-lg sm:text-lg font-semibold text-gray-700 mb-3 break-words">${job.company}</p>
                                <div class="flex flex-wrap gap-2">
                                    <span class="text-sm font-medium text-indigo-600 bg-indigo-50 px-3 py-1 rounded-full">
                                        ${categoryData.name}
                                    </span>
                                    <span class="text-sm font-medium text-green-600 bg-green-50 px-3 py-1 rounded-full">
                                        ${jobTypeNames[job.type]}
                                    </span>
                                </div>
                            </div>
                        </div>
                        <button onclick="closeDetailModal()" class="text-gray-400 hover:text-gray-600 text-4xl ml-3 touch-manipulation touch-target flex-shrink-0 tap-area p-2 rounded-full hover:bg-gray-100">×</button>
                    </div>
                    
                    <div class="space-y-4 mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>📍</span>
                                    <span class="font-medium">สถานที่ทำงาน</span>
                                </div>
                                <p class="text-gray-900">${job.location}</p>
                            </div>
                            
                            <div class="bg-green-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>💰</span>
                                    <span class="font-medium">เงินเดือน</span>
                                </div>
                                <p class="text-green-700 font-bold text-lg">${salaryRange} บาท</p>
                            </div>
                            
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>📊</span>
                                    <span class="font-medium">ประสบการณ์</span>
                                </div>
                                <p class="text-gray-900">${job.experience} ปี</p>
                            </div>
                            
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>👥</span>
                                    <span class="font-medium">ผู้สมัคร</span>
                                </div>
                                <p class="text-gray-900">${job.applications} คน</p>
                            </div>
                        </div>
                        
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <div class="flex items-center gap-2 text-gray-700 mb-2">
                                <span>📝</span>
                                <span class="font-medium">รายละเอียดงาน</span>
                            </div>
                            <p class="text-gray-900">${job.description}</p>
                        </div>
                        
                        <div class="bg-blue-50 p-4 rounded-lg">
                            <div class="flex items-center gap-2 text-blue-700 mb-2">
                                <span>📅</span>
                                <span class="font-medium">โพสต์เมื่อ</span>
                            </div>
                            <p class="text-blue-900">${daysAgo === 0 ? 'วันนี้' : `${daysAgo} วันที่แล้ว`}</p>
                        </div>
                    </div>
                    
                    <div class="flex flex-col gap-4 sm:flex-row">
                        ${currentMode === 'job-seeker' || fromCompany ? 
                            `<button onclick="applyJob(${job.id})" class="flex-1 bg-green-600 text-white py-5 px-6 rounded-xl hover:bg-green-700 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback">
                                สมัคร
                            </button>` :
                            `<button onclick="viewApplicants(${job.id})" class="flex-1 bg-orange-600 text-white py-5 px-6 rounded-xl hover:bg-orange-700 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback">
                                ดูผู้สมัคร (${job.applications} คน)
                            </button>`
                        }
                        <button onclick="closeDetailModal()" class="flex-1 bg-gray-300 text-gray-700 py-5 px-6 rounded-xl hover:bg-gray-400 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback">
                            ปิด
                        </button>
                    </div>
                </div>
            `;
            
            document.getElementById('detail-modal').classList.remove('hidden');
        }

        // Close detail modal
        function closeDetailModal() {
            document.getElementById('detail-modal').classList.add('hidden');
        }

        // Apply for job
        function applyJob(id) {
            const job = jobs.find(j => j.id === id);
            if (!job) return;
            
            job.applications++;
            renderJobs();
            closeDetailModal();
            
            alert(`สมัครงาน "${job.title}" ที่ ${job.company} เรียบร้อยแล้ว!`);
        }

        // View applicants (for employer mode)
        function viewApplicants(id) {
            const job = jobs.find(j => j.id === id);
            if (!job) return;
            
            alert(`ตำแหน่ง "${job.title}" มีผู้สมัครทั้งหมด ${job.applications} คน\n\nฟีเจอร์นี้จะพัฒนาเพิ่มเติมในอนาคต`);
        }

        // Open add modal
        function openAddModal() {
            editingId = null;
            document.getElementById('modal-title').textContent = 'เพิ่มตำแหน่งงานใหม่';
            document.getElementById('job-form').reset();
            document.getElementById('edit-modal').classList.remove('hidden');
        }

        // Edit job
        function editJob(id) {
            const job = jobs.find(j => j.id === id);
            if (!job) return;
            
            editingId = id;
            document.getElementById('modal-title').textContent = 'แก้ไขตำแหน่งงาน';
            
            document.getElementById('job-title').value = job.title;
            document.getElementById('job-company').value = job.company;
            document.getElementById('job-category').value = job.category;
            document.getElementById('job-location').value = job.location;
            document.getElementById('job-salary-min').value = job.salaryMin;
            document.getElementById('job-salary-max').value = job.salaryMax;
            document.getElementById('job-type').value = job.type;
            document.getElementById('job-description').value = job.description;
            document.getElementById('job-experience').value = job.experience;
            
            document.getElementById('edit-modal').classList.remove('hidden');
        }

        // Save job
        function saveJob(event) {
            event.preventDefault();
            
            const formData = {
                title: document.getElementById('job-title').value,
                company: document.getElementById('job-company').value,
                category: document.getElementById('job-category').value,
                location: document.getElementById('job-location').value,
                salaryMin: parseInt(document.getElementById('job-salary-min').value),
                salaryMax: parseInt(document.getElementById('job-salary-max').value),
                type: document.getElementById('job-type').value,
                description: document.getElementById('job-description').value,
                experience: parseInt(document.getElementById('job-experience').value)
            };
            
            if (editingId) {
                // Edit existing job
                const job = jobs.find(j => j.id === editingId);
                if (job) {
                    Object.assign(job, formData);
                }
            } else {
                // Add new job
                const newJob = {
                    id: Date.now(),
                    ...formData,
                    applications: 0,
                    posted: new Date().toISOString().split('T')[0]
                };
                jobs.push(newJob);
            }
            
            renderJobs();
            closeEditModal();
            
            alert(editingId ? 'แก้ไขตำแหน่งงานเรียบร้อยแล้ว!' : 'เพิ่มตำแหน่งงานใหม่เรียบร้อยแล้ว!');
        }

        // Close edit modal
        function closeEditModal() {
            document.getElementById('edit-modal').classList.add('hidden');
            editingId = null;
        }

        // Delete job
        function deleteJob(id) {
            const job = jobs.find(j => j.id === id);
            if (!job) return;
            
            if (confirm(`คุณต้องการลบตำแหน่งงาน "${job.title}" หรือไม่?`)) {
                jobs = jobs.filter(j => j.id !== id);
                renderJobs();
                alert('ลบตำแหน่งงานเรียบร้อยแล้ว!');
            }
        }

        // View person details
        function viewPersonDetails(id) {
            const person = people.find(p => p.id === id);
            if (!person) return;
            
            const stars = '⭐'.repeat(Math.floor(person.rating));
            const availabilityStatus = person.available ? 'พร้อมทำงาน' : 'ไม่ว่าง';
            const availabilityColor = person.available ? 'text-green-600' : 'text-red-600';
            
            document.getElementById('modal-content').innerHTML = `
                <div class="p-4 sm:p-6">
                    <!-- Mobile handle bar -->
                    <div class="w-12 h-1 bg-gray-300 rounded-full mx-auto mb-4 sm:hidden"></div>
                    
                    <div class="flex justify-between items-start mb-4 sm:mb-6">
                        <div class="flex items-start gap-4 flex-1 min-w-0">
                            <span class="text-4xl sm:text-4xl flex-shrink-0">${person.avatar}</span>
                            <div class="flex-1 min-w-0">
                                <h2 class="text-xl sm:text-xl font-bold text-gray-900 break-words leading-tight">${person.name}</h2>
                                <p class="text-lg sm:text-lg font-semibold text-gray-700 mb-2">${person.position}</p>
                                <div class="flex flex-wrap gap-2 mb-2">
                                    <span class="text-sm font-medium text-indigo-600 bg-indigo-50 px-3 py-1 rounded-full">
                                        ${person.age} ปี
                                    </span>
                                    <span class="text-sm font-medium ${availabilityColor} ${person.available ? 'bg-green-50' : 'bg-red-50'} px-3 py-1 rounded-full">
                                        ${availabilityStatus}
                                    </span>
                                </div>
                                <div class="flex items-center gap-2">
                                    <span class="text-sm text-gray-600">${stars} ${person.rating}</span>
                                    <span class="text-sm text-gray-500">•</span>
                                    <span class="text-sm text-gray-600">${person.projects} โปรเจกต์</span>
                                </div>
                            </div>
                        </div>
                        <button onclick="closeDetailModal()" class="text-gray-400 hover:text-gray-600 text-4xl ml-3 touch-manipulation touch-target flex-shrink-0 tap-area p-2 rounded-full hover:bg-gray-100">×</button>
                    </div>
                    
                    <div class="space-y-4 mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>📍</span>
                                    <span class="font-medium">สถานที่</span>
                                </div>
                                <p class="text-gray-900">${person.location}</p>
                            </div>
                            
                            <div class="bg-green-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>💰</span>
                                    <span class="font-medium">เงินเดือนที่ต้องการ</span>
                                </div>
                                <p class="text-green-700 font-bold text-lg">${person.expectedSalary} บาท</p>
                            </div>
                            
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>📊</span>
                                    <span class="font-medium">ประสบการณ์</span>
                                </div>
                                <p class="text-gray-900">${person.experience} ปี</p>
                            </div>
                            
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>🎓</span>
                                    <span class="font-medium">การศึกษา</span>
                                </div>
                                <p class="text-gray-900">${person.education}</p>
                            </div>
                        </div>
                        
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <div class="flex items-center gap-2 text-gray-700 mb-3">
                                <span>🛠️</span>
                                <span class="font-medium">ทักษะ</span>
                            </div>
                            <div class="flex flex-wrap gap-2">
                                ${person.skills.map(skill => 
                                    `<span class="bg-indigo-100 text-indigo-800 px-3 py-1 rounded-full text-sm">${skill}</span>`
                                ).join('')}
                            </div>
                        </div>
                        
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <div class="flex items-center gap-2 text-gray-700 mb-2">
                                <span>📝</span>
                                <span class="font-medium">เกี่ยวกับ</span>
                            </div>
                            <p class="text-gray-900">${person.description}</p>
                        </div>
                        
                        <div class="bg-blue-50 p-4 rounded-lg">
                            <div class="flex items-center gap-2 text-blue-700 mb-2">
                                <span>💼</span>
                                <span class="font-medium">ประเภทงาน</span>
                            </div>
                            <p class="text-blue-900">${jobTypeNames[person.workType] || person.workType}</p>
                        </div>
                    </div>
                    
                    <div class="flex flex-col gap-4 sm:flex-row">
                        <button onclick="contactPerson(${person.id})" class="flex-1 bg-green-600 text-white py-5 px-6 rounded-xl hover:bg-green-700 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback ${!person.available ? 'opacity-50 cursor-not-allowed' : ''}" ${!person.available ? 'disabled' : ''}>
                            ${person.available ? 'ติดต่อเพื่อจ้างงาน' : 'ไม่สามารถติดต่อได้'}
                        </button>
                        <button onclick="closeDetailModal()" class="flex-1 bg-gray-300 text-gray-700 py-5 px-6 rounded-xl hover:bg-gray-400 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback">
                            ปิด
                        </button>
                    </div>
                </div>
            `;
            
            document.getElementById('detail-modal').classList.remove('hidden');
        }

        // Contact person
        function contactPerson(id) {
            const person = people.find(p => p.id === id);
            if (!person) return;
            
            if (!person.available) {
                alert('ขออภัย บุคคลนี้ไม่ว่างในขณะนี้');
                return;
            }
            
            closeDetailModal();
            alert(`ส่งข้อความติดต่อไปยัง ${person.name} เรียบร้อยแล้ว!\n\nเขา/เธอจะได้รับการแจ้งเตือนและจะติดต่อกลับในเร็วๆ นี้`);
        }

        // View company details
        function viewCompanyDetails(id) {
            const company = companies.find(c => c.id === id);
            if (!company) return;
            
            const stars = '⭐'.repeat(Math.floor(company.rating));
            
            document.getElementById('modal-content').innerHTML = `
                <div class="p-4 sm:p-6">
                    <!-- Mobile handle bar -->
                    <div class="w-12 h-1 bg-gray-300 rounded-full mx-auto mb-4 sm:hidden"></div>
                    
                    <div class="flex justify-between items-start mb-4 sm:mb-6">
                        <div class="flex items-start gap-4 flex-1 min-w-0">
                            <span class="text-4xl sm:text-4xl flex-shrink-0">${company.logo}</span>
                            <div class="flex-1 min-w-0">
                                <h2 class="text-xl sm:text-xl font-bold text-gray-900 break-words leading-tight">${company.name}</h2>
                                <p class="text-lg sm:text-lg font-semibold text-gray-700 mb-2">${company.industry}</p>
                                <div class="flex flex-wrap gap-2 mb-2">
                                    <span class="text-sm font-medium text-indigo-600 bg-indigo-50 px-3 py-1 rounded-full">
                                        ${categoryInfo[company.category].name}
                                    </span>
                                    <span class="text-sm font-medium text-green-600 bg-green-50 px-3 py-1 rounded-full">
                                        ${company.openPositions} ตำแหน่งเปิด
                                    </span>
                                </div>
                                <div class="flex items-center gap-2">
                                    <span class="text-sm text-gray-600">${stars} ${company.rating}</span>
                                    <span class="text-sm text-gray-500">•</span>
                                    <span class="text-sm text-gray-600">ก่อตั้ง ${company.founded}</span>
                                </div>
                            </div>
                        </div>
                        <button onclick="closeDetailModal()" class="text-gray-400 hover:text-gray-600 text-4xl ml-3 touch-manipulation touch-target flex-shrink-0 tap-area p-2 rounded-full hover:bg-gray-100">×</button>
                    </div>
                    
                    <div class="space-y-4 mb-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>📍</span>
                                    <span class="font-medium">สถานที่ตั้ง</span>
                                </div>
                                <p class="text-gray-900">${company.location}</p>
                            </div>
                            
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>👥</span>
                                    <span class="font-medium">จำนวนพนักงาน</span>
                                </div>
                                <p class="text-gray-900">${company.employees}</p>
                            </div>
                            
                            <div class="bg-gray-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>🌐</span>
                                    <span class="font-medium">เว็บไซต์</span>
                                </div>
                                <p class="text-blue-600">${company.website}</p>
                            </div>
                            
                            <div class="bg-green-50 p-4 rounded-lg">
                                <div class="flex items-center gap-2 text-gray-700 mb-2">
                                    <span>💼</span>
                                    <span class="font-medium">ตำแหน่งเปิด</span>
                                </div>
                                <p class="text-green-700 font-bold text-lg">${company.openPositions} ตำแหน่ง</p>
                            </div>
                        </div>
                        
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <div class="flex items-center gap-2 text-gray-700 mb-2">
                                <span>📝</span>
                                <span class="font-medium">เกี่ยวกับบริษัท</span>
                            </div>
                            <p class="text-gray-900">${company.description}</p>
                        </div>
                        
                        <div class="bg-blue-50 p-4 rounded-lg">
                            <div class="flex items-center gap-2 text-blue-700 mb-2">
                                <span>🎯</span>
                                <span class="font-medium">วัฒนธรรมองค์กร</span>
                            </div>
                            <p class="text-blue-900">${company.culture}</p>
                        </div>
                        
                        <div class="bg-yellow-50 p-4 rounded-lg">
                            <div class="flex items-center gap-2 text-yellow-700 mb-3">
                                <span>🎁</span>
                                <span class="font-medium">สวัสดิการ</span>
                            </div>
                            <div class="flex flex-wrap gap-2">
                                ${company.benefits.map(benefit => 
                                    `<span class="bg-yellow-100 text-yellow-800 px-3 py-1 rounded-full text-sm">${benefit}</span>`
                                ).join('')}
                            </div>
                        </div>
                    </div>
                    
                    <div class="flex flex-col gap-4 sm:flex-row">
                        <button onclick="viewCompanyJobs(${company.id})" class="flex-1 bg-green-600 text-white py-5 px-6 rounded-xl hover:bg-green-700 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback">
                            ดูตำแหน่งงาน (${company.openPositions})
                        </button>
                        <button onclick="followCompany(${company.id})" class="flex-1 bg-blue-600 text-white py-5 px-6 rounded-xl hover:bg-blue-700 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback">
                            ติดตามบริษัท
                        </button>
                        <button onclick="closeDetailModal()" class="flex-1 bg-gray-300 text-gray-700 py-5 px-6 rounded-xl hover:bg-gray-400 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback">
                            ปิด
                        </button>
                    </div>
                </div>
            `;
            
            document.getElementById('detail-modal').classList.remove('hidden');
        }

        // View company jobs
        function viewCompanyJobs(id) {
            const company = companies.find(c => c.id === id);
            if (!company) return;
            
            // Filter jobs by company
            const companyJobs = jobs.filter(job => job.company === company.name);
            
            if (companyJobs.length === 0) {
                alert(`ขออภัย ไม่มีตำแหน่งงานว่างที่ ${company.name} ในขณะนี้`);
                return;
            }
            
            document.getElementById('modal-content').innerHTML = `
                <div class="p-4 sm:p-6">
                    <!-- Mobile handle bar -->
                    <div class="w-12 h-1 bg-gray-300 rounded-full mx-auto mb-4 sm:hidden"></div>
                    
                    <div class="flex justify-between items-start mb-6">
                        <div class="flex items-start gap-4 flex-1 min-w-0">
                            <span class="text-4xl flex-shrink-0">${company.logo}</span>
                            <div class="flex-1 min-w-0">
                                <h2 class="text-xl font-bold text-gray-900 break-words leading-tight">ตำแหน่งงานที่ ${company.name}</h2>
                                <p class="text-lg text-gray-600 mb-2">${companyJobs.length} ตำแหน่งว่าง</p>
                            </div>
                        </div>
                        <button onclick="closeDetailModal()" class="text-gray-400 hover:text-gray-600 text-4xl ml-3 touch-manipulation touch-target flex-shrink-0 tap-area p-2 rounded-full hover:bg-gray-100">×</button>
                    </div>
                    
                    <div class="space-y-4 mb-6 max-h-96 overflow-y-auto scrollable">
                        ${companyJobs.map(job => {
                            const categoryData = categoryInfo[job.category];
                            const salaryRange = `${job.salaryMin.toLocaleString()}-${job.salaryMax.toLocaleString()}`;
                            const daysAgo = Math.floor((new Date() - new Date(job.posted)) / (1000 * 60 * 60 * 24));
                            
                            return `
                                <div class="bg-gray-50 p-4 rounded-lg border hover:border-indigo-300 transition-colors cursor-pointer touch-feedback" onclick="viewJobFromCompany(${job.id})">
                                    <div class="flex justify-between items-start mb-3">
                                        <div class="flex-1 min-w-0">
                                            <div class="flex items-center gap-2 mb-2">
                                                <span class="text-lg">${categoryData.icon}</span>
                                                <h3 class="text-lg font-semibold text-gray-900 break-words">${job.title}</h3>
                                            </div>
                                            <div class="flex flex-wrap gap-2 mb-2">
                                                <span class="text-sm font-medium text-indigo-600 bg-indigo-100 px-2 py-1 rounded">
                                                    ${categoryData.name}
                                                </span>
                                                <span class="text-sm font-medium text-green-600 bg-green-100 px-2 py-1 rounded">
                                                    ${jobTypeNames[job.type]}
                                                </span>
                                            </div>
                                        </div>
                                        <div class="text-right flex-shrink-0 ml-4">
                                            <div class="text-lg font-bold text-green-600">${salaryRange}</div>
                                            <div class="text-sm text-gray-500">บาท</div>
                                        </div>
                                    </div>
                                    
                                    <div class="space-y-2 text-sm text-gray-600 mb-3">
                                        <div class="flex items-center gap-2">
                                            <span>📍</span>
                                            <span>${job.location}</span>
                                        </div>
                                        <div class="flex items-center gap-2">
                                            <span>📊</span>
                                            <span>ประสบการณ์ ${job.experience} ปี</span>
                                        </div>
                                        <div class="flex items-center gap-2">
                                            <span>👥</span>
                                            <span>${job.applications} คนสมัครแล้ว</span>
                                        </div>
                                        <div class="flex items-center gap-2">
                                            <span>📅</span>
                                            <span>โพสต์ ${daysAgo === 0 ? 'วันนี้' : `${daysAgo} วันที่แล้ว`}</span>
                                        </div>
                                    </div>
                                    
                                    <p class="text-sm text-gray-700 mb-3 line-clamp-2">${job.description}</p>
                                    
                                    <div class="flex justify-end">
                                        <span class="text-sm text-indigo-600 font-medium">คลิกเพื่อดูรายละเอียด →</span>
                                    </div>
                                </div>
                            `;
                        }).join('')}
                    </div>
                    
                    <div class="flex flex-col gap-4">
                        <button onclick="closeDetailModal()" class="w-full bg-gray-300 text-gray-700 py-4 px-6 rounded-xl hover:bg-gray-400 transition-colors duration-200 font-medium touch-manipulation touch-target text-base touch-feedback">
                            ปิด
                        </button>
                    </div>
                </div>
            `;
            
            document.getElementById('detail-modal').classList.remove('hidden');
        }

        // View job from company listing
        function viewJobFromCompany(jobId) {
            viewJobDetails(jobId, true); // Pass true to indicate this is from company view
        }

        // Follow company
        function followCompany(id) {
            const company = companies.find(c => c.id === id);
            if (!company) return;
            
            closeDetailModal();
            alert(`ติดตาม ${company.name} เรียบร้อยแล้ว!\n\nคุณจะได้รับการแจ้งเตือนเมื่อมีตำแหน่งงานใหม่`);
        }

        // Close modals when clicking outside
        document.getElementById('detail-modal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeDetailModal();
            }
        });

        document.getElementById('edit-modal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeEditModal();
            }
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97ac7d4327130c87',t:'MTc1NzE0NjIyMC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
