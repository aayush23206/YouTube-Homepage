# YouTube-Homepage
Basic project
<!DOCTYPE html> <html lang="en" > <head> <meta charset="UTF-8" /> <meta name="viewport" content="width=device-width, initial-scale=1" /> <title>YouTube - Dark Mode with Navigation & Backend</title> <script src="https://cdn.tailwindcss.com"></script> <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" /> <style> body { font-family: Arial, sans-serif; } .sidebar { min-height: 100vh; } .video-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 20px; } .video-card { background: #1f2937; /* Tailwind gray-800 */ border-radius: 8px; overflow: hidden; box-shadow: 0 2px 4px rgba(0,0,0,0.5); transition: transform 0.2s; color: #e5e7eb; /* Tailwind gray-200 */ } .video-card:hover { transform: scale(1.05); } .thumbnail img { width: 100%; height: auto; display: block; } /* Dark mode sidebar */ .sidebar { background-color: #111827; /* Tailwind gray-900 */ color: #d1d5db; /* Tailwind gray-300 */ } .sidebar ul li:hover { background-color: #374151; /* Tailwind gray-700 */ } /* Dark mode header */ header { background-color: #111827; /* Tailwind gray-900 */ color: #e5e7eb; /* Tailwind gray-200 */ } /* Dark mode nav bar */ nav#mainNav { background-color: #1f2937; /* Tailwind gray-800 */ color: #e5e7eb; border-bottom: 1px solid #374151; } nav#mainNav a { color: #e5e7eb; } nav#mainNav a:hover { color: #3b82f6; /* Tailwind blue-500 */ } /* Dark mode backdrop */ #backdrop { background-color: rgba(0, 0, 0, 0.7); } /* Modal styles */ .modal { background-color: #1f2937; /* Tailwind gray-800 */ color: #e5e7eb; border-radius: 8px; box-shadow: 0 10px 25px rgba(0,0,0,0.7); padding: 1rem; position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); z-index: 50; width: 90%; max-width: 400px; display: none; } .modal.show { display: block; } .modal-header { font-weight: bold; font-size: 1.25rem; margin-bottom: 0.5rem; } .modal-close { cursor: pointer; float: right; font-size: 1.25rem; font-weight: bold; color: #9ca3af; /* Tailwind gray-400 */ } .modal-close:hover { color: #f87171; /* Tailwind red-400 */ } /* Responsive sidebar */ @media (max-width: 768px) { .sidebar { display: none; } .sidebar.show { display: block; position: fixed; top: 0; left: 0; width: 16rem; /* 64 */ height: 100vh; z-index: 40; box-shadow: 2px 0 8px rgba(0,0,0,0.7); overflow-y: auto; } .video-grid { grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); } } </style> </head> <body class="bg-gray-900 text-gray-200"> <!-- Header --> <header class="px-4 py-2 flex items-center justify-between border-b border-gray-700"> <div class="flex items-center"> <button id="menuBtn" class="mr-4 text-2xl hover:text-blue-500 focus:outline-none" aria-label="Toggle menu"> <i class="material-icons">menu</i> </button> <div class="flex items-center"> <i class="material-icons text-red-600 text-3xl mr-1">play_circle</i> <span class="text-2xl font-semibold">YouTube</span> </div> </div> <div class="flex-1 max-w-xl mx-4"> <div class="flex"> <input type="text" id="searchInput" placeholder="Search" class="flex-1 px-4 py-2 border border-gray-700 rounded-l-full bg-gray-800 text-gray-200 focus:outline-none focus:ring-2 focus:ring-blue-500" aria-label="Search videos" /> <button id="searchBtn" class="px-4 py-2 bg-gray-800 border border-gray-700 rounded-r-full hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-blue-500" aria-label="Search" > <i class="material-icons">search</i> </button> </div> </div> <div class="flex items-center space-x-4"> <button id="createBtn" class="px-3 py-2 bg-blue-600 text-white rounded flex items-center hover:bg-blue-700 focus:outline-none" aria-haspopup="dialog" aria-controls="createModal" aria-expanded="false"> <i class="material-icons mr-1">videocam</i>Create </button> <button id="notificationsBtn" class="relative hover:text-blue-500 focus:outline-none" aria-haspopup="dialog" aria-controls="notificationsModal" aria-expanded="false" aria-label="Notifications"> <i class="material-icons">notifications</i> <span id="notifCount" class="absolute top-0 right-0 bg-red-600 text-xs rounded-full px-1 leading-none">3</span> </button> <button id="accountBtn" class="hover:text-blue-500 focus:outline-none" aria-haspopup="dialog" aria-controls="accountModal" aria-expanded="false" aria-label="Account info"> <i class="material-icons">account_circle</i> </button> </div> </header> <!-- Navigation Bar --> <nav id="mainNav" class="flex space-x-6 px-6 py-3 border-b border-gray-700"> <a href="#" class="hover:text-blue-500">Home</a> <a href="#" class="hover:text-blue-500">Shorts</a> <a href="#" class="hover:text-blue-500">Subscriptions</a> <a href="#" class="hover:text-blue-500">Library</a> <a href="#" class="hover:text-blue-500">History</a> <a href="#" class="hover:text-blue-500">Liked Videos</a> </nav> <!-- Main Content --> <div class="flex"> <!-- Sidebar --> <aside class="sidebar w-64 md:block"> <nav> <ul class="py-4"> <li class="px-4 py-2 hover:bg-gray-700 cursor-pointer flex items-center"><i class="material-icons mr-3">home</i>Home</li> <li class="px-4 py-2 hover:bg-gray-700 cursor-pointer flex items-center"><i class="material-icons mr-3">bolt</i>Shorts</li> <li class="px-4 py-2 hover:bg-gray-700 cursor-pointer flex items-center"><i class="material-icons mr-3">subscriptions</i>Subscriptions</li> <li class="px-4 py-2 hover:bg-gray-700 cursor-pointer flex items-center"><i class="material-icons mr-3">video_library</i>Library</li> <li class="px-4 py-2 hover:bg-gray-700 cursor-pointer flex items-center"><i class="material-icons mr-3">history</i>History</li> <li class="px-4 py-2 hover:bg-gray-700 cursor-pointer flex items-center"><i class="material-icons mr-3">thumb_up</i>Liked videos</li> </ul> </nav> </aside>
<!-- Backdrop -->
<div id="backdrop" class="fixed inset-0 bg-black bg-opacity-70 hidden z-30"></div>

