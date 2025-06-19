<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Zomato Clone - Simple Modern</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=Material+Icons" rel="stylesheet" />
  <style>
    /* Reset and base */
    *, *::before, *::after {
      box-sizing: border-box;
    }
    body {
      margin: 0;      
      font-family: 'Inter', sans-serif;
      background: #fafafa;
      color: #374151;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      line-height: 1.5;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      overflow-x: hidden;
    }
    a {
      color: inherit;
      text-decoration: none;
      cursor: pointer;
    }
    ul {
      list-style: none;
      margin: 0;
      padding: 0;
    }
    button {
      cursor: pointer;
      border: none;
      background: transparent;
    }
    /* Material Icons */
    .material-icons {
      font-family: 'Material Icons';
      font-weight: normal;
      font-style: normal;
      font-size: 20px;
      line-height: 1;
      letter-spacing: normal;
      text-transform: none;
      display: inline-block;
      white-space: nowrap;
      direction: ltr;
      -webkit-font-feature-settings: 'liga';
      -webkit-font-smoothing: antialiased;
      vertical-align: middle;
      user-select: none;
    }
    /* Glassmorphism colors and shadows */
    :root {
      --glass-bg: rgba(255 255 255 / 0.75);
      --glass-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.1);
      --primary-color: #d32f2f;
      --secondary-color: #f44336;
      --gray-light: #f3f4f6;
      --gray-medium: #9ca3af;
      --gray-dark: #374151;
      --text-color: #1f2937;
      --badge-bg: #ef4444;
      --sidebar-bg: rgba(255 255 255 / 0.85);
    }
    /* Utility classes */
    .hidden {
      display: none !important;
    }

    /* Scrollbar custom */
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #f3f4f6;
      border-radius: 8px;
    }
    ::-webkit-scrollbar-thumb {
      background-color: #d32f2f;
      border-radius: 8px;
      border: 2px solid #f3f4f6;
    }
    
    /* Header */
    header {
      position: sticky;
      top: 0;
      z-index: 100;
      height: 64px;
      background: var(--glass-bg);
      backdrop-filter: blur(16px);
      box-shadow: var(--glass-shadow);
      display: flex;
      align-items: center;
      padding: 0 24px;
      border-bottom: 1px solid rgba(0,0,0,0.05);
      user-select:none;
    }
    .header-left {
      display: flex;
      align-items: center;
      gap: 16px;
    }
    .logo {
      font-weight: 700;
      font-size: clamp(1.3rem, 2vw, 1.8rem);
      color: var(--primary-color);
      letter-spacing: -0.02em;
      user-select:none;
    }
    .material-icons.menu-toggle {
      font-size: 28px;
      cursor: pointer;
      display: none;
      color: var(--primary-color);
    }

    /* Search */
    .header-search {
      flex-grow: 1;
      margin: 0 24px;
      position: relative;
      max-width: 460px;
    }
    .header-search input {
      width: 100%;
      padding: 10px 44px 10px 16px;
      border-radius: 12px;
      border: 1.5px solid var(--gray-light);
      font-size: 16px;
      outline-offset: 2px;
      transition: border-color 0.3s ease;
    }
    .header-search input:focus {
      border-color: var(--primary-color);
      box-shadow: 0 0 8px var(--primary-color);
    }
    .header-search .material-icons.search-icon {
      position: absolute;
      right: 12px;
      top: 50%;
      transform: translateY(-50%);
      font-size: 24px;
      color: var(--gray-medium);
      pointer-events: none;
    }
    /* User controls */
    .header-right {
      display: flex;
      align-items: center;
      gap: 16px;
    }
    .header-btn {
      background: var(--primary-color);
      color: white;
      border-radius: 32px;
      padding: 8px 20px;
      font-weight: 600;
      font-size: 14px;
      transition: background-color 0.3s ease;
      user-select:none;
    }
    .header-btn:hover,
    .header-btn:focus {
      background: var(--secondary-color);
      outline: none;
    }
    /* Sidebar */
    .sidebar {
      position: fixed;
      top: 64px;
      bottom: 0;
      left: 0;
      width: 280px;
      background: var(--sidebar-bg);
      backdrop-filter: blur(16px);
      box-shadow: var(--glass-shadow);
      padding: 24px 0;
      overflow-y: auto;
      transition: transform 0.3s ease;
      z-index: 90;
      display: flex;
      flex-direction: column;
    }
    .sidebar.hide {
      transform: translateX(-100%);
      pointer-events: none;
    }
    .sidebar nav {
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      gap: 8px;
      padding: 0 16px;
    }
    .nav-item {
      display: flex;
      align-items: center;
      gap: 16px;
      padding: 12px 16px;
      border-radius: 12px;
      font-weight: 600;
      color: var(--text-color);
      transition: background-color 0.3s ease, color 0.3s ease;
      user-select:none;
    }
    .nav-item:hover,
    .nav-item:focus {
      background-color: var(--primary-color);
      color: white;
      outline: none;
    }
    .nav-item.active {
      background-color: var(--primary-color);
      color: white;
    }
    .nav-item .material-icons {
      font-size: 24px;
    }
    /* Notification badge */
    .badge {
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: var(--badge-bg);
      color: white;
      border-radius: 12px;
      padding: 2px 8px;
      font-size: 12px;
      font-weight: 700;
      margin-left: auto;
      user-select:none;
    }
    /* Main content */
    main {
      margin-left: 280px;
      flex-grow: 1;
      min-height: calc(100vh - 64px);
      padding: 24px 32px 72px;
      transition: margin-left 0.3s ease;
      background: #fefefe;
      display: flex;
      flex-direction: column;
    }
    main.hide-sidebar {
      margin-left: 0;
    }
    .welcome-header {
      font-weight: 700;
      font-size: clamp(1.75rem, 3vw, 2.5rem);
      margin-bottom: 32px;
      user-select:none;
    }
    .search-bar {
      margin-bottom: 32px;
      max-width: 500px;
    }
    .search-bar input {
      width: 100%;
      padding: 12px 16px;
      font-size: 18px;
      border-radius: 12px;
      border: 1.5px solid var(--gray-light);
      outline-offset: 2px;
      transition: border-color 0.3s ease;
      user-select:none;
    }
    .search-bar input:focus {
      border-color: var(--primary-color);
      box-shadow: 0 0 8px var(--primary-color);
    }
    /* Cards grid */
    .card-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(280px,1fr));
      gap: 24px;
    }
    /* Each restaurant card */
    .restaurant-card {
      background: white;
      border-radius: 16px;
      box-shadow: 0 4px 8px rgb(0 0 0 / 0.05);
      overflow: hidden;
      display: flex;
      flex-direction: column;
      transition: box-shadow 0.3s ease, transform 0.3s ease;
      cursor: pointer;
      user-select:none;
    }
    .restaurant-card:hover,
    .restaurant-card:focus-within {
      box-shadow: 0 12px 24px rgb(211 47 47 / 0.3);
      transform: translateY(-4px);
      outline: none;
    }
    .restaurant-image {
      width: 100%;
      height: 160px;
      object-fit: cover;
      flex-shrink: 0;
    }
    .card-content {
      padding: 16px 20px;
      display: flex;
      flex-direction: column;
      gap: 8px;
      flex-grow: 1;
    }
    .restaurant-title {
      font-weight: 700;
      font-size: 1.25rem;
      color: var(--text-color);
      user-select:none;
    }
    .restaurant-info {
      color: var(--gray-medium);
      font-size: 0.9rem;
      display: flex;
      align-items: center;
      gap: 12px;
      font-weight: 500;
    }
    .restaurant-info .material-icons.star {
      font-size: 18px;
      color: #fbbf24; /* amber-400 for star */
      user-select:none;
    }
    /* Footer */
    footer {
      background: var(--glass-bg);
      backdrop-filter: blur(16px);
      box-shadow: var(--glass-shadow);
      color: var(--text-color);
      padding: 16px 32px;
      font-size: 14px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-shrink: 0;
      border-top: 1px solid rgba(0,0,0,0.05);
      user-select:none;
    }
    .footer-links {
      display: flex;
      gap: 20px;
    }
    .footer-link {
      color: var(--text-color);
      text-decoration: none;
      transition: color 0.3s ease;
    }
    .footer-link:hover,
    .footer-link:focus {
      color: var(--primary-color);
      outline: none;
    }
    /* Social icons */
    .footer-social {
      display: flex;
      gap: 16px;
    }
    .footer-social a {
      color: var(--text-color);
      font-size: 20px;
      transition: color 0.3s ease;
      display: inline-flex;
      align-items: center;
      justify-content: center;
    }
    .footer-social a:hover,
    .footer-social a:focus {
      color: var(--primary-color);
      outline: none;
    }

    /* Responsive */
    @media (max-width: 1023px) {
      main {
        margin-left: 0;
        padding: 24px 16px 100px;
      }
      .sidebar {
        width: 280px;
        position: fixed;
        top: 64px;
        transform: translateX(-100%);
        transition: transform 0.3s ease;
        box-shadow: 8px 0 30px rgba(0,0,0,0.1);
        pointer-events: none;
      }
      .sidebar.show {
        transform: translateX(0);
        pointer-events: auto;
      }
      header .material-icons.menu-toggle {
        display: inline-flex;
      }
    }
    @media (max-width: 767px) {
      footer {
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        z-index: 100;
        border-top: 1px solid rgba(0,0,0,0.1);
        padding: 12px 20px;
        font-size: 13px;
      }
      main {
        padding-bottom: 120px;
      }
      .header-search {
        display: none;
      }
      .header-right {
        display: none;
      }
    }
  </style>
