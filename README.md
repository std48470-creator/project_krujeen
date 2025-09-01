# project_krujeen
#https://www.canva.com/ai/code/thread/57065a08-481a-457e-a21d-a0eeeee2514f
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>รายการกิจกรรม - Easy Work</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Kanit', sans-serif; }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen">
    <!-- Header -->
    <header class="bg-white shadow-lg border-b-4 border-indigo-500">
        <div class="px-4 py-4">
            <div class="text-center mb-4">
                <h1 class="text-2xl sm:text-3xl font-bold text-gray-900">🎯 Easy Work</h1>
                <p class="text-gray-600 mt-1 text-sm sm:text-base">ค้นหาFreelance</p>
            </div>
            <button onclick="showAddForm()" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-4 rounded-lg font-medium transition-colors duration-200 shadow-md hover:shadow-lg text-lg">
                ➕ โพสสิ่งที่คุณอยากได้
            </button>
        </div>
    </header>

    <div class="px-4 py-6">
        <!-- Category Filter -->
        <div class="bg-white rounded-xl shadow-md p-4 mb-6">
            <h2 class="text-lg font-semibold text-gray-800 mb-4">🏷️ กรองตามประเภท</h2>
            <div class="grid grid-cols-2 sm:grid-cols-3 gap-2">
                <button onclick="filterByCategory('all')" class="category-btn active bg-indigo-600 text-white px-3 py-3 rounded-lg font-medium transition-all duration-200 hover:bg-indigo-700 text-sm">
                    ทั้งหมด
                </button>
                <button onclick="filterByCategory('workshop')" class="category-btn bg-gray-200 text-gray-700 px-3 py-3 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300 text-sm">
                    🛠️ Workshop
                </button>
                <button onclick="filterByCategory('seminar')" class="category-btn bg-gray-200 text-gray-700 px-3 py-3 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300 text-sm">
                    📚 Seminar
                </button>
                <button onclick="filterByCategory('conference')" class="category-btn bg-gray-200 text-gray-700 px-3 py-3 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300 text-sm">
                    🎤 Conference
                </button>
                <button onclick="filterByCategory('networking')" class="category-btn bg-gray-200 text-gray-700 px-3 py-3 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300 text-sm">
                    🤝 Networking
                </button>
                <button onclick="filterByCategory('training')" class="category-btn bg-gray-200 text-gray-700 px-3 py-3 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300 text-sm">
                    🎯 Training
                </button>
            </div>
        </div>

        <!-- Activities Grid -->
        <div id="activities-grid" class="space-y-4">
            <!-- Activity cards will be populated by JavaScript -->
        </div>

        <!-- No results message -->
        <div id="no-results" class="hidden text-center py-12">
            <div class="text-6xl mb-4">🔍</div>
            <h3 class="text-xl font-semibold text-gray-600 mb-2">ไม่พบกิจกรรมในประเภทนี้</h3>
            <p class="text-gray-500">ลองเลือกประเภทอื่นหรือดูกิจกรรมทั้งหมด</p>
        </div>
    </div>

    <!-- Activity Detail Modal -->
    <div id="detail-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center p-4">
        <div class="bg-white rounded-xl max-w-2xl w-full max-h-[90vh] overflow-y-auto">
            <div id="modal-content">
                <!-- Modal content will be populated by JavaScript -->
            </div>
        </div>
    </div>

    <!-- Add/Edit Activity Modal -->
    <div id="edit-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center p-4">
        <div class="bg-white rounded-xl max-w-lg w-full max-h-[90vh] overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 id="modal-title" class="text-xl font-bold text-gray-900">เพิ่มกิจกรรมใหม่</h2>
                    <button onclick="closeEditModal()" class="text-gray-400 hover:text-gray-600 text-2xl">×</button>
                </div>
                
                <form id="activity-form" onsubmit="saveActivity(event)">
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อกิจกรรม</label>
                            <input type="text" id="activity-title" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">ประเภท</label>
                            <select id="activity-category" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                                <option value="workshop">🛠️ Workshop</option>
                                <option value="seminar">📚 Seminar</option>
                                <option value="conference">🎤 Conference</option>
                                <option value="networking">🤝 Networking</option>
                                <option value="training">🎯 Training</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">วันที่</label>
                            <input type="date" id="activity-date" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">เวลา</label>
                            <input type="time" id="activity-time" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">สถานที่</label>
                            <input type="text" id="activity-location" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">ราคา (บาท)</label>
                            <input type="number" id="activity-price" required min="0" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">รายละเอียด</label>
                            <textarea id="activity-description" required rows="4" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"></textarea>
                        </div>
                    </div>
                    
                    <div class="flex gap-3 mt-6">
                        <button type="button" onclick="closeEditModal()" class="flex-1 px-4 py-2 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors">
                            ยกเลิก
                        </button>
                        <button type="submit" class="flex-1 px-4 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition-colors">
                            บันทึก
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <script>
        // Sample data
        let activities = [
            {
                id: 1,
                title: "Workshop การพัฒนาเว็บไซต์ด้วย React",
                category: "workshop",
                date: "2024-02-15",
                time: "09:00",
                location: "ห้องประชุม A ชั้น 5",
                price: 2500,
                description: "เรียนรู้การสร้างเว็บไซต์สมัยใหม่ด้วย React จากผู้เชี่ยวชาญ พร้อมแบบฝึกหัดและโปรเจคจริง",
                organizer: "Tech Academy",
                participants: 25,
                maxParticipants: 30
            },
            {
                id: 2,
                title: "Seminar การตลาดดิจิทัลยุค 4.0",
                category: "seminar",
                date: "2024-02-20",
                time: "14:00",
                location: "โรงแรมแกรนด์ ห้องบอลรูม",
                price: 1500,
                description: "เทคนิคการตลาดออนไลน์ที่ทันสมัย Social Media Marketing และ SEO",
                organizer: "Digital Marketing Pro",
                participants: 45,
                maxParticipants: 100
            },
            {
                id: 3,
                title: "Conference นวัตกรรมเทคโนโลยี AI",
                category: "conference",
                date: "2024-02-25",
                time: "08:30",
                location: "ศูนย์ประชุมแห่งชาติสิริกิติ์",
                price: 3500,
                description: "การประชุมใหญ่เกี่ยวกับปัญญาประดิษฐ์และอนาคตของเทคโนโลジี",
                organizer: "AI Innovation Hub",
                participants: 150,
                maxParticipants: 500
            }
        ];

        let currentFilter = 'all';
        let editingId = null;

        // Initialize the page
        document.addEventListener('DOMContentLoaded', function() {
            renderActivities();
        });

        function renderActivities() {
            const grid = document.getElementById('activities-grid');
            const noResults = document.getElementById('no-results');
            
            let filteredActivities = activities;
            if (currentFilter !== 'all') {
                filteredActivities = activities.filter(activity => activity.category === currentFilter);
            }

            if (filteredActivities.length === 0) {
                grid.innerHTML = '';
                noResults.classList.remove('hidden');
                return;
            }

            noResults.classList.add('hidden');
            
            grid.innerHTML = filteredActivities.map(activity => `
                <div class="bg-white rounded-xl shadow-md hover:shadow-lg transition-shadow duration-200 overflow-hidden">
                    <div class="p-6">
                        <div class="flex justify-between items-start mb-4">
                            <div class="flex-1">
                                <h3 class="text-lg font-semibold text-gray-900 mb-2">${activity.title}</h3>
                                <div class="flex items-center gap-2 text-sm text-gray-600 mb-2">
                                    <span class="bg-indigo-100 text-indigo-800 px-2 py-1 rounded-full text-xs font-medium">
                                        ${getCategoryIcon(activity.category)} ${getCategoryName(activity.category)}
                                    </span>
                                </div>
                            </div>
                            <div class="text-right">
                                <div class="text-2xl font-bold text-indigo-600">฿${activity.price.toLocaleString()}</div>
                            </div>
                        </div>
                        
                        <div class="space-y-2 text-sm text-gray-600 mb-4">
                            <div class="flex items-center gap-2">
                                <span>📅</span>
                                <span>${formatDate(activity.date)} เวลา ${activity.time} น.</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <span>📍</span>
                                <span>${activity.location}</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <span>👥</span>
                                <span>${activity.participants}/${activity.maxParticipants} คน</span>
                            </div>
                        </div>
                        
                        <p class="text-gray-700 text-sm mb-4 line-clamp-2">${activity.description}</p>
                        
                        <div class="flex gap-2">
                            <button onclick="showActivityDetail(${activity.id})" class="flex-1 bg-indigo-600 hover:bg-indigo-700 text-white px-4 py-2 rounded-lg font-medium transition-colors text-sm">
                                ดูรายละเอียด
                            </button>
                            <button onclick="editActivity(${activity.id})" class="px-4 py-2 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors text-sm">
                                แก้ไข
                            </button>
                            <button onclick="deleteActivity(${activity.id})" class="px-4 py-2 border border-red-300 text-red-600 rounded-lg hover:bg-red-50 transition-colors text-sm">
                                ลบ
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function filterByCategory(category) {
            currentFilter = category;
            
            // Update button styles
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('active', 'bg-indigo-600', 'text-white');
                btn.classList.add('bg-gray-200', 'text-gray-700');
            });
            
            event.target.classList.remove('bg-gray-200', 'text-gray-700');
            event.target.classList.add('active', 'bg-indigo-600', 'text-white');
            
            renderActivities();
        }

        function showActivityDetail(id) {
            const activity = activities.find(a => a.id === id);
            if (!activity) return;

            const modal = document.getElementById('detail-modal');
            const content = document.getElementById('modal-content');
            
            content.innerHTML = `
                <div class="p-6">
                    <div class="flex justify-between items-start mb-6">
                        <h2 class="text-2xl font-bold text-gray-900">${activity.title}</h2>
                        <button onclick="closeDetailModal()" class="text-gray-400 hover:text-gray-600 text-2xl">×</button>
                    </div>
                    
                    <div class="space-y-4 mb-6">
                        <div class="flex items-center gap-3">
                            <span class="bg-indigo-100 text-indigo-800 px-3 py-1 rounded-full text-sm font-medium">
                                ${getCategoryIcon(activity.category)} ${getCategoryName(activity.category)}
                            </span>
                            <span class="text-2xl font-bold text-indigo-600">฿${activity.price.toLocaleString()}</span>
                        </div>
                        
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 text-sm">
                            <div class="flex items-center gap-2">
                                <span>📅</span>
                                <span>${formatDate(activity.date)}</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <span>⏰</span>
                                <span>${activity.time} น.</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <span>📍</span>
                                <span>${activity.location}</span>
                            </div>
                            <div class="flex items-center gap-2">
                                <span>👥</span>
                                <span>${activity.participants}/${activity.maxParticipants} คน</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="mb-6">
                        <h3 class="text-lg font-semibold text-gray-900 mb-3">รายละเอียด</h3>
                        <p class="text-gray-700 leading-relaxed">${activity.description}</p>
                    </div>
                    
                    <div class="mb-6">
                        <h3 class="text-lg font-semibold text-gray-900 mb-3">ผู้จัด</h3>
                        <p class="text-gray-700">${activity.organizer}</p>
                    </div>
                    
                    <div class="flex gap-3">
                        <button onclick="registerActivity(${activity.id})" class="flex-1 bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-3 rounded-lg font-medium transition-colors">
                            สมัครเข้าร่วม
                        </button>
                        <button onclick="closeDetailModal()" class="px-6 py-3 border border-gray-300 text-gray-700 rounded-lg hover:bg-gray-50 transition-colors">
                            ปิด
                        </button>
                    </div>
                </div>
            `;
            
            modal.classList.remove('hidden');
        }

        function closeDetailModal() {
            document.getElementById('detail-modal').classList.add('hidden');
        }

        function showAddForm() {
            editingId = null;
            document.getElementById('modal-title').textContent = 'เพิ่มกิจกรรมใหม่';
            document.getElementById('activity-form').reset();
            document.getElementById('edit-modal').classList.remove('hidden');
        }

        function editActivity(id) {
            const activity = activities.find(a => a.id === id);
            if (!activity) return;

            editingId = id;
            document.getElementById('modal-title').textContent = 'แก้ไขกิจกรรม';
            
            document.getElementById('activity-title').value = activity.title;
            document.getElementById('activity-category').value = activity.category;
            document.getElementById('activity-date').value = activity.date;
            document.getElementById('activity-time').value = activity.time;
            document.getElementById('activity-location').value = activity.location;
            document.getElementById('activity-price').value = activity.price;
            document.getElementById('activity-description').value = activity.description;
            
            document.getElementById('edit-modal').classList.remove('hidden');
        }

        function closeEditModal() {
            document.getElementById('edit-modal').classList.add('hidden');
            editingId = null;
        }

        function saveActivity(event) {
            event.preventDefault();
            
            const formData = {
                title: document.getElementById('activity-title').value,
                category: document.getElementById('activity-category').value,
                date: document.getElementById('activity-date').value,
                time: document.getElementById('activity-time').value,
                location: document.getElementById('activity-location').value,
                price: parseInt(document.getElementById('activity-price').value),
                description: document.getElementById('activity-description').value,
                organizer: "Easy Work User",
                participants: 0,
                maxParticipants: 50
            };

            if (editingId) {
                // Edit existing activity
                const index = activities.findIndex(a => a.id === editingId);
                if (index !== -1) {
                    activities[index] = { ...activities[index], ...formData };
                }
            } else {
                // Add new activity
                const newActivity = {
                    id: Date.now(),
                    ...formData
                };
                activities.unshift(newActivity);
            }

            closeEditModal();
            renderActivities();
        }

        function deleteActivity(id) {
            if (confirm('คุณแน่ใจหรือไม่ที่จะลบกิจกรรมนี้?')) {
                activities = activities.filter(a => a.id !== id);
                renderActivities();
            }
        }

        function registerActivity(id) {
            const activity = activities.find(a => a.id === id);
            if (activity && activity.participants < activity.maxParticipants) {
                activity.participants++;
                alert('สมัครเข้าร่วมกิจกรรมเรียบร้อยแล้ว!');
                closeDetailModal();
                renderActivities();
            } else {
                alert('ขออภัย กิจกรรมนี้เต็มแล้ว');
            }
        }

        function getCategoryIcon(category) {
            const icons = {
                workshop: '🛠️',
                seminar: '📚',
                conference: '🎤',
                networking: '🤝',
                training: '🎯'
            };
            return icons[category] || '📋';
        }

        function getCategoryName(category) {
            const names = {
                workshop: 'Workshop',
                seminar: 'Seminar',
                conference: 'Conference',
                networking: 'Networking',
                training: 'Training'
            };
            return names[category] || category;
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
            const options = { 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric',
                weekday: 'long'
            };
            return date.toLocaleDateString('th-TH', options);
        }

        // Close modals when clicking outside
        document.getElementById('detail-modal').addEventListener('click', function(e) {
            if (e.target === this) closeDetailModal();
        });

        document.getElementById('edit-modal').addEventListener('click', function(e) {
            if (e.target === this) closeEditModal();
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9783b40bf710a1ae',t:'MTc1NjcxODU0OC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