<!-- Videos Section -->
<main class="flex-1 p-4">
  <div id="videosContainer" class="video-grid">
    <!-- Videos will be populated by JS -->
  </div>
</main>
</div> <!-- Modals --> <!-- Create Modal --> <div id="createModal" class="modal" role="dialog" aria-modal="true" aria-labelledby="createModalTitle" tabindex="-1"> <div class="modal-header"> Create Video <span class="modal-close" data-close="createModal" aria-label="Close modal">&times;</span> </div> <p>Here you can add your video creation tools or upload form.</p> </div> <!-- Notifications Modal --> <div id="notificationsModal" class="modal" role="dialog" aria-modal="true" aria-labelledby="notificationsModalTitle" tabindex="-1"> <div class="modal-header"> Notifications <span class="modal-close" data-close="notificationsModal" aria-label="Close modal">&times;</span> </div> <ul class="list-disc list-inside"> <li>New comment on your video</li> <li>Channel subscription update</li> <li>New video recommendation</li> </ul> </div> <!-- Account Modal --> <div id="accountModal" class="modal" role="dialog" aria-modal="true" aria-labelledby="accountModalTitle" tabindex="-1"> <div class="modal-header"> Account Info <span class="modal-close" data-close="accountModal" aria-label="Close modal">&times;</span> </div> <p><strong>User:</strong> John Doe</p> <p><strong>Email:</strong> john.doe@example.com</p> <button class="mt-4 px-4 py-2 bg-red-600 rounded hover:bg-red-700 focus:outline-none" id="logoutBtn">Logout</button> </div> <script> // Mock video data const videos = [ { title: "Amazing Coding Tutorial", channel: "CodeMaster", views: "1.2M views", thumbnail: "https://placehold.co/320x180/FF0000/FFFFFF?text=Code+Tutorial", time: "10 minutes ago" }, { title: "Travel Vlog: Exploring Mountains", channel: "AdventureSeeker", views: "500K views", thumbnail: "https://placehold.co/320x180/00FF00/000000?text=Mountain+Vlog", time: "2 hours ago" }, { title: "Cooking Show: Delicious Pasta", channel: "ChefGourmet", views: "750K views", thumbnail: "https://placehold.co/320x180/0000FF/FFFFFF?text=Italian+Pasta", time: "1 day ago" }, { title: "Music Video: Electronic Beats", channel: "DJElectro", views: "2M views", thumbnail: "https://placehold.co/320x180/FFFF00/000000?text=Electronic+Music", time: "3 days ago" }, { title: "Science Explained: Quantum Physics", channel: "SciExplain", views: "900K views", thumbnail: "https://placehold.co/320x180/FF00FF/FFFFFF?text=Quantum+Physics", time: "5 hours ago" }, { title: "Fitness Workout: Full Body", channel: "FitLife", views: "1.5M views", thumbnail: "https://placehold.co/320x180/00FFFF/000000?text=Fitness+Workout", time: "1 week ago" } ]; // Function to render videos function renderVideos(videoList) { const container = document.getElementById('videosContainer'); container.innerHTML = ''; videoList.forEach(video => { const videoCard = document.createElement('div'); videoCard.className = 'video-card'; videoCard.innerHTML = ` <div class="thumbnail"> <img src="${video.thumbnail}" alt="${video.title} video thumbnail featuring a vibrant and engaging scene related to the topic" /> </div> <div class="p-4"> <h3 class="font-bold text-lg mb-1">${video.title}</h3> <p class="text-gray-400 text-sm mb-1">${video.channel}</p> <p class="text-gray-500 text-sm">${video.views} • ${video.time}</p> </div> `; container.appendChild(videoCard); }); } // Initial render renderVideos(videos); // Search functionality const searchInput = document.getElementById('searchInput'); const searchBtn = document.getElementById('searchBtn'); function performSearch() { const query = searchInput.value.toLowerCase(); const filteredVideos = videos.filter(video => video.title.toLowerCase().includes(query) || video.channel.toLowerCase().includes(query) ); renderVideos(filteredVideos); } searchBtn.addEventListener('click', performSearch); searchInput.addEventListener('keypress', (e) => { if (e.key === 'Enter') { performSearch(); } }); // Sidebar toggle for mobile with backdrop const menuBtn = document.getElementById('menuBtn'); const sidebar = document.querySelector('.sidebar'); const backdrop = document.getElementById('backdrop'); menuBtn.addEventListener('click', () => { sidebar.classList.toggle('show'); backdrop.classList.toggle('hidden'); }); backdrop.addEventListener('click', () => { sidebar.classList.remove('show'); backdrop.classList.add('hidden'); closeAllModals(); }); // Modal handling const createBtn = document.getElementById('createBtn'); const notificationsBtn = document.getElementById('notificationsBtn'); const accountBtn = document.getElementById('accountBtn'); const createModal = document.getElementById('createModal'); const notificationsModal = document.getElementById('notificationsModal'); const accountModal = document.getElementById('accountModal'); function closeAllModals() { [createModal, notificationsModal, accountModal].forEach(modal => { modal.classList.remove('show'); modal.setAttribute('aria-hidden', 'true'); }); backdrop.classList.add('hidden'); } function openModal(modal) { closeAllModals(); modal.classList.add('show'); modal.setAttribute('aria-hidden', 'false'); backdrop.classList.remove('hidden'); } createBtn.addEventListener('click', () => { openModal(createModal); }); notificationsBtn.addEventListener('click', () => { openModal(notificationsModal); }); accountBtn.addEventListener('click', () => { openModal(accountModal); }); // Close modal buttons document.querySelectorAll('.modal-close').forEach(btn => { btn.addEventListener('click', (e) => { const modalId = e.target.getAttribute('data-close'); const modal = document.getElementById(modalId); modal.classList.remove('show'); modal.setAttribute('aria-hidden', 'true'); backdrop.classList.add('hidden'); }); }); // Logout button simulation document.getElementById('logoutBtn').addEventListener('click', () => { alert('Logged out!'); closeAllModals(); }); // Close modals on Escape key document.addEventListener('keydown', (e) => { if (e.key === 'Escape') { closeAllModals(); } }); </script> </body> </html>
/* Base font /
body {
font-family: Arial, sans-serif;
background-color: #111827; / Tailwind gray-900 /
color: #e5e7eb; / Tailwind gray-200 */
margin: 0;
}