</head>
<body>
  <header>
    <div class="header-left">
      <span class="material-icons menu-toggle" role="button" aria-label="Toggle menu" tabindex="0" id="menu-toggle">menu</span>
      <a href="#" class="logo" aria-label="Zomato homepage">Zomato</a>
    </div>
    <div class="header-search" role="search">
      <input type="search" placeholder="Search for restaurants or dishes" aria-label="Search restaurants or dishes" />
      <span class="material-icons search-icon" aria-hidden="true">search</span>
    </div>
    <div class="header-right">
      <button class="header-btn" aria-label="Log in to your account">Login</button>
      <button class="header-btn" aria-label="Sign up for a new account">Sign up</button>
    </div>
  </header>

  <aside class="sidebar" id="sidebar" aria-label="Primary navigation">
    <nav>
      <a href="#" class="nav-item active" tabindex="0" aria-current="page">
        <span class="material-icons" aria-hidden="true">home</span> Home
      </a>
      <a href="#" class="nav-item" tabindex="0">
        <span class="material-icons" aria-hidden="true">restaurant_menu</span> Restaurants
        <span class="badge" aria-label="3 new notifications">3</span>
      </a>
      <a href="#" class="nav-item" tabindex="0">
        <span class="material-icons" aria-hidden="true">local_offer</span> Offers
      </a>
      <a href="#" class="nav-item" tabindex="0">
        <span class="material-icons" aria-hidden="true">favorite</span> Favorites
      </a>
      <a href="#" class="nav-item" tabindex="0">
        <span class="material-icons" aria-hidden="true">person</span> Profile
      </a>
      <a href="#" class="nav-item" tabindex="0">
        <span class="material-icons" aria-hidden="true">settings</span> Settings
      </a>
    </nav>
  </aside>

  <main id="main-content" tabindex="-1">
    <h1 class="welcome-header">Discover restaurants near you</h1>
    <section class="card-grid" aria-label="Featured restaurants">
      <article class="restaurant-card" tabindex="0" aria-labelledby="res-1-title" role="region">
        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/367599e6-9831-47e4-9961-c58341f2a9f4.png" alt="Interior view of a cozy Italian Pizzeria" class="restaurant-image" loading="lazy" />
        <div class="card-content">
          <h2 id="res-1-title" class="restaurant-title">Mama Mia Pizzeria</h2>
          <div class="restaurant-info">
            <span class="material-icons star" aria-hidden="true">star</span>
            <span>4.6</span>
            <span>·</span>
            <span>Italian, Pizza</span>
            <span>·</span>
            <span>$$</span>
          </div>
        </div>
      </article>

      <article class="restaurant-card" tabindex="0" aria-labelledby="res-2-title" role="region">
        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/5ee1e072-4f70-4229-bf78-3e54cace0722.png" alt="Close-up of fresh sushi dishes on a wooden table" class="restaurant-image" loading="lazy" />
        <div class="card-content">
          <h2 id="res-2-title" class="restaurant-title">Sakura Sushi Bar</h2>
          <div class="restaurant-info">
            <span class="material-icons star" aria-hidden="true">star</span>
            <span>4.8</span>
            <span>·</span>
            <span>Japanese, Sushi</span>
            <span>·</span>
            <span>$$$</span>
          </div>
        </div>
      </article>

      <article class="restaurant-card" tabindex="0" aria-labelledby="res-3-title" role="region">
        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/23ae9f1a-4a8b-4948-ad51-ae8e3ce7ebe3.png" alt="Bright vegan cafe interior with plants and wooden furniture" class="restaurant-image" loading="lazy" />
        <div class="card-content">
          <h2 id="res-3-title" class="restaurant-title">Green Roots Cafe</h2>
          <div class="restaurant-info">
            <span class="material-icons star" aria-hidden="true">star</span>
            <span>4.5</span>
            <span>·</span>
            <span>Vegan, Healthy</span>
            <span>·</span>
            <span>$</span>
          </div>
        </div>
      </article>

      <article class="restaurant-card" tabindex="0" aria-labelledby="res-4-title" role="region">
        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/02bd7f09-5ae8-44f8-bfc8-343c3377ed56.png" alt="Classic burger with fries on a wooden table" class="restaurant-image" loading="lazy" />
        <div class="card-content">
          <h2 id="res-4-title" class="restaurant-title">Burger Bros</h2>
          <div class="restaurant-info">
            <span class="material-icons star" aria-hidden="true">star</span>
            <span>4.3</span>
            <span>·</span>
            <span>American, Burgers</span>
            <span>·</span>
            <span>$$</span>
          </div>
        </div>
      </article>
    </section>
  </main>

  <footer>
    <div>&copy; 2024 Zomato Clone. All rights reserved.</div>
    <nav class="footer-links" aria-label="Footer navigation">
      <a href="#" class="footer-link" tabindex="0">Privacy</a>
      <a href="#" class="footer-link" tabindex="0">Terms</a>
      <a href="#" class="footer-link" tabindex="0">Contact</a>
    </nav>
  </footer>

  <script>
    // Mobile sidebar toggle
    const menuToggle = document.getElementById('menu-toggle');
    const sidebar = document.getElementById('sidebar');
    const mainContent = document.getElementById('main-content');

    menuToggle.addEventListener('click', () => {
      sidebar.classList.toggle('show');
      if(sidebar.classList.contains('show')) {
        mainContent.setAttribute('aria-hidden', 'true');
      } else {
        mainContent.removeAttribute('aria-hidden');
      }
    });

    // Close sidebar when focus leaves sidebar on mobile (optional accessibility)
    sidebar.addEventListener('keydown', (e) => {
      if (e.key === 'Escape' || e.key === 'Esc') {
        sidebar.classList.remove('show');
        mainContent.removeAttribute('aria-hidden');
        menuToggle.focus();
      }
    });
  </script>
</body>
</html>

