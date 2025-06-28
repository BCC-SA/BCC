<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BCC Internal Services</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-blue: #041961;
            --secondary-blue: #0040AA;
            --accent-blue: #04A4FA;
            --primary-red: #D2040A;
            --accent-red: #FF3650;
            --light-bg: #f8fafc;
            --dark-text: #1e293b;
            --card-bg: #ffffff;
            --border: #e2e8f0;
            --shadow: 0 4px 12px rgba(4, 25, 97, 0.15);
            --transition: all 0.3s ease;
        }

        .dark-mode {
            --primary-blue: #0d2b8a;
            --secondary-blue: #0055cc;
            --accent-blue: #0fb4ff;
            --primary-red: #e3050c;
            --accent-red: #ff4d65;
            --light-bg: #0f172a;
            --dark-text: #f1f5f9;
            --card-bg: #1e293b;
            --border: #334155;
            --shadow: 0 4px 12px rgba(4, 25, 97, 0.3);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--light-bg);
            color: var(--dark-text);
            line-height: 1.6;
            transition: var(--transition);
            padding-bottom: 60px;
            background-image: linear-gradient(135deg, rgba(4, 25, 97, 0.03) 0%, rgba(248, 250, 252, 0.03) 100%);
        }

        .dark-mode body {
            background-image: linear-gradient(135deg, rgba(4, 25, 97, 0.1) 0%, rgba(15, 23, 42, 0.1) 100%);
        }

        .container {
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 15px;
        }

        header {
            background: linear-gradient(135deg, var(--primary-blue) 0%, var(--secondary-blue) 100%);
            color: white;
            padding: 15px 0;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: var(--shadow);
        }

        .header-content {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo {
            width: 50px;
            height: 50px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: white;
            padding: 5px;
        }

        .logo img {
            width: 100%;
            height: 100%;
            object-fit: contain;
        }

        .app-title {
            font-size: 1.4rem;
            font-weight: 600;
            letter-spacing: 0.5px;
        }

        .controls {
            display: flex;
            gap: 10px;
        }

        .btn {
            background-color: var(--accent-blue);
            color: white;
            border: none;
            border-radius: 30px;
            padding: 8px 15px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 5px;
            transition: var(--transition);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .btn:hover {
            opacity: 0.9;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
        }

        .btn i {
            font-size: 1.1rem;
        }

        .btn-dark {
            background-color: var(--dark-text);
            color: white;
        }

        .btn-ar {
            background-color: var(--accent-red);
            color: white;
        }

        .section-title {
            margin: 30px 0 20px;
            font-size: 1.8rem;
            color: var(--primary-blue);
            position: relative;
            padding-bottom: 10px;
            font-weight: 700;
            text-align: center;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background: var(--accent-red);
            border-radius: 2px;
        }

        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: var(--shadow);
            transition: var(--transition);
            display: flex;
            flex-direction: column;
            height: 100%;
            border: 1px solid var(--border);
        }

        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 12px 20px rgba(4, 25, 97, 0.2);
        }

        .card-icon {
            height: 140px;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 15px;
            background: linear-gradient(135deg, rgba(4, 25, 97, 0.05) 0%, rgba(4, 164, 250, 0.05) 100%);
        }

        .dark-mode .card-icon {
            background: linear-gradient(135deg, rgba(4, 25, 97, 0.15) 0%, rgba(4, 164, 250, 0.15) 100%);
        }

        .card-icon img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
            filter: drop-shadow(0 4px 6px rgba(0, 0, 0, 0.1));
            transition: var(--transition);
        }

        .card:hover .card-icon img {
            transform: scale(1.05);
        }

        .card-content {
            padding: 20px;
            flex-grow: 1;
            display: flex;
            flex-direction: column;
        }

        .card-title {
            font-size: 1.25rem;
            margin-bottom: 10px;
            color: var(--primary-blue);
            font-weight: 700;
        }

        .card-text {
            color: var(--dark-text);
            opacity: 0.8;
            flex-grow: 1;
            margin-bottom: 15px;
            font-size: 0.95rem;
        }

        .card-btn {
            display: block;
            width: 100%;
            text-align: center;
            background: linear-gradient(135deg, var(--secondary-blue) 0%, var(--accent-blue) 100%);
            color: white;
            padding: 10px;
            border-radius: 8px;
            text-decoration: none;
            font-weight: 600;
            transition: var(--transition);
            border: none;
            cursor: pointer;
            font-size: 1rem;
        }

        .card-btn:hover {
            background: linear-gradient(135deg, var(--primary-blue) 0%, var(--secondary-blue) 100%);
            color: white;
            box-shadow: 0 4px 8px rgba(4, 25, 97, 0.2);
        }

        .menu-section {
            background-color: var(--card-bg);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: var(--shadow);
            margin-top: 20px;
            border: 1px solid var(--border);
        }

        .menu-tabs {
            display: flex;
            background: linear-gradient(135deg, var(--primary-blue) 0%, var(--secondary-blue) 100%);
        }

        .menu-tab {
            flex: 1;
            padding: 16px 0;
            text-align: center;
            color: white;
            cursor: pointer;
            transition: var(--transition);
            font-weight: 600;
            position: relative;
            font-size: 1.1rem;
        }

        .menu-tab.active {
            background: rgba(255, 255, 255, 0.15);
        }

        .menu-tab.active::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: var(--accent-red);
        }

        .day-tabs {
            display: flex;
            background-color: var(--light-bg);
            overflow-x: auto;
            padding: 0 10px;
            border-bottom: 1px solid var(--border);
        }

        .day-tab {
            padding: 14px 16px;
            cursor: pointer;
            white-space: nowrap;
            font-weight: 500;
            color: var(--dark-text);
            opacity: 0.7;
            transition: var(--transition);
            position: relative;
            font-size: 1rem;
        }

        .day-tab:hover {
            color: var(--primary-blue);
            opacity: 1;
        }

        .day-tab.active {
            color: var(--primary-blue);
            font-weight: 600;
            opacity: 1;
        }

        .day-tab.active::after {
            content: '';
            position: absolute;
            bottom: -1px;
            left: 0;
            width: 100%;
            height: 3px;
            background: var(--accent-blue);
        }

        .today-highlight {
            background-color: var(--accent-red);
            color: white;
            padding: 3px 8px;
            border-radius: 20px;
            font-size: 0.75rem;
            margin-left: 5px;
            vertical-align: middle;
            font-weight: 600;
        }

        .menu-content {
            padding: 30px;
        }

        .meal-section {
            margin-bottom: 30px;
            background: linear-gradient(135deg, rgba(248, 250, 252, 0.5) 0%, rgba(255, 255, 255, 0.5) 100%);
            border-radius: 12px;
            padding: 20px;
            border: 1px solid var(--border);
        }

        .dark-mode .meal-section {
            background: linear-gradient(135deg, rgba(30, 41, 59, 0.5) 0%, rgba(15, 23, 42, 0.5) 100%);
        }

        .meal-title {
            font-size: 1.4rem;
            color: var(--primary-blue);
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 2px solid var(--accent-blue);
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 600;
        }

        .meal-title i {
            color: var(--accent-red);
            background: rgba(210, 4, 10, 0.1);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .menu-items {
            background-color: var(--light-bg);
            padding: 18px;
            border-radius: 8px;
            border-left: 4px solid var(--accent-blue);
        }

        .dark-mode .menu-items {
            background-color: rgba(15, 23, 42, 0.5);
        }

        .menu-items p {
            margin: 10px 0;
            color: var(--dark-text);
            font-size: 1.05rem;
            line-height: 1.7;
        }

        footer {
            text-align: center;
            padding: 25px 0;
            margin-top: 50px;
            color: var(--dark-text);
            opacity: 0.8;
            border-top: 1px solid var(--border);
            font-size: 0.95rem;
            background: linear-gradient(135deg, rgba(248, 250, 252, 0.8) 0%, rgba(255, 255, 255, 0.8) 100%);
        }

        .dark-mode footer {
            background: linear-gradient(135deg, rgba(15, 23, 42, 0.8) 0%, rgba(30, 41, 59, 0.8) 100%);
        }

        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                gap: 15px;
                text-align: center;
            }
            
            .logo-container {
                justify-content: center;
            }
            
            .controls {
                justify-content: center;
                flex-wrap: wrap;
            }
            
            .section-title {
                font-size: 1.5rem;
            }
            
            .menu-content {
                padding: 20px;
            }
            
            .meal-title {
                font-size: 1.25rem;
            }
        }

        /* Animation for today's menu */
        @keyframes highlight {
            0% { background-color: var(--light-bg); }
            50% { background-color: rgba(4, 164, 250, 0.1); }
            100% { background-color: var(--light-bg); }
        }

        .today-menu {
            animation: highlight 3s ease-in-out 2;
        }

        .dark-mode .today-menu {
            animation: none;
            border: 2px solid var(--accent-blue);
            box-shadow: 0 0 15px rgba(4, 164, 250, 0.3);
        }

        /* Splash intro animation */
        .splash-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--primary-blue) 0%, var(--secondary-blue) 100%);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        .splash-logo {
            width: 150px;
            height: 150px;
            margin-bottom: 30px;
            animation: pulse 2s infinite;
        }

        .splash-title {
            color: white;
            font-size: 2rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 20px;
            opacity: 0;
            animation: fadeIn 1s ease 0.5s forwards;
        }

        .loading-dots {
            display: flex;
            gap: 10px;
            margin-top: 30px;
        }

        .dot {
            width: 12px;
            height: 12px;
            background-color: white;
            border-radius: 50%;
            animation: bounce 1.5s infinite ease-in-out;
        }

        .dot:nth-child(1) { animation-delay: 0s; }
        .dot:nth-child(2) { animation-delay: 0.2s; }
        .dot:nth-child(3) { animation-delay: 0.4s; }

        @keyframes pulse {
            0% { transform: scale(0.9); opacity: 0.8; }
            50% { transform: scale(1.1); opacity: 1; }
            100% { transform: scale(0.9); opacity: 0.8; }
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-15px); }
        }
    </style>