/* Sidebar /
.sidebar {
min-height: 100vh;
background-color: #111827; / Tailwind gray-900 /
color: #d1d5db; / Tailwind gray-300 /
width: 16rem; / 64 */
}

.sidebar ul {
padding-top: 1rem;
padding-bottom: 1rem;
margin: 0;
list-style: none;
}

.sidebar ul li {
padding: 0.5rem 1rem;
cursor: pointer;
display: flex;
align-items: center;
}

.sidebar ul li:hover {
background-color: #374151; /* Tailwind gray-700 */
}

.sidebar ul li i.material-icons {
margin-right: 0.75rem;
}

/* Video grid */
.video-grid {
display: grid;
grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
gap: 20px;
}

/* Video card /
.video-card {
background: #1f2937; / Tailwind gray-800 /
border-radius: 8px;
overflow: hidden;
box-shadow: 0 2px 4px rgba(0,0,0,0.5);
transition: transform 0.2s;
color: #e5e7eb; / Tailwind gray-200 */
}

.video-card:hover {
transform: scale(1.05);
}

.thumbnail img {
width: 100%;
height: auto;
display: block;
}

/* Header /
header {
background-color: #111827; / Tailwind gray-900 /
color: #e5e7eb; / Tailwind gray-200 /
padding: 0.5rem 1rem;
border-bottom: 1px solid #374151; / Tailwind gray-700 */
display: flex;
align-items: center;
justify-content: space-between;
}

