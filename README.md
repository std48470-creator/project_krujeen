# project_krujeen
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>รายการกิจกรรม - Activity Management</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Kanit', sans-serif; }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen">
    <!-- Header -->
    <header class="bg-white shadow-lg border-b-4 border-indigo-500">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
            <div class="flex justify-between items-center">
                <div>
                    <h1 class="text-3xl font-bold text-gray-900">🎯 Activity Management</h1>
                    <p class="text-gray-600 mt-1">จัดการและค้นหากิจกรรมที่น่าสนใจ</p>
                </div>
                <button onclick="showAddForm()" class="bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-3 rounded-lg font-medium transition-colors duration-200 shadow-md hover:shadow-lg">
                    ➕ เพิ่มกิจกรรมใหม่
                </button>
            </div>
        </div>
    </header>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <!-- Category Filter -->
        <div class="bg-white rounded-xl shadow-md p-6 mb-8">
            <h2 class="text-xl font-semibold text-gray-800 mb-4">🏷️ กรองตามประเภท</h2>
            <div class="flex flex-wrap gap-3">
                <button onclick="filterByCategory('all')" class="category-btn active bg-indigo-600 text-white px-4 py-2 rounded-lg font-medium transition-all duration-200 hover:bg-indigo-700">
                    ทั้งหมด
                </button>
                <button onclick="filterByCategory('workshop')" class="category-btn bg-gray-200 text-gray-700 px-4 py-2 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300">
                    🛠️ Workshop
                </button>
                <button onclick="filterByCategory('seminar')" class="category-btn bg-gray-200 text-gray-700 px-4 py-2 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300">
                    📚 Seminar
                </button>
                <button onclick="filterByCategory('conference')" class="category-btn bg-gray-200 text-gray-700 px-4 py-2 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300">
                    🎤 Conference
                </button>
                <button onclick="filterByCategory('networking')" class="category-btn bg-gray-200 text-gray-700 px-4 py-2 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300">
                    🤝 Networking
                </button>
                <button onclick="filterByCategory('training')" class="category-btn bg-gray-200 text-gray-700 px-4 py-2 rounded-lg font-medium transition-all duration-200 hover:bg-gray-300">
                    🎯 Training
                </button>
            </div>
        </div>

        <!-- Activities Grid -->
        <div id="activities-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
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

    <!-- Edit Activity Modal -->
    <div id="edit-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center p-4">
        <div class="bg-white rounded-xl max-w-2xl w-full max-h-[90vh] overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-bold text-gray-900">✏️ แก้ไขกิจกรรม</h2>
                    <button onclick="closeEditForm()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
                </div>
                
                <form id="edit-activity-form" class="space-y-4">
                    <input type="hidden" id="edit-id">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อกิจกรรม</label>
                        <input type="text" id="edit-title" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">รายละเอียด</label>
                        <textarea id="edit-description" required rows="3" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"></textarea>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">สถานที่</label>
                            <input type="text" id="edit-location" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">ประเภท</label>
                            <select id="edit-category" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                                <option value="">เลือกประเภท</option>
                                <option value="workshop">Workshop</option>
                                <option value="seminar">Seminar</option>
                                <option value="conference">Conference</option>
                                <option value="networking">Networking</option>
                                <option value="training">Training</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">วันที่เริ่ม</label>
                            <input type="datetime-local" id="edit-start_date" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">วันที่สิ้นสุด</label>
                            <input type="datetime-local" id="edit-end_date" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">ผู้จัด</label>
                        <input type="text" id="edit-organizer" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">ลิงก์การสมัครเข้าร่วม</label>
                        <input type="url" id="edit-registration_link" placeholder="https://example.com/register" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                    </div>
                    
                    <div class="flex gap-3 pt-4">
                        <button type="submit" class="flex-1 bg-orange-500 hover:bg-orange-600 text-white py-3 rounded-lg font-medium transition-colors duration-200">
                            บันทึกการแก้ไข
                        </button>
                        <button type="button" onclick="closeEditForm()" class="px-6 py-3 border border-gray-300 text-gray-700 rounded-lg font-medium hover:bg-gray-50 transition-colors duration-200">
                            ยกเลิก
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Add Activity Modal -->
    <div id="add-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center p-4">
        <div class="bg-white rounded-xl max-w-2xl w-full max-h-[90vh] overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-bold text-gray-900">➕ เพิ่มกิจกรรมใหม่</h2>
                    <button onclick="closeAddForm()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
                </div>
                
                <form id="add-activity-form" class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อกิจกรรม</label>
                        <input type="text" id="title" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">รายละเอียด</label>
                        <textarea id="description" required rows="3" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"></textarea>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">สถานที่</label>
                            <input type="text" id="location" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">ประเภท</label>
                            <select id="category" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                                <option value="">เลือกประเภท</option>
                                <option value="workshop">Workshop</option>
                                <option value="seminar">Seminar</option>
                                <option value="conference">Conference</option>
                                <option value="networking">Networking</option>
                                <option value="training">Training</option>
                            </select>
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">วันที่เริ่ม</label>
                            <input type="datetime-local" id="start_date" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">วันที่สิ้นสุด</label>
                            <input type="datetime-local" id="end_date" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                        </div>
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">ผู้จัด</label>
                        <input type="text" id="organizer" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">ลิงก์การสมัครเข้าร่วม</label>
                        <input type="url" id="registration_link" placeholder="https://example.com/register" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500">
                    </div>
                    
                    <div class="flex gap-3 pt-4">
                        <button type="submit" class="flex-1 bg-indigo-600 hover:bg-indigo-700 text-white py-3 rounded-lg font-medium transition-colors duration-200">
                            บันทึกกิจกรรม
                        </button>
                        <button type="button" onclick="closeAddForm()" class="px-6 py-3 border border-gray-300 text-gray-700 rounded-lg font-medium hover:bg-gray-50 transition-colors duration-200">
                            ยกเลิก
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <script>
        // Sample activities data (simulating Django context)
        let activities = [
            {
                id: 1,
                title: "Python Web Development Workshop",
                description: "เรียนรู้การพัฒนาเว็บแอปพลิเคชันด้วย Django Framework พร้อมแนวทางปฏิบัติที่ดีและเทคนิคขั้นสูง",
                location: "ห้องประชุม A, ชั้น 5",
                start_date: "2024-02-15T09:00",
                end_date: "2024-02-15T17:00",
                category: "workshop",
                organizer: "Tech Academy",
                registration_link: "https://techacademy.com/python-workshop",
                image: "🐍"
            },
            {
                id: 2,
                title: "Digital Marketing Seminar",
                description: "กลยุทธ์การตลาดดิจิทัลในยุค AI และการใช้ Social Media อย่างมีประสิทธิภาพ",
                location: "โรงแรม Grand Palace",
                start_date: "2024-02-20T13:00",
                end_date: "2024-02-20T18:00",
                category: "seminar",
                organizer: "Marketing Pro",
                registration_link: "https://marketingpro.com/digital-seminar",
                image: "📱"
            },
            {
                id: 3,
                title: "Tech Conference 2024",
                description: "การประชุมเทคโนโลยีประจำปี พบกับนวัตกรรมใหม่ๆ และแนวโน้มเทคโนโลยีในอนาคต",
                location: "ศูนย์การประชุมแห่งชาติสิริกิติ์",
                start_date: "2024-03-01T08:00",
                end_date: "2024-03-03T18:00",
                category: "conference",
                organizer: "Tech Innovation",
                registration_link: "https://techinnovation.com/conference2024",
                image: "💻"
            },
            {
                id: 4,
                title: "Startup Networking Night",
                description: "พบปะเจ้าของธุรกิจ นักลงทุน และผู้ประกอบการรุ่นใหม่ แลกเปลี่ยนประสบการณ์และสร้างเครือข่าย",
                location: "Sky Bar, Lebua Hotel",
                start_date: "2024-02-25T18:00",
                end_date: "2024-02-25T22:00",
                category: "networking",
                organizer: "Startup Hub",
                registration_link: "https://startuphub.com/networking-night",
                image: "🤝"
            },
            {
                id: 5,
                title: "Leadership Training Program",
                description: "พัฒนาทักษะการเป็นผู้นำ การจัดการทีม และการสื่อสารที่มีประสิทธิภาพ",
                location: "ศูนย์ฝึกอบรม Excellence",
                start_date: "2024-03-10T09:00",
                end_date: "2024-03-12T17:00",
                category: "training",
                organizer: "Leadership Institute",
                registration_link: "https://leadership-institute.com/training",
                image: "🎯"
            },
            {
                id: 6,
                title: "UX/UI Design Workshop",
                description: "เรียนรู้หลักการออกแบบ User Experience และ User Interface ที่ดี พร้อมเครื่องมือและเทคนิคใหม่ๆ",
                location: "Creative Space, Siam Square",
                start_date: "2024-02-28T10:00",
                end_date: "2024-02-28T16:00",
                category: "workshop",
                organizer: "Design Studio",
                registration_link: "https://designstudio.com/ux-ui-workshop",
                image: "🎨"
            }
        ];

        let currentFilter = 'all';

        function renderActivities(activitiesToRender = activities) {
            const grid = document.getElementById('activities-grid');
            const noResults = document.getElementById('no-results');
            
            if (activitiesToRender.length === 0) {
                grid.innerHTML = '';
                noResults.classList.remove('hidden');
                return;
            }
            
            noResults.classList.add('hidden');
            
            grid.innerHTML = activitiesToRender.map(activity => {
                const startDate = new Date(activity.start_date);
                const endDate = new Date(activity.end_date);
                const categoryIcons = {
                    workshop: '🛠️',
                    seminar: '📚',
                    conference: '🎤',
                    networking: '🤝',
                    training: '🎯'
                };
                
                return `
                    <div class="bg-white rounded-xl shadow-md hover:shadow-xl transition-all duration-300 overflow-hidden cursor-pointer transform hover:-translate-y-1" onclick="showActivityDetail(${activity.id})">
                        <div class="p-6">
                            <div class="flex items-center justify-between mb-4">
                                <div class="text-4xl">${activity.image}</div>
                                <span class="bg-indigo-100 text-indigo-800 px-3 py-1 rounded-full text-sm font-medium">
                                    ${categoryIcons[activity.category]} ${activity.category}
                                </span>
                            </div>
                            
                            <h3 class="text-xl font-semibold text-gray-900 mb-2 line-clamp-2">${activity.title}</h3>
                            <p class="text-gray-600 mb-4 line-clamp-3">${activity.description}</p>
                            
                            <div class="space-y-2 text-sm text-gray-500">
                                <div class="flex items-center">
                                    <span class="mr-2">📍</span>
                                    <span>${activity.location}</span>
                                </div>
                                <div class="flex items-center">
                                    <span class="mr-2">📅</span>
                                    <span>${startDate.toLocaleDateString('th-TH')} ${startDate.toLocaleTimeString('th-TH', {hour: '2-digit', minute: '2-digit'})}</span>
                                </div>
                                ${activity.organizer ? `
                                <div class="flex items-center">
                                    <span class="mr-2">👤</span>
                                    <span>${activity.organizer}</span>
                                </div>
                                ` : ''}
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
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
            
            // Filter activities
            const filteredActivities = category === 'all' 
                ? activities 
                : activities.filter(activity => activity.category === category);
            
            renderActivities(filteredActivities);
        }

        function showActivityDetail(activityId) {
            const activity = activities.find(a => a.id === activityId);
            if (!activity) return;
            
            const startDate = new Date(activity.start_date);
            const endDate = new Date(activity.end_date);
            const categoryIcons = {
                workshop: '🛠️',
                seminar: '📚',
                conference: '🎤',
                networking: '🤝',
                training: '🎯'
            };
            
            const modalContent = document.getElementById('modal-content');
            modalContent.innerHTML = `
                <div class="relative">
                    <div class="bg-gradient-to-r from-indigo-500 to-purple-600 text-white p-6 rounded-t-xl">
                        <button onclick="closeModal()" class="absolute top-4 right-4 text-white hover:text-gray-200 text-2xl">✕</button>
                        <div class="text-6xl mb-4">${activity.image}</div>
                        <h2 class="text-2xl font-bold mb-2">${activity.title}</h2>
                        <span class="bg-white bg-opacity-20 px-3 py-1 rounded-full text-sm font-medium">
                            ${categoryIcons[activity.category]} ${activity.category}
                        </span>
                    </div>
                    
                    <div class="p-6">
                        <div class="mb-6">
                            <h3 class="text-lg font-semibold text-gray-900 mb-2">📝 รายละเอียด</h3>
                            <p class="text-gray-700 leading-relaxed">${activity.description}</p>
                        </div>
                        
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                            <div>
                                <h4 class="font-semibold text-gray-900 mb-2">📍 สถานที่</h4>
                                <p class="text-gray-700">${activity.location}</p>
                            </div>
                            
                            <div>
                                <h4 class="font-semibold text-gray-900 mb-2">📅 วันที่และเวลา</h4>
                                <p class="text-gray-700">
                                    <strong>เริ่ม:</strong> ${startDate.toLocaleDateString('th-TH')} ${startDate.toLocaleTimeString('th-TH', {hour: '2-digit', minute: '2-digit'})}<br>
                                    <strong>สิ้นสุด:</strong> ${endDate.toLocaleDateString('th-TH')} ${endDate.toLocaleTimeString('th-TH', {hour: '2-digit', minute: '2-digit'})}
                                </p>
                            </div>
                        </div>
                        
                        ${activity.organizer ? `
                        <div class="mb-6">
                            <h4 class="font-semibold text-gray-900 mb-2">👤 ผู้จัด</h4>
                            <p class="text-gray-700">${activity.organizer}</p>
                        </div>
                        ` : ''}
                        
                        ${activity.registration_link ? `
                        <div class="mb-6">
                            <h4 class="font-semibold text-gray-900 mb-2">🔗 ลิงก์การสมัครเข้าร่วม</h4>
                            <a href="${activity.registration_link}" target="_blank" class="text-indigo-600 hover:text-indigo-800 underline break-all">${activity.registration_link}</a>
                        </div>
                        ` : ''}
                        
                        <div class="flex gap-3">
                            ${activity.registration_link ? `
                            <a href="${activity.registration_link}" target="_blank" class="flex-1 bg-indigo-600 hover:bg-indigo-700 text-white py-3 rounded-lg font-medium transition-colors duration-200 text-center">
                                🔗 สมัครเข้าร่วม
                            </a>
                            ` : ''}
                            <button onclick="showEditForm(${activity.id})" class="px-6 py-3 bg-orange-500 hover:bg-orange-600 text-white rounded-lg font-medium transition-colors duration-200">
                                ✏️ แก้ไข
                            </button>
                            <button onclick="showSaveNotification()" class="px-6 py-3 border border-gray-300 text-gray-700 rounded-lg font-medium hover:bg-gray-50 transition-colors duration-200">
                                🔔 แจ้งเตือน
                            </button>
                        </div>
                    </div>
                </div>
            `;
            
            document.getElementById('detail-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('detail-modal').classList.add('hidden');
        }

        function showAddForm() {
            document.getElementById('add-modal').classList.remove('hidden');
        }

        function closeAddForm() {
            document.getElementById('add-modal').classList.add('hidden');
            document.getElementById('add-activity-form').reset();
        }

        document.getElementById('add-activity-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const formData = new FormData(e.target);
            const newActivity = {
                id: activities.length + 1,
                title: document.getElementById('title').value,
                description: document.getElementById('description').value,
                location: document.getElementById('location').value,
                start_date: document.getElementById('start_date').value,
                end_date: document.getElementById('end_date').value,
                category: document.getElementById('category').value,
                organizer: document.getElementById('organizer').value || '',
                registration_link: document.getElementById('registration_link').value || '',
                image: ['🎯', '🚀', '💡', '⭐', '🎨', '📊'][Math.floor(Math.random() * 6)]
            };
            
            activities.unshift(newActivity);
            
            // Re-render with current filter
            const filteredActivities = currentFilter === 'all' 
                ? activities 
                : activities.filter(activity => activity.category === currentFilter);
            renderActivities(filteredActivities);
            
            closeAddForm();
            
            // Show success message
            const successMsg = document.createElement('div');
            successMsg.className = 'fixed top-4 right-4 bg-green-500 text-white px-6 py-3 rounded-lg shadow-lg z-50';
            successMsg.textContent = '✅ เพิ่มกิจกรรมเรียบร้อยแล้ว!';
            document.body.appendChild(successMsg);
            
            setTimeout(() => {
                successMsg.remove();
            }, 3000);
        });

        document.getElementById('edit-activity-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const activityId = parseInt(document.getElementById('edit-id').value);
            const activityIndex = activities.findIndex(a => a.id === activityId);
            
            if (activityIndex !== -1) {
                // Update the activity
                activities[activityIndex] = {
                    ...activities[activityIndex],
                    title: document.getElementById('edit-title').value,
                    description: document.getElementById('edit-description').value,
                    location: document.getElementById('edit-location').value,
                    start_date: document.getElementById('edit-start_date').value,
                    end_date: document.getElementById('edit-end_date').value,
                    category: document.getElementById('edit-category').value,
                    organizer: document.getElementById('edit-organizer').value || '',
                    registration_link: document.getElementById('edit-registration_link').value || ''
                };
                
                // Re-render with current filter
                const filteredActivities = currentFilter === 'all' 
                    ? activities 
                    : activities.filter(activity => activity.category === currentFilter);
                renderActivities(filteredActivities);
                
                closeEditForm();
                
                // Show success message
                const successMsg = document.createElement('div');
                successMsg.className = 'fixed top-4 right-4 bg-orange-500 text-white px-6 py-3 rounded-lg shadow-lg z-50';
                successMsg.textContent = '✅ แก้ไขกิจกรรมเรียบร้อยแล้ว!';
                document.body.appendChild(successMsg);
                
                setTimeout(() => {
                    successMsg.remove();
                }, 3000);
            }
        });

        function showSaveNotification() {
            // Show notification message
            const notificationMsg = document.createElement('div');
            notificationMsg.className = 'fixed top-4 right-4 bg-yellow-500 text-white px-6 py-3 rounded-lg shadow-lg z-50 flex items-center gap-2';
            notificationMsg.innerHTML = '🔔 <span>ตั้งค่าการแจ้งเตือนสำหรับกิจกรรมนี้แล้ว!</span>';
            document.body.appendChild(notificationMsg);
            
            setTimeout(() => {
                notificationMsg.remove();
            }, 3000);
        }

        function showEditForm(activityId) {
            const activity = activities.find(a => a.id === activityId);
            if (!activity) return;
            
            // Fill form with current activity data
            document.getElementById('edit-id').value = activity.id;
            document.getElementById('edit-title').value = activity.title;
            document.getElementById('edit-description').value = activity.description;
            document.getElementById('edit-location').value = activity.location;
            document.getElementById('edit-category').value = activity.category;
            document.getElementById('edit-start_date').value = activity.start_date;
            document.getElementById('edit-end_date').value = activity.end_date;
            document.getElementById('edit-organizer').value = activity.organizer || '';
            document.getElementById('edit-registration_link').value = activity.registration_link || '';
            
            // Close detail modal and show edit modal
            closeModal();
            document.getElementById('edit-modal').classList.remove('hidden');
        }

        function closeEditForm() {
            document.getElementById('edit-modal').classList.add('hidden');
            document.getElementById('edit-activity-form').reset();
        }

        // Close modals when clicking outside
        document.getElementById('detail-modal').addEventListener('click', function(e) {
            if (e.target === this) closeModal();
        });

        document.getElementById('add-modal').addEventListener('click', function(e) {
            if (e.target === this) closeAddForm();
        });

        document.getElementById('edit-modal').addEventListener('click', function(e) {
            if (e.target === this) closeEditForm();
        });

        // Initial render
        renderActivities();
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97838f7ff7e4a1ae',t:'MTc1NjcxNzA1MS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