</head>
<body>
    <!-- Splash Screen -->
    <div class="splash-screen" id="splashScreen">
        <img src="https://i.postimg.cc/SQVc2828/LOGO-PNG.png" alt="BCC Logo" class="splash-logo">
        <h1 class="splash-title">BCC Internal Services</h1>
        <div class="loading-dots">
            <div class="dot"></div>
            <div class="dot"></div>
            <div class="dot"></div>
        </div>
    </div>

    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo-container">
                    <div class="logo">
                        <img src="https://i.postimg.cc/SQVc2828/LOGO-PNG.png" alt="BCC Logo">
                    </div>
                    <h1 class="app-title">BCC Internal Services</h1>
                </div>
                <div class="controls">
                    <button class="btn btn-dark" id="themeToggle">
                        <i class="fas fa-moon"></i> Dark Mode
                    </button>
                    <button class="btn btn-ar" id="langToggle">
                        <i class="fas fa-language"></i> العربية
                    </button>
                </div>
            </div>
        </div>
    </header>

    <main class="container">
        <h2 class="section-title">Quick Services</h2>
        
        <div class="cards-grid">
            <div class="card">
                <div class="card-icon">
                    <img src="https://i.postimg.cc/02fXNbxH/BCC-Staff-Illustration.png" alt="Residents Check-In">
                </div>
                <div class="card-content">
                    <h3 class="card-title">Residents Check-In</h3>
                    <p class="card-text">Register new residents arriving at BCC facilities</p>
                    <a href="https://form.jotform.com/242793935528470" class="card-btn" target="_blank">
                        Open Form <i class="fas fa-external-link-alt"></i>
                    </a>
                </div>
            </div>
            
            <div class="card">
                <div class="card-icon">
                    <img src="https://i.postimg.cc/MGXFNxC3/BCC-Staff-Illustration-10.png" alt="Residents Check-Out">
                </div>
                <div class="card-content">
                    <h3 class="card-title">Residents Check-Out</h3>
                    <p class="card-text">Process resident departures from BCC facilities</p>
                    <a href="https://form.jotform.com/bcccampandcatering/check-out-prefill-form" class="card-btn" target="_blank">
                        Open Form <i class="fas fa-external-link-alt"></i>
                    </a>
                </div>
            </div>
            
            <div class="card">
                <div class="card-icon">
                    <img src="https://i.postimg.cc/bJtFYgNQ/BCC-Staff-Illustration-11.png" alt="Sewage Trip Receipts">
                </div>
                <div class="card-content">
                    <h3 class="card-title">Sewage Trip Receipts</h3>
                    <p class="card-text">Record daily sewage transportation details</p>
                    <a href="https://form.jotform.com/240675060364050" class="card-btn" target="_blank">
                        Open Form <i class="fas fa-external-link-alt"></i>
                    </a>
                </div>
            </div>
            
            <div class="card">
                <div class="card-icon">
                    <img src="https://i.postimg.cc/Vv9GnNtv/BCC-Staff-Illustration-12.png" alt="Laundry Collection">
                </div>
                <div class="card-content">
                    <h3 class="card-title">Laundry Collection</h3>
                    <p class="card-text">Track laundry bag collection for residents</p>
                    <a href="https://form.jotform.com/240781925940058" class="card-btn" target="_blank">
                        Open Form <i class="fas fa-external-link-alt"></i>
                    </a>
                </div>
            </div>
            
            <div class="card">
                <div class="card-icon">
                    <img src="https://i.postimg.cc/k5Zpdz9J/BCC-Staff-Illustration-13.png" alt="Vegetable Orders">
                </div>
                <div class="card-content">
                    <h3 class="card-title">Vegetable Orders</h3>
                    <p class="card-text">Place purchase orders for kitchen vegetables</p>
                    <a href="https://form.jotform.com/250376919739068" class="card-btn" target="_blank">
                        Open Form <i class="fas fa-external-link-alt"></i>
                    </a>
                </div>
            </div>
            
            <div class="card">
                <div class="card-icon">
                    <img src="https://i.postimg.cc/vTw24ncC/BCC-Staff-Illustration-14.png" alt="Cleaning Supplies">
                </div>
                <div class="card-content">
                    <h3 class="card-title">Cleaning Supplies</h3>
                    <p class="card-text">Order plastic and cleaning items for facilities</p>
                    <a href="https://form.jotform.com/250384936944468" class="card-btn" target="_blank">
                        Open Form <i class="fas fa-external-link-alt"></i>
                    </a>
                </div>
            </div>
        </div>
        
        <h2 class="section-title">Know Your Food Menu</h2>
        
        <div class="menu-section">
            <div class="menu-tabs">
                <div class="menu-tab active" data-menu="senior">Senior Menu</div>
                <div class="menu-tab" data-menu="worker">Worker Menu</div>
            </div>
            
            <div class="day-tabs" id="dayTabs">
                <!-- Days will be populated by JavaScript -->
            </div>
            
            <div class="menu-content" id="menuContent">
                <!-- Menu content will be populated by JavaScript -->
            </div>
        </div>
    </main>
    
    <footer class="container">
        <p>BCC Bader Camp & Catering &copy; 2023 | King Abdulaziz Rd, Yanbu, Saudi Arabia</p>
        <p>For support, contact Administration: +966 12 123 4567</p>
    </footer>

    <script>
        // Menu data
        const workerMenu = {
            "Saturday": {
                "Breakfast": "Chana Dal Curry, Porata, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Gopy Aloo Masala, Aloo-Kerala Chat Masala Fry, Dal Curry, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Chicken Fry, Mix Vegetable, Dal Curry, Arabic Bread"
            },
            "Sunday": {
                "Breakfast": "Red Loobiya Curry, Porata, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Mix Vegetable, Dal Curry, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Mutton Curry or Fish Fry, Mix Vegetable, Dal Curry, Arabic Bread"
            },
            "Monday": {
                "Breakfast": "Greenpeas Curry, Porata, Tea/Coffee",
                "Lunch": "Kapsa, Chicken Curry, Tomato Chutney, Dal Curry, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Boiled Egg, Mix Vegetable, Dal Curry, Arabic Bread"
            },
            "Tuesday": {
                "Breakfast": "Moong Whole Curry, Porata, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Palak Chena, Mutton Keema, Dal Curry, Arabic Bread",
                "Dinner": "Ghee Rice, Chicken Kadai, Mix Vegetable, Dal Curry, Arabic Bread"
            },
            "Wednesday": {
                "Breakfast": "Black Chana Curry, Porata/Chapati, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Chicken Curry, Mix Vegetable, Dal Curry, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Mix Vegetable, Soyabeen Masala, Dal Curry, Arabic Bread"
            },
            "Thursday": {
                "Breakfast": "Eye Beans Curry, Porata, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Okra with Boiled Egg, Mix Vegetable, Dal Curry, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Sambar, Fish Fry, Dal Curry, Arabic Bread"
            },
            "Friday": {
                "Breakfast": "Moong Dal Curry, Porata, Tea/Coffee",
                "Lunch": "Chicken Biryani, Veggie Salad/Laben, Dal Curry, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Boiled Egg, Chana Mix Curry, Dal Curry, Arabic Bread"
            }
        };

        const seniorMenu = {
            "Saturday": {
                "Breakfast": "Red Kidney Curry, Porata, Dosa/Idly, Sambar/Chutney, Sliced Bread, Butter/Jam, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Red Pumpkin Stew, Aloo-Kerala Chat Roast, Dal Curry, Fresh Veg Salad, Curd, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Chicken Fry, Dahi Curry or Dahi Pakoda, Mix Vegetable, Dal Curry, Fresh Veg Salad, Arabic Bread, Tandoori Roti, Fruits"
            },
            "Sunday": {
                "Breakfast": "Moong Whole Curry, Porata, Scrambled Egg, Sliced Bread, Butter/Jam, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Chicken Kadai, Long Beans Stir-Fry, Mix Vegetable, Dal Curry, Fresh Veg Salad, Curd, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Mutton Curry, Mix Vegetables, Dal Curry, Fresh Veg Salad, Arabic Bread, Tandoori Roti, Fruits"
            },
            "Monday": {
                "Breakfast": "Eye Beans Curry, Porata, Dosa/Idly, Sambar/Chutney, Sliced Bread, Butter/Jam, Tea/Coffee",
                "Lunch": "Kapsa, Chicken Fry, Green Peas Potato Masala, Tomato Chutney, Dal Curry, Fresh Veg Salad, Curd, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Paneer Masala or Fish Fry, Green Banana Stir-Fry, Mix Vegetables, Dal Curry, Fresh Veg Salad, Arabic Bread, Tandoori Roti, Fruits"
            },
            "Tuesday": {
                "Breakfast": "Black Chana Curry, Porata, Boiled Egg, Sliced Bread, Butter/Jam, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Palak Chena/Palak Paneer, Gobi Manchurian, Dal Curry, Fresh Veg Salad, Curd, Arabic Bread",
                "Dinner": "Ghee Rice, Chicken Chilli, Mix Vegetable, Dal Curry, Fresh Veg Salad, Arabic Bread, Tandoori Roti, Fruits"
            },
            "Wednesday": {
                "Breakfast": "Chickpeas Curry, Porata/Chapati, Oats or Semolina Halva, Sliced Bread, Butter/Jam, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Butter Chicken, Snake Gourd Masala, Mix Vegetable, Dal Curry, Fresh Veg Salad, Curd, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Mushroom Masala, Yellow Pumpkin Masala, Soyabean Masala, Dal Curry, Fresh Veg Salad, Arabic Bread, Tandoori Roti, Fruits"
            },
            "Thursday": {
                "Breakfast": "Moong Dal Curry, Porata, Scrambled Egg, Sliced Bread, Butter/Jam, Tea/Coffee",
                "Lunch": "Plain Boiled Rice, Chicken Masala, Cabbage Stir-Fry, Gobi Manchurian, Dal Curry, Fresh Veg Salad, Curd, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Fish Fry, Sambar, Beetroot Stir-Fry, Dal Curry, Fresh Veg Salad, Arabic Bread, Tandoori Roti, Fruits"
            },
            "Friday": {
                "Breakfast": "Greenpeas with Potatoes Curry, Porata, Upma, Boiled Egg, Sliced Bread, Butter/Jam, Tea/Coffee",
                "Lunch": "Chicken Biryani, Bhindi Thik Masala, Pappad, Dal Curry, Fresh Veg Salad, Curd, Arabic Bread",
                "Dinner": "Plain Boiled Rice, Boiled Egg, Chana Mix Curry, Mix Vegetables, Dal Curry, Fresh Veg Salad, Arabic Bread, Tandoori Roti, Fruits"
            }
        };

        // Get today's day
        const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
        const today = new Date();
        const todayDay = days[today.getDay()];
        
        // DOM elements
        const themeToggle = document.getElementById('themeToggle');
        const langToggle = document.getElementById('langToggle');
        const dayTabsContainer = document.getElementById('dayTabs');
        const menuContent = document.getElementById('menuContent');
        const menuTabs = document.querySelectorAll('.menu-tab');
        const splashScreen = document.getElementById('splashScreen');
        
        // State
        let currentMenuType = 'senior';
        let currentDay = todayDay;
        
        // Initialize the app
        function initApp() {
            renderDayTabs();
            renderMenu();
            
            // Set today as active
            document.querySelector(`.day-tab[data-day="${todayDay}"]`).classList.add('active');
            
            // Hide splash screen after delay
            setTimeout(() => {
                splashScreen.style.opacity = '0';
                splashScreen.style.visibility = 'hidden';
            }, 2500);
        }
        
        // Render day tabs
        function renderDayTabs() {
            dayTabsContainer.innerHTML = '';
            
            days.forEach(day => {
                const dayTab = document.createElement('div');
                dayTab.className = 'day-tab';
                dayTab.dataset.day = day;
                dayTab.textContent = day;
                
                // Add today indicator
                if (day === todayDay) {
                    const todaySpan = document.createElement('span');
                    todaySpan.className = 'today-highlight';
                    todaySpan.textContent = 'Today';
                    dayTab.appendChild(todaySpan);
                }
                
                dayTab.addEventListener('click', () => {
                    // Remove active class from all tabs
                    document.querySelectorAll('.day-tab').forEach(tab => tab.classList.remove('active'));
                    // Add active class to clicked tab
                    dayTab.classList.add('active');
                    currentDay = day;
                    renderMenu();
                });
                
                dayTabsContainer.appendChild(dayTab);
            });
        }
        
        // Render menu content
        function renderMenu() {
            const menu = currentMenuType === 'senior' ? seniorMenu[currentDay] : workerMenu[currentDay];
            
            let menuHTML = '';
            
            // Highlight today's menu
            const isToday = currentDay === todayDay;
            
            for (const [meal, items] of Object.entries(menu)) {
                let iconClass;
                if (meal === 'Breakfast') iconClass = 'fa-coffee';
                else if (meal === 'Lunch') iconClass = 'fa-utensils';
                else iconClass = 'fa-moon';
                
                menuHTML += `
                    <div class="meal-section ${isToday ? 'today-menu' : ''}">
                        <h3 class="meal-title">
                            <i class="fas ${iconClass}"></i>
                            ${meal}
                        </h3>
                        <div class="menu-items">
                            <p>${items}</p>
                        </div>
                    </div>
                `;
            }
            
            menuContent.innerHTML = menuHTML;
        }
        
        // Menu type tab switching
        menuTabs.forEach(tab => {
            tab.addEventListener('click', () => {
                // Remove active class from all tabs
                menuTabs.forEach(t => t.classList.remove('active'));
                // Add active class to clicked tab
                tab.classList.add('active');
                currentMenuType = tab.dataset.menu;
                renderMenu();
            });
        });
        
        // Dark mode toggle
        themeToggle.addEventListener('click', () => {
            document.body.classList.toggle('dark-mode');
            const isDark = document.body.classList.contains('dark-mode');
            themeToggle.innerHTML = isDark ? 
                '<i class="fas fa-sun"></i> Light Mode' : 
                '<i class="fas fa-moon"></i> Dark Mode';
            
            // Update the menu to reapply dark mode styles
            renderMenu();
        });
        
        // Language toggle (simplified for demo)
        langToggle.addEventListener('click', () => {
            const isArabic = langToggle.textContent.includes('العربية');
            langToggle.innerHTML = isArabic ? 
                '<i class="fas fa-language"></i> English' : 
                '<i class="fas fa-language"></i> العربية';
            
            // In a real implementation, this would switch all text to Arabic
            alert('In a full implementation, this would switch the entire interface to Arabic with RTL layout.');
        });
        
        // Initialize the app
        window.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>