header .flex {
display: flex;
align-items: center;
}

header button {
background: none;
border: none;
color: inherit;
cursor: pointer;
}

header button:hover,
header button:focus {
color: #3b82f6; /* Tailwind blue-500 */
outline: none;
}

header input[type="text"] {
flex: 1;
padding: 0.5rem 1rem;
border: 1px solid #374151; /* Tailwind gray-700 /
border-right: none;
border-radius: 9999px 0 0 9999px;
background-color: #1f2937; / Tailwind gray-800 */
color: #e5e7eb;
}

header input[type="text"]::placeholder {
color: #9ca3af; /* Tailwind gray-400 */
}

header input[type="text"]:focus {
outline: none;
border-color: #3b82f6; /* Tailwind blue-500 */
box-shadow: 0 0 0 2px #3b82f6;
}

header button#searchBtn {
padding: 0.5rem 1rem;
background-color: #1f2937; /* Tailwind gray-800 /
border: 1px solid #374151; / Tailwind gray-700 */
border-radius: 0 9999px 9999px 0;
cursor: pointer;
}

header button#searchBtn:hover,
header button#searchBtn:focus {
background-color: #374151; /* Tailwind gray-700 */
outline: none;
box-shadow: 0 0 0 2px #3b82f6;
}

/* Navigation bar /
nav#mainNav {
background-color: #1f2937; / Tailwind gray-800 */
color: #e5e7eb;
border-bottom: 1px solid #374151;
display: flex;
gap: 1.5rem;
padding: 0.75rem 1.5rem;
}

