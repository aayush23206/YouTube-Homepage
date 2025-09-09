<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube - Homepage</title>
    <!-- Import Font Awesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        /* General Reset and Body */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        :root {
            --bg-color: #f9f9f9;
            --text-color: #333;
            --card-bg: #fff;
            --border-color: #e0e0e0;
            --hover-bg: #f0f0f0;
            --sidebar-bg: #fff;
            --header-bg: #fff;
        }
        body {
            font-family: 'Roboto', Arial, sans-serif;
            background: var(--bg-color);
            color: var(--text-color);
            overflow-x: hidden;
            transition: background 0.3s, color 0.3s;
        }
        body.dark {
            --bg-color: #181818;
            --text-color: #f1f1f1;
            --card-bg: #212121;
            --border-color: #303030;
            --hover-bg: #333;
            --sidebar-bg: #212121;
            --header-bg: #212121;
        }

        /* Header */
        .header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: var(--header-bg);
            display: flex;
            align-items: center;
            padding: 0 16px;
            height: 56px;
            border-bottom: 1px solid var(--border-color);
            z-index: 1000;
        }
        .header-left {
            display: flex;
            align-items: center;
            flex: 0 0 220px;
        }
        .menu-toggle {
            background: none;
            border: none;
            font-size: 18px;
            color: var(--text-color);
            margin-right: 24px;
            cursor: pointer;
        }
        .logo {
            display: flex;
            align-items: center;
            text-decoration: none;
        }
        .logo i {
            color: #ff0000;
            font-size: 24px;
            margin-right: 8px;
        }
        .logo span {
            font-size: 20px;
            font-weight: bold;
            color: var(--text-color);
        }
        .header-center {
            flex: 1;
            display: flex;
            justify-content: center;
        }
        .search-bar {
            display: flex;
            width: 100%;
            max-width: 600px;
        }
        .search-input {
            flex: 1;
            padding: 0 16px;
            height: 40px;
            border: 1px solid var(--border-color);
            border-right: none;
            border-radius: 40px 0 0 40px;
            font-size: 16px;
            outline: none;
            background: var(--card-bg);
            color: var(--text-color);
        }
        .search-button {
            width: 64px;
            height: 40px;
            background: var(--hover-bg);
            border: 1px solid var(--border-color);
            border-left: none;
            border-radius: 0 40px 40px 0;
            cursor: pointer;
        }
        .search-button i {
            color: var(--text-color);
            font-size: 18px;
        }
        .header-right {
            display: flex;
            align-items: center;
            flex: 0 0 220px;
            justify-content: flex-end;
        }
        .header-icon {
            background: none;
            border: none;
            font-size: 20px;
            color: var(--text-color);
            margin-left: 16px;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: background 0.2s;
        }
        .header-icon:hover {
            background: var(--hover-bg);
        }
        .upload-btn i {
            color: var(--text-color);
        }

        /* Options Modal */
        .options-modal {
            display: none;
            position: fixed;
            top: 60px;
            right: 10px;
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
            width: 200px;
            z-index: 1100;
            padding: 0;
        }
        .options-modal.show {
            display: block;
        }
        .option-item {
            display: block;
            padding: 12px 16px;
            color: var(--text-color);
            text-decoration: none;
            font-size: 14px;
            transition: background 0.2s;
        }
        .option-item:hover {
            background: var(--hover-bg);
        }

        /* Sidebar */
        .sidebar {
            position: fixed;
            left: 0;
            top: 56px;
            width: 220px;
            height: calc(100vh - 56px);
            background: var(--sidebar-bg);
            border-right: 1px solid var(--border-color);
            overflow-y: auto;
            transition: transform 0.3s;
            z-index: 999;
        }
        .sidebar.hidden {
            transform: translateX(-220px);
        }
        .sidebar-item {
            display: flex;
            align-items: center;
            padding: 16px 20px;
            cursor: pointer;
            text-decoration: none;
            color: var(--text-color);
            font-size: 14px;
            transition: background 0.2s;
        }
        .sidebar-item:hover {
            background: var(--hover-bg);
        }
        .sidebar-item i {
            margin-right: 24px;
            width: 20px;
            text-align: center;
        }
        .sidebar-divider {
            height: 1px;
            background: var(--border-color);
            margin: 8px 0;
        }

        /* Main Content */
        .main-content {
            margin-left: 220px;
            margin-top: 56px;
            padding: 24px 24px 0;
            transition: margin-left 0.3s;
        }
        .main-content.expanded {
            margin-left: 0;
        }
        .categories {
            display: flex;
            gap: 12px;
            margin-bottom: 24px;
            overflow-x: auto;
            white-space: nowrap;
        }
        .category {
            background: var(--hover-bg);
            padding: 8px 16px;
            border-radius: 16px;
            font-size: 14px;
            cursor: pointer;
            transition: background 0.2s;
            white-space: nowrap;
            color: var(--text-color);
        }
        .category:hover {
            background: var(--border-color);
        }
        .category.active {
            background: #ff0000;
            color: #fff;
        }
        .videos {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 16px;
        }
        .video-card {
            background: var(--card-bg);
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            cursor: pointer;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .video-card:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
        }
        .video-thumb {
            position: relative;
            overflow: hidden;
        }
        .video-thumb img {
            width: 100%;
            height: 180px;
            object-fit: cover;
        }
        .video-duration {
            position: absolute;
            bottom: 8px;
            right: 8px;
            background: rgba(0,0,0,0.8);
            color: #fff;
            padding: 2px 6px;
            border-radius: 4px;
            font-size: 12px;
        }
        .video-info {
            padding: 12px 16px;
        }
        .video-title {
            font-size: 16px;
            font-weight: 500;
            line-height: 1.4;
            margin-bottom: 8px;
            color: var(--text-color);
        }
        .channel-info {
            display: flex;
            align-items: center;
        }
        .channel-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            margin-right: 12px;
            object-fit: cover;
        }
        .channel-details p {
            font-size: 14px;
            color: var(--text-color);
            line-height: 1.3;
        }
        .channel-details .channel-name {
            color: var(--text-color);
        }
        .channel-details p:last-child {
            color: #aaa;
        }

        /* Dark mode specific adjustments */
        body.dark .channel-details p:last-child {
            color: #ccc;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-220px);
            }
            .sidebar.hidden {
                transform: translateX(-220px);
            }
            .main-content {
                margin-left: 0;
            }
            .options-modal {
                width: 150px;
            }
        }

        /* Dark mode toggle */
        .dark-mode-toggle {
            margin-left: 16px;
        }
        .dark-mode-toggle i {
            color: var(--text-color);
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header class="header">
        <div class="header-left">
            <button class="menu-toggle" id="menu-toggle"><i class="fas fa-bars"></i></button>
            <a class="logo" href="#">
                <i class="fab fa-youtube"></i>
                <span>YouTube</span>
            </a>
        </div>
        <div class="header-center">
            <div class="search-bar">
                <input type="text" class="search-input" placeholder="Search">
                <button class="search-button"><i class="fas fa-search"></i></button>
            </div>
        </div>
        <div class="header-right">
            <button class="header-icon dark-mode-toggle" id="dark-mode-toggle"><i class="fas fa-moon"></i></button>
            <button class="header-icon" id="upload-btn"><i class="fas fa-video"></i></button>
            <button class="header-icon" id="apps-btn"><i class="fas fa-th"></i></button>
            <button class="header-icon"><i class="fas fa-bell"></i></button>
            <button class="header-icon">
                <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/259a4be8-8b76-4162-83b3-82c77865271c.png" alt="Default user profile picture showing a circular avatar with initials in white on a blue background" class="channel-avatar">
            </button>
        </div>
        <!-- Options Modal -->
        <div class="options-modal" id="options-modal">
            <a class="option-item" href="#" id="account-settings">Account Settings</a>
            <a class="option-item" href="#" id="privacy">Privacy</a>
            <a class="option-item" href="#" id="help">Help & Support</a>
            <a class="option-item" href="#" id="feedback">Send Feedback</a>
        </div>
    </header>

    <!-- Sidebar -->
    <aside class="sidebar" id="sidebar">
        <a class="sidebar-item active" href="#"><i class="fas fa-home"></i>Home</a>
        <a class="sidebar-item" href="#"><i class="fab fa-youtube"></i>Shorts</a>
        <a class="sidebar-item" href="#"><i class="fas fa-compass"></i>Explore</a>
        <div class="sidebar-divider"></div>
        <a class="sidebar-item" href="#"><i class="fas fa-list"></i>Subscriptions</a>
        <div class="sidebar-divider"></div>
        <a class="sidebar-item" href="#"><i class="fas fa-clock"></i>Watch Later</a>
        <a class="sidebar-item" href="#"><i class="fas fa-thumbs-up"></i>Liked Videos</a>
        <a class="sidebar-item" href="#"><i class="fas fa-history"></i>History</a>
        <a class="sidebar-item" href="#"><i class="fas fa-folder"></i>Library</a>
        <div class="sidebar-divider"></div>
        <a class="sidebar-item" href="#"><i class="fas fa-plus"></i>Downloads</a>
        <a class="sidebar-item" href="#"><i class="fas fa-question"></i>Help & Feedback</a>
    </aside>

    <!-- Main Content -->
    <main class="main-content" id="main-content">
        <!-- Categories -->
        <div class="categories">
            <div class="category active" data-category="all">All</div>
            <div class="category" data-category="music">Music</div>
            <div class="category" data-category="gaming">Gaming</div>
            <div class="category" data-category="news">News</div>
            <div class="category" data-category="technology">Technology</div>
            <div class="category" data-category="sports">Sports</div>
            <div class="category" data-category="comedy">Comedy</div>
            <div class="category" data-category="cooking">Cooking</div>
        </div>

        <!-- Videos Grid -->
        <div class="videos">
            <div class="video-card" data-category="music">
                <div class="video-thumb">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/4f728ddd-e59e-4c76-9e86-2c2af4056ba3.png" alt="A vibrant music video scene with a guitarist playing passionately on stage under colorful spotlights with an enthusiastic crowd in the background, high energy performance in a live concert setting">
                    <span class="video-duration">3:45</span>
                </div>
                <div class="video-info">
                    <h3 class="video-title">Epic Guitar Solo Live Performance</h3>
                    <div class="channel-info">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/c5c5230e-eb23-435b-8a70-8616a5dd5ab1.png" alt="Channel avatar for Rock Legends, featuring a stylized guitar icon in red on a white circle background" class="channel-avatar">
                        <div class="channel-details">
                            <p class="channel-name">Rock Legends</p>
                            <p>1.2M views • 2 days ago</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="video-card" data-category="gaming">
                <div class="video-thumb">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/b12a633f-0a83-4f62-b753-fbec590e7fea.png" alt="Futuristic gaming setup with a high-definition monitor displaying an intense battle scene from a first-person shooter game, surrounded by RGB-lit peripherals and a gamer's hands on keyboard and mouse">
                    <span class="video-duration">12:30</span>
                </div>
                <div class="video-info">
                    <h3 class="video-title">Ultimate Gaming Setup Tour 2023</h3>
                    <div class="channel-info">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/4203d574-4f91-46fc-b01b-2a99b425296d.png" alt="Channel avatar for Tech Gamer, showing a pixelated controller icon in green on a black square background" class="channel-avatar">
                        <div class="channel-details">
                            <p class="channel-name">Tech Gamer</p>
                            <p>500K views • 5 hours ago</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="video-card" data-category="news">
                <div class="video-thumb">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/b49cc15f-f700-47f6-8269-1422a82c2cce.png" alt="Breaking news broadcast with anchor in suit reporting on global events, overlaid with dramatic headlines and city skyline footage at night">
                    <span class="video-duration">5:20</span>
                </div>
                <div class="video-info">
                    <h3 class="video-title">Top Headlines: Economy Shocks World Markets</h3>
                    <div class="channel-info">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/e1268a5e-5bc0-45da-8678-59f5b4de961e.png" alt="Channel avatar for Global News Network, featuring a globe icon in blue on a white earth background" class="channel-avatar">
                        <div class="channel-details">
                            <p class="channel-name">Global News Network</p>
                            <p>3M views • 1 hour ago</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="video-card" data-category="technology">
                <div class="video-thumb">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/49dc9c10-d69a-4567-a55c-b84f6b2bb9fc.png" alt="Innovative smartphone demonstration with close-up shots of advanced camera features in a modern lab setting, showing crystal-clear photography and augmented reality applications">
                    <span class="video-duration">8:15</span>
                </div>
                <div class="video-info">
                    <h3 class="video-title">New Smartphone Revolutionizes Photography</h3>
                    <div class="channel-info">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/0d1eb1da-ad23-46e4-b5ad-1bab479fca8d.png" alt="Channel avatar for Tech Innovation, displaying a stylized smartphone icon in silver on a black background" class="channel-avatar">
                        <div class="channel-details">
                            <p class="channel-name">Tech Innovation</p>
                            <p>750K views • 3 days ago</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="video-card" data-category="cooking">
                <div class="video-thumb">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/586f66c5-9d21-4036-b2f9-5106b54be414.png" alt="Calm cooking tutorial in a cozy kitchen with fresh ingredients, featuring step-by-step mixing of dough for homemade bread with soft warm lighting">
                    <span class="video-duration">10:45</span>
                </div>
                <div class="video-info">
                    <h3 class="video-title">Easy Homemade Artisan Bread Recipe</h3>
                    <div class="channel-info">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/3c22b3b0-1a91-4044-bfa0-0bd25a23af4a.png" alt="Channel avatar for Home Chef, showing a oven mitt icon in orange on a cooking pot background" class="channel-avatar">
                        <div class="channel-details">
                            <p class="channel-name">Home Chef</p>
                            <p>2.5M views • 1 week ago</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="video-card" data-category="comedy">
                <div class="video-thumb">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/12846955-fff9-40d5-b478-f09f15808db4.png" alt="Humorous comedy sketch with actors dressed in ridiculous costumes performing slapstick jokes in a colorful stage setting with audience laughter">
                    <span class="video-duration">4:05</span>
                </div>
                <div class="video-info">
                    <h3 class="video-title">Hilarious Comedy Blooper Reel</h3>
                    <div class="channel-info">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/4723d6ce-a4ef-4a1c-9653-90231a2ba19d.png" alt="Channel avatar for Funny Moments, featuring a laughing face icon in yellow on a blue circle" class="channel-avatar">
                        <div class="channel-details">
                            <p class="channel-name">Funny Moments</p>
                            <p>1.8M views • 4 days ago</p>
                        </div>
                    </div>
                </div>
            </div>
            <!-- Add more video cards as needed -->
        </div>
    </main>

    <script>
        // Basic JS for sidebar toggle
        const menuToggle = document.getElementById('menu-toggle');
        const sidebar = document.getElementById('sidebar');
        const mainContent = document.getElementById('main-content');

        menuToggle.addEventListener('click', () => {
            sidebar.classList.toggle('hidden');
            mainContent.classList.toggle('expanded');
        });

        // Dark mode toggle
        const darkModeToggle = document.getElementById('dark-mode-toggle');
        darkModeToggle.addEventListener('click', () => {
            document.body.classList.toggle('dark');
            const icon = darkModeToggle.querySelector('i');
            if (document.body.classList.contains('dark')) {
                icon.className = 'fas fa-sun';
                localStorage.setItem('darkMode', 'enabled');
            } else {
                icon.className = 'fas fa-moon';
                localStorage.setItem('darkMode', 'disabled');
            }
        });

        // Load dark mode on page load
        if (localStorage.getItem('darkMode') === 'enabled') {
            document.body.classList.add('dark');
            darkModeToggle.querySelector('i').className = 'fas fa-sun';
        }

        // Options modal (Apps button)
        const appsBtn = document.getElementById('apps-btn');
        const optionsModal = document.getElementById('options-modal');
        appsBtn.addEventListener('click', () => {
            optionsModal.classList.toggle('show');
        });

        // Close modal when clicking outside
        document.addEventListener('click', (e) => {
            if (!appsBtn.contains(e.target) && !optionsModal.contains(e.target)) {
                optionsModal.classList.remove('show');
            }
        });

        // Make categories clickable (filter videos)
        const categories = document.querySelectorAll('.category');
        const cards = document.querySelectorAll('.video-card');
        categories.forEach(cat => {
            cat.addEventListener('click', () => {
                categories.forEach(c => c.classList.remove('active'));
                cat.classList.add('active');
                const filter = cat.dataset.category;
                cards.forEach(card => {
                    if (filter === 'all' || card.dataset.category === filter) {
                        card.style.display = 'block';
                    } else {
                        card.style.display = 'none';
                    }
                });
            });
        });
    </script>
</body>
</html>
</content>
</create_file>
<script src="script.js"></script>
// Profile Menu Toggle
const profileBtn = document.getElementById("profileBtn");
const profileMenu = document.getElementById("profileMenu");

profileBtn.addEventListener("click", () => {
  profileMenu.style.display =
    profileMenu.style.display === "block" ? "none" : "block";
});

// Close profile menu when clicking outside
window.addEventListener("click", (e) => {
  if (!profileBtn.contains(e.target) && !profileMenu.contains(e.target)) {
    profileMenu.style.display = "none";
  }
});

// Dark/Light Mode Toggle
const themeToggle = document.getElementById("themeToggle");
const body = document.body;

themeToggle.addEventListener("click", () => {
  body.classList.toggle("dark-mode");
  body.classList.toggle("light-mode");
  themeToggle.textContent = body.classList.contains("dark-mode") ? "☀️" : "🌙";
});
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
  }
  
  body.light-mode {
    background-color: #f9f9f9;
    color: #000;
  }
  
  body.dark-mode {
    background-color: #181818;
    color: #fff;
  }
  
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    background: white;
    border-bottom: 1px solid #ddd;
    position: sticky;
    top: 0;
    z-index: 100;
  }
  
  body.dark-mode .header {
    background: #202020;
    border-bottom: 1px solid #333;
  }
  
  .logo {
    font-size: 22px;
    font-weight: bold;
    color: red;
  }
  
  .search-bar {
    display: flex;
    flex: 1;
    max-width: 500px;
    margin: 0 20px;
  }
  
  .search-bar input {
    flex: 1;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 2px 0 0 2px;
  }
  
  .search-bar button {
    padding: 8px 12px;
    border: 1px solid #ccc;
    border-left: none;
    background: #f8f8f8;
    cursor: pointer;
  }
  
  .header-icons {
    display: flex;
    align-items: center;
    gap: 15px;
  }
  
  .profile {
    background: #ff0000;
    color: white;
    width: 35px;
    height: 35px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    cursor: pointer;
  }
  
  /* Profile Menu */
  .profile-menu {
    display: none;
    position: absolute;
    top: 60px;
    right: 20px;
    background: white;
    border: 1px solid #ddd;
    width: 250px;
    padding: 10px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    z-index: 100;
  }
  
  body.dark-mode .profile-menu {
    background: #202020;
    border: 1px solid #333;
  }
  
  .profile-menu a {
    display: block;
    padding: 8px;
    text-decoration: none;
    color: inherit;
    font-size: 14px;
  }
  
  .profile-menu a:hover {
    background: #f0f0f0;
  }
  
  body.dark-mode .profile-menu a:hover {
    background: #333;
  }
  
  .profile-info {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 0;
  }
  
  .profile-icon {
    background: #ff0000;
    color: white;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
  }
  
  .profile-info h3 {
    margin-bottom: 2px;
  }
  
  /* Container */
  .container {
    display: flex;
  }
  
  /* Sidebar */
  .sidebar {
    width: 200px;
    background: white;
    border-right: 1px solid #ddd;
    height: calc(100vh - 50px);
    padding-top: 20px;
    position: sticky;
    top: 50px;
  }
  
  .sidebar a {
    display: block;
    padding: 10px 20px;
    text-decoration: none;
    color: inherit;
  }
  
  .sidebar a:hover {
    background: #f0f0f0;
  }
  
  body.dark-mode .sidebar {
    background: #202020;
    border-right: 1px solid #333;
  }
  
  body.dark-mode .sidebar a:hover {
    background: #333;
  }
  
  /* Video Section */
  .video-section {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 20px;
    padding: 20px;
    flex: 1;
  }
  
  .video-card {
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease;
  }
  
  .video-card:hover {
    transform: scale(1.02);
  }
  
  body.dark-mode .video-card {
    background: #202020;
    box-shadow: 0 2px 5px rgba(255, 255, 255, 0.1);
  }
  
  .video-card img {
    width: 100%;
    display: block;
  }
  
  .video-info {
    display: flex;
    padding: 10px;
    gap: 10px;
  }
  
  .channel-logo {
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
  
  .video-info h3 {
    font-size: 16px;
    margin-bottom: 5px;
  }
  
  .video-info p {
    color: #606060;
    font-size: 14px;
  }
  
  body.dark-mode .video-info p {
    color: #aaa;
  }
  
  /* Responsive */
  @media (max-width: 768px) {
    .sidebar {
      display: none;
    }
    .video-section {
      grid-template-columns: 1fr 1fr;
    }
  }
  
  @media (max-width: 480px) {
    .video-section {
      grid-template-columns: 1fr;
    }
    .search-bar {
      display: none;
    }
  }
  
