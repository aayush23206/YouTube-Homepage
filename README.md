# YouTube-Homepage
Basic project
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='0.9em' font-size='90'>📺</text></svg>">
    <style>
        /* Reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Roboto', sans-serif;
            background-color: #0f0f0f;
            color: #f1f1f1;
            overflow-x: hidden;
        }

        header {
            background-color: #000;
            position: fixed;
            top: 0;
            width: 100%;
            height: 56px;
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 16px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
        }

        .logo {
            display: flex;
            align-items: center;
            cursor: pointer;
        }

        .logo img {
            height: 20px;
            margin-right: 8px;
        }

        .logo-text {
            font-size: 20px;
            font-weight: 400;
            color: #fff;
            display: block;
        }

        /* Search Bar */
        .search-container {
            display: flex;
            align-items: center;
            flex: 1;
            max-width: 600px;
            margin: 0 16px;
        }

        .search-box {
            display: flex;
            flex: 1;
            background-color: #303030;
            border-radius: 20px;
            overflow: hidden;
            height: 40px;
        }

        .search-input {
            flex: 1;
            padding: 0 16px;
            background-color: transparent;
            border: none;
            color: #fff;
            font-size: 16px;
            outline: none;
        }

        .search-input::placeholder {
            color: #aaa;
        }

        .search-button {
            width: 65px;
            background-color: #404040;
            border: none;
            border-radius: 50%;
            color: #fff;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            margin: 4px;
            transition: background-color 0.2s;
        }

        .search-button:hover {
            background-color: #505050;
        }

        .mic-button {
            width: 40px;
            height: 40px;
            background-color: #303030;
            border: none;
            border-radius: 50%;
            color: #fff;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            margin-left: 8px;
            transition: background-color 0.2s;
        }

        .mic-button:hover {
            background-color: #404040;
        }

        /* Header Icons */
        .header-icons {
            display: flex;
            align-items: center;
            gap: 16px;
        }

        .header-icon {
            background: none;
            border: none;
            color: #fff;
            cursor: pointer;
            padding: 8px;
            border-radius: 50%;
            transition: background-color 0.2s;
        }

        .header-icon:hover {
            background-color: #303030;
        }

        .user-avatar {
            width: 32px;
            height: 32px;
            background-color: #303030;
            border-radius: 50%;
            cursor: pointer;
        }

        /* Sidebar */
        .sidebar {
            position: fixed;
            left: 0;
            top: 56px;
            width: 240px;
            height: calc(100vh - 56px);
            background-color: #0f0f0f;
            overflow-y: auto;
            z-index: 999;
            padding: 8px 0;
        }

        .sidebar-collapsed {
            width: 72px;
        }

        .sidebar-section {
            margin-bottom: 16px;
        }

        .sidebar-item {
            display: flex;
            align-items: center;
            padding: 12px 24px;
            color: #f1f1f1;
            text-decoration: none;
            font-size: 14px;
            cursor: pointer;
            transition: background-color 0.2s;
            position: relative;
        }

        .sidebar-item:hover {
            background-color: #303030;
        }

        .sidebar-item i {
            margin-right: 24px;
            width: 24px;
            text-align: center;
        }

        .sidebar-item.sidebar-active {
            background-color: #272727;
            font-weight: 500;
        }

        .sidebar-item.sidebar-active::before {
            content: '';
            position: absolute;
            left: 0;
            width: 4px;
            height: 100%;
            background-color: #fff;
        }

        .sidebar-divider {
            height: 1px;
            background-color: #303030;
            margin: 8px 16px;
        }

        .sidebar-heading {
            font-size: 14px;
            font-weight: 500;
            color: #f1f1f1;
            padding: 12px 24px;
            margin-bottom: 4px;
        }

        .signin-section {
            padding: 12px 24px;
        }

        .signin-text {
            font-size: 14px;
            color: #aaa;
            margin-bottom: 12px;
        }

        .signin-button {
            background: none;
            border: 1px solid #3ea6ff;
            color: #3ea6ff;
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 14px;
            transition: background-color 0.2s;
        }

        .signin-button:hover {
            background-color: #3ea6ff;
            color: #fff;
        }

        /* Main Content */
        .main-content {
            margin-left: 240px;
            padding-top: 56px;
            min-height: 100vh;
            background-color: #0f0f0f;
        }

        .main-content.sidebar-collapsed {
            margin-left: 72px;
        }

        /* Chips Navigation */
        .chips-container {
            display: flex;
            gap: 8px;
            padding: 12px 24px;
            overflow-x: auto;
            scrollbar-width: none;
        }

        .chips-container::-webkit-scrollbar {
            display: none;
        }

        .chip {
            background-color: #272727;
            color: #f1f1f1;
            padding: 8px 16px;
            border-radius: 8px;
            cursor: pointer;
            flex-shrink: 0;
            white-space: nowrap;
            font-size: 14px;
            border: 1px solid transparent;
        }

        .chip:hover {
            background-color: #3e3e3e;
        }

        .chip.chip-active {
            background-color: #f1f1f1;
            color: #0f0f0f;
        }

        /* Video Grid */
        .video-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 16px;
            padding: 0 24px 24px;
            max-width: calc(100vw - 264px);
        }

        .video-card {
            background-color: #0f0f0f;
            border-radius: 8px;
            overflow: hidden;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .video-card:hover {
            transform: translateY(-2px);
        }

        .video-thumbnail {
            width: 100%;
            aspect-ratio: 16 / 9;
            object-fit: cover;
            display: block;
        }

        .video-info {
            padding: 12px;
        }

        .video-title {
            font-size: 16px;
            font-weight: 500;
            color: #f1f1f1;
            margin-bottom: 8px;
            line-height: 1.3;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
        }

        .video-meta {
            font-size: 14px;
            color: #aaa;
            line-height: 1.4;
        }

        .video-channel {
            margin-bottom: 4px;
        }

        .video-stats {
            font-size: 12px;
        }

        .channel-avatar {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            margin-right: 12px;
            flex-shrink: 0;
            background-color: #303030;
        }

        /* Responsiveness */
        @media (max-width: 1000px) {
            .video-grid {
                max-width: calc(100vw - 72px);
            }
        }

        @media (max-width: 800px) {
            .sidebar {
                width: 72px;
                padding: 8px;
            }

            .sidebar-item {
                padding: 16px;
                justify-content: center;
                font-size: 10px;
            }

            .sidebar-item i {
                margin: 0;
                font-size: 18px;
            }

            .sidebar-item span {
                display: none;
            }

            .sidebar-heading {
                display: none;
            }

            .signin-section {
                display: none;
            }

            .sidebar-divider {
                margin: 8px;
            }

            .main-content {
                margin-left: 72px;
            }

            .logo-text {
                display: none;
            }

            .search-container {
                max-width: calc(100vw - 200px);
            }

            .header-icons {
                gap: 8px;
            }
        }

        @media (max-width: 500px) {
            .search-container {
                display: none;
            }

            .mobile-search-show .search-container {
                position: absolute;
                top: 56px;
                left: 0;
                right: 0;
                background-color: #000;
                padding: 16px;
                display: flex;
                z-index: 1001;
            }

            .video-grid {
                grid-template-columns: 1fr;
                padding: 0 16px 16px;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="logo">
            <i class="fas fa-bars header-icon toggle-sidebar"></i>
            <img src="https://www.gstatic.com/youtube/img/branding/youtubelogo/svg/youtubelogo.svg" alt="YouTube Logo" style="height: 20px; margin: 0 8px;">
            <span class="logo-text"></span>
        </div>
        <div class="search-container">
            <div class="search-box">
                <input type="text" class="search-input" placeholder="Search">
                <button class="search-button">
                    <i class="fas fa-search"></i>
                </button>
            </div>
            <button class="mic-button">
                <i class="fas fa-microphone"></i>
            </button>
        </div>
        <div class="header-icons">
            <button class="header-icon">
                <i class="fas fa-video"></i>
            </button>
            <button class="header-icon">
                <i class="fas fa-bell"></i>
            </button>
            <div class="user-avatar"></div>
        </div>
    </header>

    <!-- Sidebar -->
    <aside class="sidebar">
        <div class="sidebar-section">
            <a href="#" class="sidebar-item sidebar-active">
                <i class="fas fa-home"></i>
                <span>Home</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-film"></i>
                <span>Shorts</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-bell"></i>
                <span>Subscriptions</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-video"></i>
                <span>You</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-history"></i>
                <span>History</span>
            </a>
        </div>
        
        <div class="sidebar-divider"></div>
        
        <div class="sidebar-section">
            <div class="signin-section">
                <p class="signin-text">Sign in to like videos, comment, and subscribe.</p>
                <button class="signin-button">
                    <i class="fas fa-user-circle"></i> Sign in
                </button>
            </div>
        </div>
        
        <div class="sidebar-divider"></div>
        
        <div class="sidebar-section">
            <h4 class="sidebar-heading">Explore</h4>
            <a href="#" class="sidebar-item">
                <i class="fas fa-fire"></i>
                <span>Trending</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-music"></i>
                <span>Music</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-trophy"></i>
                <span>Gaming</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-newspaper"></i>
                <span>News</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-basketball-ball"></i>
                <span>Sports</span>
            </a>
        </div>
        
        <div class="sidebar-divider"></div>
        
        <div class="sidebar-section">
            <h4 class="sidebar-heading">More from YouTube</h4>
            <a href="#" class="sidebar-item">
                <i class="fas fa-play-circle"></i>
                <span>YouTube Premium</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-music"></i>
                <span>YouTube Music</span>
            </a>
            <a href="#" class="sidebar-item">
                <i class="fas fa-tv"></i>
                <span>YouTube Kids</span>
            </a>
        </div>
    </aside>

    <!-- Main Content -->
    <main class="main-content">
        <div class="chips-container">
            <button class="chip chip-active">All</button>
            <button class="chip">Music</button>
            <button class="chip">JavaScript</button>
            <button class="chip">Computer programming</button>
            <button class="chip">Podcasts</button>
            <button class="chip">Recently uploaded</button>
            <button class="chip">Watched</button>
            <button class="chip">New to you</button>
        </div>
        <div class="video-grid">
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/2da16db8-31bd-46af-ae1e-7cc1b14607b9.png" alt="Cute kitten playing with laser pointer on wooden floor in brightly lit living room">
                <div class="video-info">
                    <h3 class="video-title">Cute Kitten Playing with Laser Pointer</h3>
                    <p class="video-meta">
                        <span class="video-channel">Channel Name</span>
                        <span class="video-stats">1.2M views • 2 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/5edac6b4-f406-4702-a7b7-13926b9f100c.png" alt="Futuristic spaceship landing on snowy mountain peak under starry night sky with aurora lights">
                <div class="video-info">
                    <h3 class="video-title">Epic Sci-Fi Trailer</h3>
                    <p class="video-meta">
                        <span class="video-channel">Movie Channel</span>
                        <span class="video-stats">500K views • 1 week ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/555ea865-0d50-4838-89cc-3af05900bab5.png" alt="Chef preparing sizzling steak with herbs, vegetables, and steam on modern kitchen countertop">
                <div class="video-info">
                    <h3 class="video-title">Grilling the Perfect Steak</h3>
                    <p class="video-meta">
                        <span class="video-channel">Cooking Tips</span>
                        <span class="video-stats">750K views • 3 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/761db6f2-7747-4730-a08a-f1f45fb2d3e6.png" alt="Musician playing electric guitar on stage with colorful lights and cheering crowd in background">
                <div class="video-info">
                    <h3 class="video-title">Rock Concert Highlights</h3>
                    <p class="video-meta">
                        <span class="video-channel">Music Live</span>
                        <span class="video-stats">2M views • 5 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a4800960-e7a7-45f5-b246-1e9e09b91e40.png" alt="Adventurous hiker climbing rugged cliff face surrounded by lush green forest and distant mountain peaks">
                <div class="video-info">
                    <h3 class="video-title">Extreme Hiking Adventure</h3>
                    <p class="video-meta">
                        <span class="video-channel">Outdoor Adventures</span>
                        <span class="video-stats">1.5M views • 1 week ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/2a908db7-717d-4e45-90c1-dc389e43dc38.png" alt="Vintage car speeding on coastal highway with ocean waves crashing and sunset glowing orange and pink">
                <div class="video-info">
                    <h3 class="video-title">Classic Car Road Trip</h3>
                    <p class="video-meta">
                        <span class="video-channel">Auto Channel</span>
                        <span class="video-stats">450K views • 4 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/f9b39ea7-458d-4bca-93dd-687db2eae5fe.png" alt="Dark themed coding tutorial with computer screen showing code in dimly lit room with coffee and books nearby">
                <div class="video-info">
                    <h3 class="video-title">Learn JavaScript in 10 Minutes</h3>
                    <p class="video-meta">
                        <span class="video-channel">Code Academy</span>
                        <span class="video-stats">800K views • 6 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/c012a7d7-1b74-4fa9-a7e0-db0776799a63.png" alt="Dark themed cooking show with chef basting lamb chops in kitchen under spotlight lighting">
                <div class="video-info">
                    <h3 class="video-title">Perfect Lamb Chops Recipe</h3>
                    <p class="video-meta">
                        <span class="video-channel">Culinary Arts</span>
                        <span class="video-stats">1.1M views • 3 days ago</span>
                    </p>
                </div>
            </div>
        </div>
    </main>

    <script>
        // Sidebar toggle
        const toggleSidebar = document.querySelector('.toggle-sidebar');
        const sidebar = document.querySelector('.sidebar');
        const mainContent = document.querySelector('.main-content');

        toggleSidebar.addEventListener('click', () => {
            sidebar.classList.toggle('sidebar-collapsed');
            mainContent.classList.toggle('sidebar-collapsed');
        });

        // Chip navigation
        const chips = document.querySelectorAll('.chip');
        chips.forEach(chip => {
            chip.addEventListener('click', () => {
                chips.forEach(c => c.classList.remove('chip-active'));
                chip.classList.add('chip-active');
            });
        });

        // Video card interaction
        const videoCards = document.querySelectorAll('.video-card');
        videoCards.forEach(card => {
            card.addEventListener('click', () => {
                alert('Playing video... This is a demo');
            });
        });
    </script>
</body>
</html>

/* Reset */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Roboto', sans-serif;
    background-color: #0f0f0f;
    color: #f1f1f1;
    overflow-x: hidden;
}

header {
    background-color: #000;
    position: fixed;
    top: 0;
    width: 100%;
    height: 56px;
    z-index: 1000;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 16px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.logo {
    display: flex;
    align-items: center;
    cursor: pointer;
}

.logo img {
    height: 20px;
    margin-right: 8px;
}

.logo-text {
    font-size: 20px;
    font-weight: 400;
    color: #fff;
}

/* Search Bar */
.search-container {
    display: flex;
    align-items: center;
    flex: 1;
    max-width: 600px;
    margin: 0 16px;
}

.search-box {
    display: flex;
    flex: 1;
    background-color: #303030;
    border-radius: 20px;
    overflow: hidden;
    height: 40px;
}

.search-input {
    flex: 1;
    padding: 0 16px;
    background-color: transparent;
    border: none;
    color: #fff;
    font-size: 16px;
    outline: none;
}

.search-input::placeholder {
    color: #aaa;
}

.search-button {
    width: 65px;
    background-color: #404040;
    border: none;
    border-radius: 50%;
    color: #fff;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 18px;
    margin: 4px;
    transition: background-color 0.2s;
}

.search-button:hover {
    background-color: #505050;
}

.mic-button {
    width: 40px;
    height: 40px;
    background-color: #303030;
    border: none;
    border-radius: 50%;
    color: #fff;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    margin-left: 8px;
    transition: background-color 0.2s;
}

.mic-button:hover {
    background-color: #404040;
}

/* Header Icons */
.header-icons {
    display: flex;
    align-items: center;
    gap: 10px;
}

.header-icon {
    background: none;
    border: none;
    color: #fff;
    cursor: pointer;
    padding: 8px;
    border-radius: 50%;
    transition: background-color 0.2s;
}

.header-icon:hover {
    background-color: #303030;
}

.user-avatar {
    width: 32px;
    height: 32px;
    background-color: #303030;
    border-radius: 50%;
    cursor: pointer;
}

/* Sidebar */
.sidebar {
    position: fixed;
    left: 0;
    top: 56px;
    width: 240px;
    height: calc(100vh - 56px);
    background-color: #0f0f0f;
    overflow-y: auto;
    z-index: 999;
    padding: 8px 0;
}

.sidebar-collapsed {
    width: 72px;
}

.sidebar-item {
    display: flex;
    align-items: center;
    padding: 12px 24px;
    color: #f1f1f1;
    text-decoration: none;
    font-size: 14px;
    cursor: pointer;
    transition: background-color 0.2s;
}

.sidebar-item:hover {
    background-color: #303030;
}

.sidebar-item i {
    margin-right: 24px;
    width: 24px;
    text-align: center;
}

.sidebar-item.sidebar-active {
    background-color: #272727;
    font-weight: 500;
}

.sidebar-item.sidebar-active::before {
    content: '';
    position: absolute;
    left: 0;
    width: 4px;
    height: 100%;
    background-color: #fff;
}

/* Main Content */
.main-content {
    margin-left: 240px;
    padding-top: 56px;
    min-height: 100vh;
    background-color: #0f0f0f;
}

.main-content.sidebar-collapsed {
    margin-left: 72px;
}

/* Chips Navigation */
.chips-container {
    display: flex;
    gap: 8px;
    padding: 12px 24px;
    overflow-x: auto;
    scrollbar-width: none;
}

.chips-container::-webkit-scrollbar {
    display: none;
}

.chip {
    background-color: #272727;
    color: #f1f1f1;
    padding: 8px 16px;
    border-radius: 8px;
    cursor: pointer;
    flex-shrink: 0;
    white-space: nowrap;
    font-size: 14px;
    border: 1px solid transparent;
}

.chip:hover {
    background-color: #3e3e3e;
}

.chip.chip-active {
    background-color: #f1f1f1;
    color: #0f0f0f;
}

/* Video Grid */
.video-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 16px;
    padding: 0 24px 24px;
    max-width: calc(100vw - 264px);
}

.video-card {
    background-color: #0f0f0f;
    border-radius: 8px;
    overflow: hidden;
    cursor: pointer;
    transition: transform 0.2s;
}

.video-card:hover {
    transform: translateY(-2px);
}

.video-thumbnail {
    width: 100%;
    aspect-ratio: 16 / 9;
    object-fit: cover;
    display: block;
}

.video-info {
    padding: 12px;
}

.video-title {
    font-size: 16px;
    font-weight: 500;
    color: #f1f1f1;
    margin-bottom: 8px;
    line-height: 1.3;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

.video-meta {
    font-size: 14px;
    color: #aaa;
    line-height: 1.4;
}

.video-channel {
    margin-bottom: 4px;
}

.video-stats {
    font-size: 12px;
}

.channel-avatar {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    margin-right: 12px;
    flex-shrink: 0;
    background-color: #303030;
}

/* Responsiveness */
@media (max-width: 1000px) {
    .video-grid {
        max-width: calc(100vw - 72px);
    }
}

@media (max-width: 800px) {
    .sidebar {
        width: 72px;
        padding: 8px;
    }

    .sidebar-item {
        padding: 16px;
        justify-content: center;
        font-size: 10px;
    }

    .sidebar-item i {
        margin: 0;
        font-size: 18px;
    }

    .sidebar-item span {
        display: none;
    }

    .main-content {
        margin-left: 72px;
    }

    .logo-text {
        display: none;
    }

    .search-container {
        max-width: calc(100vw - 200px);
    }

    .header-icons {
        gap: 8px;
    }
}

@media (max-width: 500px) {
    .search-container {
        display: none;
    }

    .mobile-search-show .search-container {
        position: absolute;
        top: 56px;
        left: 0;
        right: 0;
        background-color: #000;
        padding: 16px;
        display: flex;
        z-index: 1001;
    }

    .video-grid {
        grid-template-columns: 1fr;
        padding: 0 16px 16px;
    }
}
</content>
</create_file>

<create_file>
<path>YouTube-Homepage-Clone.html</path>
<content>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube</title>
    <link rel="stylesheet" href="styles.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='0.9em' font-size='90'>📺</text></svg>">
</head>
<body>
    <!-- Header -->
    <header>
        <div class="logo">
            <i class="fas fa-bars header-icon toggle-sidebar"></i>
            <img src="https://www.gstatic.com/youtube/img/branding/youtubelogo/svg/youtubelogo.svg" alt="YouTube Logo" class="ml-4">
            <span class="logo-text">YouTube</span>
        </div>
        <div class="search-container">
            <div class="search-box">
                <input type="text" class="search-input" placeholder="Search">
                <button class="search-button">
                    <i class="fas fa-search"></i>
                </button>
            </div>
            <button class="mic-button">
                <i class="fas fa-microphone"></i>
            </button>
        </div>
        <div class="header-icons">
            <button class="header-icon">
                <i class="fas fa-video"></i>
            </button>
            <button class="header-icon">
                <i class="fas fa-bell"></i>
            </button>
            <div class="user-avatar"></div>
        </div>
    </header>

    <!-- Sidebar -->
    <aside class="sidebar">
        <a href="#" class="sidebar-item sidebar-active">
            <i class="fas fa-home"></i>
            <span>Home</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-film"></i>
            <span>Shorts</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-bell"></i>
            <span>Subscriptions</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-video"></i>
            <span>You</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-history"></i>
            <span>History</span>
        </a>
        <hr class="my-4 border-gray-600">
        <div class="px-6 pb-2">
            <p class="text-sm text-gray-400 mb-2">Sign in to like videos, comment, and subscribe.</p>
            <button class="px-4 py-2 border border-blue-500 text-blue-500 rounded-full hover:bg-blue-500 hover:text-white">
                <i class="fas fa-user-circle mr-2"></i> Sign in
            </button>
        </div>
        <hr class="my-4 border-gray-600">
        <h4 class="px-6 py-2 text-sm font-medium text-white">Explore</h4>
        <a href="#" class="sidebar-item">
            <i class="fas fa-fire"></i>
            <span>Trending</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-music"></i>
            <span>Music</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-trophy"></i>
            <span>Gaming</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-newspaper"></i>
            <span>News</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-basketball-ball"></i>
            <span>Sports</span>
        </a>
        <hr class="my-4 border-gray-600">
        <h4 class="px-6 py-2 text-sm font-medium text-white">More from YouTube</h4>
        <a href="#" class="sidebar-item">
            <i class="fas fa-play-circle"></i>
            <span>YouTube Premium</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-music"></i>
            <span>YouTube Music</span>
        </a>
        <a href="#" class="sidebar-item">
            <i class="fas fa-tv"></i>
            <span>YouTube Kids</span>
        </a>
    </aside>

    <!-- Main Content -->
    <main class="main-content">
        <div class="chips-container">
            <button class="chip chip-active">All</button>
            <button class="chip">Music</button>
            <button class="chip">JavaScript</button>
            <button class="chip">Computer programming</button>
            <button class="chip">Podcasts</button>
            <button class="chip">Recently uploaded</button>
            <button class="chip">Watched</button>
            <button class="chip">New to you</button>
        </div>
        <div class="video-grid">
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/593682b2-811d-4806-a417-a540e33b0199.png" alt="Cute kitten playing">
                <div class="video-info">
                    <h3 class="video-title">Cute Kitten Playing with Laser Pointer</h3>
                    <p class="video-meta">
                        <span class="video-channel">Channel Name</span>
                        <span class="video-stats">1.2M views • 2 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/fd4acc0d-d425-41b8-bc3e-948c8ba8780b.png" alt="Sci-fi trailer">
                <div class="video-info">
                    <h3 class="video-title">Epic Sci-Fi Trailer</h3>
                    <p class="video-meta">
                        <span class="video-channel">Movie Channel</span>
                        <span class="video-stats">500K views • 1 week ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/81e433b7-932c-48b6-9c36-aa549782385a.png" alt="Grilling steak">
                <div class="video-info">
                    <h3 class="video-title">Grilling the Perfect Steak</h3>
                    <p class="video-meta">
                        <span class="video-channel">Cooking Tips</span>
                        <span class="video-stats">750K views • 3 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/871563e3-c70a-4eb9-bf31-cda8b4e0ee0c.png" alt="Rock concert">
                <div class="video-info">
                    <h3 class="video-title">Rock Concert Highlights</h3>
                    <p class="video-meta">
                        <span class="video-channel">Music Live</span>
                        <span class="video-stats">2M views • 5 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/8dff511a-3f31-4db6-90b1-2c6e938a1b96.png" alt="Hiking adventure">
                <div class="video-info">
                    <h3 class="video-title">Extreme Hiking Adventure</h3>
                    <p class="video-meta">
                        <span class="video-channel">Outdoor Adventures</span>
                        <span class="video-stats">1.5M views • 1 week ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/7b85b3e9-d3eb-4b11-99ae-5edd5c336756.png" alt="Car road trip">
                <div class="video-info">
                    <h3 class="video-title">Classic Car Road Trip</h3>
                    <p class="video-meta">
                        <span class="video-channel">Auto Channel</span>
                        <span class="video-stats">450K views • 4 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/0046cc55-131d-4e50-8251-5c329fbee903.png" alt="JavaScript tutorial">
                <div class="video-info">
                    <h3 class="video-title">Learn JavaScript in 10 Minutes</h3>
                    <p class="video-meta">
                        <span class="video-channel">Code Academy</span>
                        <span class="video-stats">800K views • 6 days ago</span>
                    </p>
                </div>
            </div>
            <div class="video-card">
                <img class="video-thumbnail" src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/c5c6c445-bd49-462b-a571-2a627a36153e.png" alt="Lamb chops recipe">
                <div class="video-info">
                    <h3 class="video-title">Perfect Lamb Chops Recipe</h3>
                    <p class="video-meta">
                        <span class="video-channel">Culinary Arts</span>
                        <span class="video-stats">1.1M views • 3 days ago</span>
                    </p>
                </div>
            </div>
            <!-- Add more videos as needed for demonstration -->
        </div>
    </main>

    <script>
        // Sidebar toggle
        const toggleSidebar = document.querySelector('.toggle-sidebar');
        const sidebar = document.querySelector('.sidebar');
        const mainContent = document.querySelector('.main-content');

        toggleSidebar.addEventListener('click', () => {
            sidebar.classList.toggle('sidebar-collapsed');
            mainContent.classList.toggle('sidebar-collapsed');
        });

        // Chip navigation
        const chips = document.querySelectorAll('.chip');
        chips.forEach(chip => {
            chip.addEventListener('click', () => {
                chips.forEach(c => c.classList.remove('chip-active'));
                chip.classList.add('chip-active');
            });
        });

        // Video card interaction
        const videoCards = document.querySelectorAll('.video-card');
        videoCards.forEach(card => {
            card.addEventListener('click', () => {
                alert('Playing video... This is a demo');
            });
        });
    </script>
</body>
</html>
</content>
</create_file>
</content>
</create_file>