nav#mainNav a {
color: #e5e7eb;
text-decoration: none;
font-weight: 500;
}

nav#mainNav a:hover,
nav#mainNav a:focus {
color: #3b82f6; /* Tailwind blue-500 */
outline: none;
}

/* Buttons in header /
header .flex.items-center.space-x-4 > button {
padding: 0.5rem 0.75rem;
border-radius: 0.375rem;
font-weight: 600;
display: flex;
align-items: center;
gap: 0.25rem;
cursor: pointer;
border: none;
background-color: #2563eb; / Tailwind blue-600 */
color: white;
transition: background-color 0.2s;
}

header .flex.items-center.space-x-4 > button:hover,
header .flex.items-center.space-x-4 > button:focus {
background-color: #1d4ed8; /* Tailwind blue-700 */
outline: none;
}

header .flex.items-center.space-x-4 > button i.material-icons {
font-size: 1.25rem;
}

/* Notification button with badge */
#notificationsBtn {
position: relative;
background: none;
border: none;
color: inherit;
cursor: pointer;
font-size: 1.5rem;
}

#notificationsBtn:hover,
#notificationsBtn:focus {
color: #3b82f6;
outline: none;
}

#notifCount {
position: absolute;
top: 0;
right: 0;
background-color: #dc2626; /* Tailwind red-600 /
color: white;
font-size: 0.625rem; / xs */
border-radius: 9999px;
padding: 0 0.25rem;
line-height: 1rem;
font-weight: 700;
transform: translate(50%, -50%);
}

/* Backdrop */
#backdrop {
position: fixed;
inset: 0;
background-color: rgba(0, 0, 0, 0.7);
z-index: 30;
display: none;
}

/* Show backdrop */
#backdrop.show {
display: block;
}

/* Modals /
.modal {
background-color: #1f2937; / Tailwind gray-800 */
color: #e5e7eb;
border-radius: 8px;
box-shadow: 0 10px 25px rgba(0,0,0,0.7);
padding: 1rem;
position: fixed;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
z-index: 50;
width: 90%;
max-width: 400px;
display: none;
}

.modal.show {
display: block;
}

.modal-header {
font-weight: bold;
font-size: 1.25rem;
margin-bottom: 0.5rem;
position: relative;
}

.modal-close {
cursor: pointer;
position: absolute;
right: 0.5rem;
top: 0;
font-size: 1.5rem;
font-weight: bold;
color: #9ca3af; /* Tailwind gray-400 */
line-height: 1;
}

.modal-close:hover,
.modal-close:focus {
color: #f87171; /* Tailwind red-400 */
outline: none;
}

/* Logout button in modal /
#logoutBtn {
margin-top: 1rem;
padding: 0.5rem 1rem;
background-color: #dc2626; / Tailwind red-600 */
border-radius: 0.375rem;
color: white;
border: none;
cursor: pointer;
font-weight: 600;
transition: background-color 0.2s;
}

#logoutBtn:hover,
#logoutBtn:focus {
background-color: #b91c1c; /* Tailwind red-700 */
outline: none;
}

/* Responsive sidebar /
@media (max-width: 768px) {
.sidebar {
display: none;
}
.sidebar.show {
display: block;
position: fixed;
top: 0;
left: 0;
width: 16rem; / 64 */
height: 100vh;
z-index: 40;
box-shadow: 2px 0 8px rgba(0,0,0,0.7);
overflow-y: auto;
background-color: #111827;
}
.video-grid {
grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
}
}
