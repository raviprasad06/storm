# storm
snowhack
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>safe Drop  Indore | Water Safety Portal</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <style>
        :root {
            --bg-primary: #0f172a;
            --bg-secondary: #1e293b;
            --bg-surface: #334155;
            --accent-cyan: #06b6d4;
            --accent-red: #ef4444;
            --accent-green: #10b981;
            --accent-amber: #f59e0b;
            --text-primary: #f8fafc;
            --text-secondary: #cbd5e1;
            --text-muted: #64748b;
            --shadow-glow: 0 0 15px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.6;
            overflow-x: hidden;
        }

        .container {
            max-width: 1280px;
            margin: 0 auto;
            padding: 0 1.5rem;
        }

        /* Header & Navigation */
        header {
            background-color: rgba(15, 23, 42, 0.95);
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 1000;
            border-bottom: 1px solid rgba(6, 182, 212, 0.1);
        }

        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 0;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--accent-cyan);
        }

        .logo i {
            font-size: 2rem;
        }

        .logo span {
            background: linear-gradient(90deg, var(--accent-cyan), #3b82f6);
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
        }

        .nav-links a {
            color: var(--text-secondary);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
            padding: 0.5rem 0;
            position: relative;
        }

        .nav-links a:hover, .nav-links a.active {
            color: var(--accent-cyan);
        }

        .nav-links a.active::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background-color: var(--accent-cyan);
            box-shadow: var(--shadow-glow) var(--accent-cyan);
        }

        .nav-actions {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .search-box {
            display: flex;
            align-items: center;
            background: var(--bg-surface);
            border-radius: 0.5rem;
            padding: 0.5rem 1rem;
            border: 1px solid rgba(6, 182, 212, 0.2);
        }

        .search-box input {
            background: transparent;
            border: none;
            color: var(--text-primary);
            padding: 0.25rem;
            width: 180px;
        }

        .search-box input:focus {
            outline: none;
        }

        .search-box i {
            color: var(--text-muted);
        }

        .language-switch {
            background: var(--bg-surface);
            border: 1px solid rgba(6, 182, 212, 0.2);
            color: var(--text-secondary);
            padding: 0.5rem 1rem;
            border-radius: 0.5rem;
            cursor: pointer;
            font-weight: 500;
        }

        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: var(--text-primary);
            font-size: 1.5rem;
            cursor: pointer;
        }

        /* Live Alert Bar */
        .alert-bar {
            background: linear-gradient(90deg, rgba(239, 68, 68, 0.9), rgba(239, 68, 68, 0.7));
            color: white;
            padding: 0.75rem 0;
            text-align: center;
            font-weight: 600;
            animation: pulse 2s infinite;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.8; }
        }

        .alert-bar i {
            margin-right: 0.5rem;
        }

        /* Hero Section */
        .hero {
            padding: 4rem 0;
            background: radial-gradient(circle at top right, rgba(6, 182, 212, 0.1), transparent 50%),
                        radial-gradient(circle at bottom left, rgba(16, 185, 129, 0.05), transparent 50%);
        }

        .hero-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 3rem;
            align-items: center;
        }

        .hero-text h1 {
            font-size: 3.5rem;
            line-height: 1.1;
            margin-bottom: 1.5rem;
            background: linear-gradient(90deg, var(--text-primary), var(--accent-cyan));
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero-text p {
            font-size: 1.25rem;
            color: var(--text-secondary);
            margin-bottom: 2rem;
        }

        .metrics {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1.5rem;
            margin-top: 2rem;
        }

        .metric-card {
            background: var(--bg-surface);
            border-radius: 1rem;
            padding: 1.5rem;
            border-left: 4px solid var(--accent-cyan);
        }

        .metric-value {
            font-size: 2rem;
            font-weight: 800;
            color: var(--accent-cyan);
            display: block;
            line-height: 1;
        }

        .metric-label {
            font-size: 0.875rem;
            color: var(--text-secondary);
            margin-top: 0.5rem;
        }

        .cta-button {
            background: linear-gradient(90deg, var(--accent-cyan), #0ea5e9);
            color: white;
            border: none;
            padding: 1rem 2rem;
            border-radius: 0.5rem;
            font-weight: 600;
            font-size: 1.125rem;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            box-shadow: var(--shadow-glow) rgba(6, 182, 212, 0.4);
        }

        .cta-button:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-glow) rgba(6, 182, 212, 0.6);
        }

        /* Sections */
        .section {
            padding: 4rem 0;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 3rem;
        }

        .section-title {
            font-size: 2.5rem;
            position: relative;
            display: inline-block;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 60px;
            height: 4px;
            background-color: var(--accent-cyan);
            border-radius: 2px;
        }

        /* Problem Cards */
        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
        }

        .problem-card {
            background: var(--bg-surface);
            border-radius: 1rem;
            padding: 2rem;
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .problem-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
        }

        .problem-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 4px;
            height: 100%;
            background-color: var(--accent-red);
        }

        .problem-card:nth-child(2)::before { background-color: var(--accent-amber); }
        .problem-card:nth-child(3)::before { background-color: var(--accent-cyan); }
        .problem-card:nth-child(4)::before { background-color: var(--accent-green); }

        .card-icon {
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
            color: var(--accent-cyan);
        }

        .card-title {
            font-size: 1.5rem;
            margin-bottom: 1rem;
        }

        .card-content {
            color: var(--text-secondary);
        }

        .card-content ul {
            list-style: none;
            margin-top: 1rem;
        }

        .card-content li {
            margin-bottom: 0.5rem;
            padding-left: 1.5rem;
            position: relative;
        }

        .card-content li::before {
            content: '•';
            position: absolute;
            left: 0;
            color: var(--accent-cyan);
            font-weight: bold;
        }

        /* Dashboard */
        .dashboard {
            background: var(--bg-secondary);
            border-radius: 1rem;
            padding: 2rem;
            margin-top: 2rem;
            border: 1px solid rgba(6, 182, 212, 0.2);
        }

        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .dashboard-title {
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .dashboard-table {
            width: 100%;
            border-collapse: collapse;
        }

        .dashboard-table th {
            text-align: left;
            padding: 1rem;
            color: var(--text-secondary);
            font-weight: 600;
            border-bottom: 1px solid var(--bg-surface);
        }

        .dashboard-table td {
            padding: 1rem;
            border-bottom: 1px solid var(--bg-surface);
        }

        .status-indicator {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 0.5rem;
        }

        .status-safe { background-color: var(--accent-green); box-shadow: 0 0 8px var(--accent-green); }
        .status-medium { background-color: var(--accent-amber); box-shadow: 0 0 8px var(--accent-amber); }
        .status-unsafe { background-color: var(--accent-red); box-shadow: 0 0 8px var(--accent-red); }

        /* Emergency Panel */
        .emergency-panel {
            background: linear-gradient(135deg, rgba(239, 68, 68, 0.1), rgba(239, 68, 68, 0.05));
            border: 2px solid var(--accent-red);
            border-radius: 1rem;
            padding: 2rem;
            margin: 2rem 0;
            animation: border-pulse 2s infinite;
        }

        @keyframes border-pulse {
            0%, 100% { border-color: var(--accent-red); }
            50% { border-color: rgba(239, 68, 68, 0.5); }
        }

        .emergency-header {
            display: flex;
            align-items: center;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }

        .emergency-header i {
            font-size: 2rem;
            color: var(--accent-red);
        }

        .emergency-header h3 {
            font-size: 1.75rem;
            color: var(--accent-red);
        }

        .sos-button {
            background: linear-gradient(90deg, var(--accent-red), #dc2626);
            color: white;
            border: none;
            padding: 1.5rem 3rem;
            border-radius: 0.5rem;
            font-weight: 800;
            font-size: 1.5rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 1rem;
            margin: 2rem auto;
            width: 100%;
            max-width: 400px;
            animation: pulse 1.5s infinite;
            box-shadow: 0 0 20px rgba(239, 68, 68, 0.5);
        }

        .sos-button:hover {
            animation: none;
            box-shadow: 0 0 30px rgba(239, 68, 68, 0.8);
        }

        /* Form Styles */
        .report-form {
            background: var(--bg-surface);
            border-radius: 1rem;
            padding: 2rem;
            margin-top: 2rem;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-label {
            display: block;
            margin-bottom: 0.5rem;
            color: var(--text-secondary);
            font-weight: 500;
        }

        .form-control {
            width: 100%;
            padding: 0.75rem 1rem;
            background: var(--bg-secondary);
            border: 1px solid rgba(6, 182, 212, 0.2);
            border-radius: 0.5rem;
            color: var(--text-primary);
            font-family: 'Inter', sans-serif;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--accent-cyan);
            box-shadow: 0 0 0 3px rgba(6, 182, 212, 0.1);
        }

        .checkbox-group {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-top: 0.5rem;
        }

        .checkbox-label {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            cursor: pointer;
        }

        .checkbox-label input[type="checkbox"] {
            width: 18px;
            height: 18px;
        }

        .upload-area {
            border: 2px dashed rgba(6, 182, 212, 0.3);
            border-radius: 0.5rem;
            padding: 3rem;
            text-align: center;
            cursor: pointer;
            transition: border-color 0.3s;
        }

        .upload-area:hover {
            border-color: var(--accent-cyan);
        }

        .upload-area i {
            font-size: 3rem;
            color: var(--accent-cyan);
            margin-bottom: 1rem;
        }

        /* Symptom Checker */
        .symptom-checker {
            background: var(--bg-surface);
            border-radius: 1rem;
            padding: 2rem;
            margin-top: 2rem;
        }

        .slider-container {
            margin: 2rem 0;
        }

        .slider-value {
            text-align: center;
            font-size: 2rem;
            font-weight: 800;
            color: var(--accent-cyan);
            margin-bottom: 0.5rem;
        }

        .slider {
            width: 100%;
            height: 10px;
            -webkit-appearance: none;
            background: var(--bg-secondary);
            border-radius: 5px;
            outline: none;
        }

        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            background: var(--accent-cyan);
            cursor: pointer;
            box-shadow: 0 0 10px var(--accent-cyan);
        }

        .result-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s, visibility 0.3s;
        }

        .result-modal.active {
            opacity: 1;
            visibility: visible;
        }

        .modal-content {
            background: var(--bg-surface);
            border-radius: 1rem;
            padding: 2rem;
            max-width: 500px;
            width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            border: 1px solid var(--accent-cyan);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .close-modal {
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 1.5rem;
            cursor: pointer;
        }

        /* Footer */
        footer {
            background: var(--bg-secondary);
            padding: 3rem 0;
            margin-top: 4rem;
            border-top: 1px solid rgba(6, 182, 212, 0.2);
        }

        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
        }

        .footer-section h3 {
            font-size: 1.25rem;
            margin-bottom: 1.5rem;
            color: var(--accent-cyan);
        }

        .footer-links {
            list-style: none;
        }

        .footer-links li {
            margin-bottom: 0.75rem;
        }

        .footer-links a {
            color: var(--text-secondary);
            text-decoration: none;
            transition: color 0.3s;
        }

        .footer-links a:hover {
            color: var(--accent-cyan);
        }

        .copyright {
            text-align: center;
            margin-top: 3rem;
            padding-top: 2rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: var(--text-muted);
            font-size: 0.875rem;
        }

        /* Map Container */
        #map {
            height: 400px;
            width: 100%;
            border-radius: 1rem;
            margin-top: 1rem;
            border: 1px solid rgba(6, 182, 212, 0.2);
        }

        /* Responsive Design */
        @media (max-width: 1024px) {
            .hero-content {
                grid-template-columns: 1fr;
            }
            
            .section-title {
                font-size: 2rem;
            }
            
            .hero-text h1 {
                font-size: 2.75rem;
            }
        }

        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            
            .mobile-menu-btn {
                display: block;
            }
            
            .nav-actions {
                display: none;
            }
            
            .hero-text h1 {
                font-size: 2.25rem;
            }
            
            .metrics {
                grid-template-columns: 1fr;
            }
            
            .section {
                padding: 3rem 0;
            }
            
            .dashboard {
                overflow-x: auto;
            }
            
            .dashboard-table {
                min-width: 600px;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 0 1rem;
            }
            
            .hero-text h1 {
                font-size: 1.75rem;
            }
            
            .section-title {
                font-size: 1.75rem;
            }
            
            .cta-button, .sos-button {
                width: 100%;
                justify-content: center;
            }
            
            .problem-card {
                padding: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <!-- Live Alert Bar -->
    <div class="alert-bar">
        <i class="fas fa-exclamation-triangle"></i>
        Alert: Bhagirathpura area reports foul-smelling water. Avoid consumption until further notice.
    </div>

    <!-- Header -->
    <header>
        <div class="container">
            <div class="nav-container">
                <div class="logo">
                    <i class="fas fa-tint"></i>
                    <span>Blue Drop</span>
                    <span style="color: var(--text-secondary); font-weight: 400;">| Indore</span>
                </div>
                
                <button class="mobile-menu-btn">
                    <i class="fas fa-bars"></i>
                </button>
                
                <ul class="nav-links">
                    <li><a href="#home" class="active">Home</a></li>
                    <li><a href="#problems">Problems</a></li>
                    <li><a href="#solutions">Solutions</a></li>
                    <li><a href="#dashboard">Dashboard</a></li>
                    <li><a href="#report">Report</a></li>
                    <li><a href="#emergency">Emergency</a></li>
                </ul>
                
                <div class="nav-actions">
                    <div class="search-box">
                        <i class="fas fa-search"></i>
                        <input type="text" placeholder="Search area or ward...">
                    </div>
                    <button class="language-switch">
                        <i class="fas fa-globe"></i> हिंदी
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero" id="home">
        <div class="container">
            <div class="hero-content">
                <div class="hero-text">
                    <h1>Clean Water is a Right, Not a Privilege</h1>
                    <p>Real-time water safety monitoring and emergency response system for Indore. Protecting public health through technology and community action.</p>
                    
                    <button class="cta-button">
                        <i class="fas fa-map-marker-alt"></i>
                        Check Your Area Safety
                    </button>
                    
                    <div class="metrics">
                        <div class="metric-card">
                            <span class="metric-value" id="activeAlerts">12</span>
                            <span class="metric-label">Active Alerts Today</span>
                        </div>
                        <div class="metric-card">
                            <span class="metric-value" id="waterTests">2,340</span>
                            <span class="metric-label">Water Tests This Month</span>
                        </div>
                        <div class="metric-card">
                            <span class="metric-value" id="responseTime">&lt;4h</span>
                            <span class="metric-label">Avg. Response Time</span>
                        </div>
                    </div>
                </div>
                
                <div id="map"></div>
        </div>
    </div>
</section>

<!-- Leaflet Map Script -->
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
    // Initialize map centered on Indore
    const map = L.map('map').setView([22.7196, 75.8577], 12);

    // Add tile layer
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '© OpenStreetMap contributors',
        maxZoom: 19
    }).addTo(map);

    // Define safe and unsafe zones in Indore
    const zones = [
        // Safe Areas
        {
            name: 'Vijay Nagar',
            lat: 22.7394,
            lng: 75.8761,
            status: 'safe',
            chlorine: '0.8 ppm',
            issues: 'None'
        },
        {
            name: 'Scheme 54',
            lat: 22.7100,
            lng: 75.8950,
            status: 'safe',
            chlorine: '0.9 ppm',
            issues: 'None'
        },
        // Medium Risk Areas
        {
            name: 'Rajendra Nagar',
            lat: 22.7050,
            lng: 75.8500,
            status: 'medium',
            chlorine: '0.3 ppm',
            issues: 'Low pressure'
        },
        {
            name: 'Bhavarkuan',
            lat: 22.6950,
            lng: 75.8700,
            status: 'medium',
            chlorine: '0.4 ppm',
            issues: 'Turbidity issue'
        },
        // Unsafe Areas
        {
            name: 'Bhagirathpura',
            lat: 22.7300,
            lng: 75.8300,
            status: 'unsafe',
            chlorine: '0.0 ppm',
            issues: 'Foul smell reported'
        }
    ];

    // Add markers for each zone
    zones.forEach(zone => {
        const iconColor = zone.status === 'safe' ? '#10b981' : zone.status === 'medium' ? '#f59e0b' : '#ef4444';
        
        const customIcon = L.divIcon({
            className: 'custom-marker',
            html: `
                <div style="
                    background-color: ${iconColor};
                    width: 30px;
                    height: 30px;
                    border-radius: 50%;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    box-shadow: 0 0 10px ${iconColor};
                    border: 3px solid white;
                ">
                    <i class="fas fa-droplet" style="color: white; font-size: 16px;"></i>
                </div>
            `,
            iconSize: [30, 30],
            iconAnchor: [15, 15]
        });

        const marker = L.marker([zone.lat, zone.lng], { icon: customIcon }).addTo(map);
        
        marker.bindPopup(`
            <div style="color: black;">
                <h4 style="margin: 0 0 0.5rem 0;">${zone.name}</h4>
                <p style="margin: 0.25rem 0;"><strong>Status:</strong> <span style="color: ${iconColor}; font-weight: bold;">${zone.status.toUpperCase()}</span></p>
                <p style="margin: 0.25rem 0;"><strong>Chlorine:</strong> ${zone.chlorine}</p>
                <p style="margin: 0.25rem 0;"><strong>Issues:</strong> ${zone.issues}</p>
            </div>
        `);
    });

    // Add legend
    const legend = L.control({ position: 'bottomright' });
    legend.onAdd = function() {
        const div = L.DomUtil.create('div', 'info');
        div.style.backgroundColor = 'white';
        div.style.padding = '10px';
        div.style.borderRadius = '5px';
        div.style.boxShadow = '0 0 15px rgba(0,0,0,0.2)';
        div.innerHTML = `
            <p style="margin: 0; font-weight: bold; margin-bottom: 8px;">Water Safety Legend</p>
            <p style="margin: 5px 0;"><span style="display: inline-block; width: 12px; height: 12px; background: #10b981; border-radius: 50%; margin-right: 5px;"></span> Safe</p>
            <p style="margin: 5px 0;"><span style="display: inline-block; width: 12px; height: 12px; background: #f59e0b; border-radius: 50%; margin-right: 5px;"></span> Medium Risk</p>
            <p style="margin: 5px 0;"><span style="display: inline-block; width: 12px; height: 12px; background: #ef4444; border-radius: 50%; margin-right: 5px;"></span> Unsafe</p>
        `;
        return div;
    };
    legend.addTo(map);
</script>
        </div>
    </section>

    <!-- Problem Section -->
    <section class="section" id="problems">
        <div class="container">
            <div class="section-header">
                <h2 class="section-title">The Water Crisis in Urban India</h2>
                <p class="section-subtitle">Understanding the key challenges</p>
            </div>
            
            <div class="cards-grid">
                <div class="problem-card">
                    <div class="card-icon">
                        <i class="fas fa-bacteria"></i>
                    </div>
                    <h3 class="card-title">Contaminated Drinking Water</h3>
                    <div class="card-content">
                        <p>Microbial and chemical pollutants making water unsafe.</p>
                        <ul>
                            <li>E. coli & coliform presence</li>
                            <li>Muddy/foul smell issues</li>
                            <li>Poor chlorination levels</li>
                            <li>Heavy metal contamination</li>
                        </ul>
                    </div>
                </div>
                
                <div class="problem-card">
                    <div class="card-icon">
                        <i class="fas fa-hospital-user"></i>
                    </div>
                    <h3 class="card-title">Waterborne Diseases</h3>
                    <div class="card-content">
                        <p>Illnesses spreading through contaminated water sources.</p>
                        <ul>
                            <li>Diarrhea & cholera outbreaks</li>
                            <li>Typhoid fever cases</li>
                            <li>Dehydration risks</li>
                            <li>Children & elderly at high risk</li>
                        </ul>
                    </div>
                </div>
                
                <div class="problem-card">
                    <div class="card-icon">
                        <i class="fas fa-pipe"></i>
                    </div>
                    <h3 class="card-title">Poor Infrastructure</h3>
                    <div class="card-content">
                        <p>Aging systems causing contamination.</p>
                        <ul>
                            <li>Old rusted pipelines</li>
                            <li>Sewage mixing issues</li>
                            <li>Uneven water pressure</li>
                            <li>Leakage and breakage</li>
                        </ul>
                    </div>
                </div>
                
                <div class="problem-card">
                    <div class="card-icon">
                        <i class="fas fa-info-circle"></i>
                    </div>
                    <h3 class="card-title">Lack of Awareness</h3>
                    <div class="card-content">
                        <p>Knowledge gaps leading to health risks.</p>
                        <ul>
                            <li>Unboiled tap water consumption</li>
                            <li>Misinformation about safety</li>
                            <li>No clear emergency instructions</li>
                            <li>Delayed medical attention</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Government Solutions & Dashboard -->
    <section class="section" id="dashboard">
        <div class="container">
            <div class="section-header">
                <h2 class="section-title">Live Water Quality Dashboard</h2>
                <div class="time-display">
                    <i class="fas fa-clock"></i>
                    Last updated: <span id="currentTime">Just now</span>
                </div>
            </div>
            
            <div class="dashboard">
                <div class="dashboard-header">
                    <h3 class="dashboard-title">
                        <i class="fas fa-chart-line"></i>
                        Indore Water Safety Status
                    </h3>
                    <div class="filters">
                        <select class="form-control" style="width: auto;" id="wardFilter">
                            <option value="">All Wards</option>
                            <option value="bhagirathpura">Bhagirathpura</option>
                            <option value="vijay-nagar">Vijay Nagar</option>
                            <option value="rajendra-nagar">Rajendra Nagar</option>
                            <option value="scheme-54">Scheme 54</option>
                            <option value="bhavarkuan">Bhavarkuan</option>
                        </select>
                    </div>
                </div>
                
                <table class="dashboard-table">
                    <thead>
                        <tr>
                            <th>Area/Ward</th>
                            <th>Safety Status</th>
                            <th>Chlorine Level</th>
                            <th>Last Test</th>
                            <th>Active Issues</th>
                        </tr>
                    </thead>
                    <tbody id="dashboardTableBody">
                        <tr data-ward="vijay-nagar">
                            <td>Vijay Nagar</td>
                            <td><span class="status-indicator status-safe"></span> Safe</td>
                            <td>0.8 ppm</td>
                            <td class="last-test">2 hours ago</td>
                            <td>None</td>
                        </tr>
                        <tr data-ward="rajendra-nagar">
                            <td>Rajendra Nagar</td>
                            <td><span class="status-indicator status-medium"></span> Medium Risk</td>
                            <td>0.3 ppm</td>
                            <td class="last-test">4 hours ago</td>
                            <td>Low pressure</td>
                        </tr>
                        <tr data-ward="bhagirathpura">
                            <td>Bhagirathpura</td>
                            <td><span class="status-indicator status-unsafe"></span> Unsafe</td>
                            <td>0.0 ppm</td>
                            <td class="last-test">1 hour ago</td>
                            <td>Foul smell reported</td>
                        </tr>
                        <tr data-ward="scheme-54">
                            <td>Scheme 54</td>
                            <td><span class="status-indicator status-safe"></span> Safe</td>
                            <td>0.9 ppm</td>
                            <td class="last-test">3 hours ago</td>
                            <td>None</td>
                        </tr>
                        <tr data-ward="bhavarkuan">
                            <td>Bhavarkuan</td>
                            <td><span class="status-indicator status-medium"></span> Medium Risk</td>
                            <td>0.4 ppm</td>
                            <td class="last-test">5 hours ago</td>
                            <td>Turbidity issue</td>
                        </tr>
                    </tbody>
                </table>
                
                <div style="margin-top: 2rem; display: flex; gap: 1rem; align-items: center;">
                    <div style="display: flex; align-items: center; gap: 0.5rem;">
                        <span class="status-indicator status-safe"></span> Safe
                    </div>
                    <div style="display: flex; align-items: center; gap: 0.5rem; margin-left: 1rem;">
                        <span class="status-indicator status-medium"></span> Medium Risk
                    </div>
                    <div style="display: flex; align-items: center; gap: 0.5rem; margin-left: 1rem;">
                        <span class="status-indicator status-unsafe"></span> Unsafe
                    </div>
                </div>
            </div>
        </div>
    </section>

    <script>
        // Update current time
        function updateTime() {
            const now = new Date();
            const timeString = now.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' });
            document.getElementById('currentTime').textContent = timeString;
        }

        // Simulate live data updates
        function updateDashboard() {
            const rows = document.querySelectorAll('#dashboardTableBody tr');
            rows.forEach(row => {
                const lastTestCell = row.querySelector('.last-test');
                if (lastTestCell) {
                    const text = lastTestCell.textContent;
                    const match = text.match(/(\d+)\s+hours?\s+ago/);
                    if (match) {
                        const hours = parseInt(match[1]);
                        if (hours > 0) {
                            lastTestCell.textContent = (hours - 1) + ' hours ago';
                        }
                    }
                }
            });
            updateTime();
        }

        // Filter dashboard by ward
        document.getElementById('wardFilter').addEventListener('change', (e) => {
            const selectedWard = e.target.value;
            const rows = document.querySelectorAll('#dashboardTableBody tr');
            
            rows.forEach(row => {
                if (selectedWard === '' || row.dataset.ward === selectedWard) {
                    row.style.display = '';
                } else {
                    row.style.display = 'none';
                }
            });
        });

        // Update dashboard every minute
        setInterval(updateDashboard, 60000);
        updateTime();
    </script>

    <!-- Emergency Response -->
    <section class="section" id="emergency">
        <div class="container">
            <div class="section-header">
                <h2 class="section-title">Emergency Response</h2>
                <p class="section-subtitle">Immediate actions for water contamination</p>
            </div>
            
            <div class="emergency-panel">
                <div class="emergency-header">
                    <i class="fas fa-exclamation-triangle"></i>
                    <h3>CONTAMINATION DETECTED: Immediate Actions Required</h3>
                </div>
                
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 2rem;">
                    <div>
                        <h4 style="margin-bottom: 1rem; color: var(--accent-red);">1. IMMEDIATE ACTIONS</h4>
                        <ul style="list-style: none;">
                            <li style="margin-bottom: 0.75rem; padding-left: 1.5rem; position: relative;">
                                <i class="fas fa-ban" style="position: absolute; left: 0; color: var(--accent-red);"></i>
                                Stop all consumption immediately
                            </li>
                            <li style="margin-bottom: 0.75rem; padding-left: 1.5rem; position: relative;">
                                <i class="fas fa-water" style="position: absolute; left: 0; color: var(--accent-red);"></i>
                                Isolate water source
                            </li>
                            <li style="margin-bottom: 0.75rem; padding-left: 1.5rem; position: relative;">
                                <i class="fas fa-bullhorn" style="position: absolute; left: 0; color: var(--accent-red);"></i>
                                Alert neighbors
                            </li>
                        </ul>
                    </div>
                    
                    <div>
                        <h4 style="margin-bottom: 1rem; color: var(--accent-amber);">2. EMERGENCY CONTACTS</h4>
                        <ul style="list-style: none;">
                            <li style="margin-bottom: 0.75rem;">
                                <strong>Water Board:</strong> <a href="tel:155313">155313</a>
                            </li>
                            <li style="margin-bottom: 0.75rem;">
                                <strong>Health Department:</strong> <a href="tel:104">104</a>
                            </li>
                            <li style="margin-bottom: 0.75rem;">
                                <strong>Ward Officer:</strong> <a href="tel:07312563642">0731-2563642</a>
                            </li>
                        </ul>
                    </div>
                    
                    <div>
                        <h4 style="margin-bottom: 1rem; color: var(--accent-green);">3. MEDICAL RESPONSE</h4>
                        <ul style="list-style: none;">
                            <li style="margin-bottom: 0.75rem;">
                                <a href="https://www.google.com/maps/search/MY+Hospital+Indore" target="_blank" style="cursor: pointer; color: var(--accent-green); text-decoration: none; display: flex; align-items: center;">
                                    <i class="fas fa-hospital" style="margin-right: 0.5rem;"></i>
                                    Nearest hospital: MY Hospital (0.8km)
                                </a>
                            </li>
                            <li style="margin-bottom: 0.75rem;">
                                <i class="fas fa-prescription-bottle" style="margin-right: 0.5rem; color: var(--accent-green);"></i>
                                ORS preparation guide available
                            </li>
                            <li style="margin-bottom: 0.75rem;">
                                <i class="fas fa-file-medical" style="margin-right: 0.5rem; color: var(--accent-green);"></i>
                                Symptom monitoring sheet
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
            
            <button class="sos-button" id="sosButton">
                <i class="fas fa-phone-alt"></i>
                <span class="sos-text">EMERGENCY SOS - CALL 104</span>
            </button>

            <script>
                document.getElementById('sosButton').addEventListener('click', function() {
                    // Trigger phone call
                    window.location.href = 'tel:104';
                });
            </script>
        </div>
    </section>

    <!-- Report Form -->
    <section class="section" id="report">
        <div class="container">
            <div class="section-header">
                <h2 class="section-title">Report Water Issue</h2>
                <p class="section-subtitle">Help us identify and resolve problems faster</p>
            </div>
            
            <form class="report-form" id="reportForm">
                <div class="form-group">
                    <label class="form-label">Your Location</label>
                    <input type="text" class="form-control" placeholder="Enter ward/area name" required>
                </div>
                
                <div class="form-group">
                    <label class="form-label">Issue Type</label>
                    <div class="checkbox-group">
                        <label class="checkbox-label">
                            <input type="checkbox" name="issue" value="foul-smell"> Foul Smell
                        </label>
                        <label class="checkbox-label">
                            <input type="checkbox" name="issue" value="turbidity"> Turbidity
                        </label>
                        <label class="checkbox-label">
                            <input type="checkbox" name="issue" value="low-pressure"> Low Pressure
                        </label>
                        <label class="checkbox-label">
                            <input type="checkbox" name="issue" value="discoloration"> Discoloration
                        </label>
                    </div>
                </div>
                
                <div class="form-group">
                    <label class="form-label">Upload Water Photo</label>
                    <div class="upload-area" id="uploadArea">
                        <i class="fas fa-cloud-upload-alt"></i>
                        <p>Drag & drop or click to upload photo</p>
                        <p style="font-size: 0.875rem; color: var(--text-muted);">Max file size: 5MB</p>
                    </div>
                    <input type="file" id="fileInput" accept="image/*" style="display: none;">
                    <div id="filePreview" style="margin-top: 1rem;"></div>
                </div>
                
                <div class="form-group">
                    <label class="form-label">Description</label>
                    <textarea class="form-control" placeholder="Describe the water issue..." rows="4" required></textarea>
                </div>
                
                <div class="form-group">
                    <label class="form-label">Contact Number</label>
                    <input type="tel" class="form-control" placeholder="Your mobile number" pattern="[0-9]{10}" required>
                </div>
                
                <button type="submit" class="cta-button" style="width: 100%; justify-content: center;">
                    <i class="fas fa-paper-plane"></i>
                    Submit Report
                </button>
            </form>
            
            <script>
                const uploadArea = document.getElementById('uploadArea');
                const fileInput = document.getElementById('fileInput');
                const filePreview = document.getElementById('filePreview');
                const reportForm = document.getElementById('reportForm');
                
                // Click to upload
                uploadArea.addEventListener('click', () => fileInput.click());
                
                // Drag and drop events
                uploadArea.addEventListener('dragover', (e) => {
                    e.preventDefault();
                    uploadArea.style.borderColor = 'var(--accent-cyan)';
                    uploadArea.style.backgroundColor = 'rgba(6, 182, 212, 0.1)';
                });
                
                uploadArea.addEventListener('dragleave', () => {
                    uploadArea.style.borderColor = 'rgba(6, 182, 212, 0.3)';
                    uploadArea.style.backgroundColor = 'transparent';
                });
                
                uploadArea.addEventListener('drop', (e) => {
                    e.preventDefault();
                    uploadArea.style.borderColor = 'rgba(6, 182, 212, 0.3)';
                    uploadArea.style.backgroundColor = 'transparent';
                    
                    const files = e.dataTransfer.files;
                    handleFiles(files);
                });
                
                // File input change
                fileInput.addEventListener('change', (e) => {
                    handleFiles(e.target.files);
                });
                
                function handleFiles(files) {
                    if (files.length > 0) {
                        const file = files[0];
                        
                        // Validate file size (5MB)
                        if (file.size > 5 * 1024 * 1024) {
                            alert('File size must be less than 5MB');
                            return;
                        }
                        
                        // Validate file type
                        if (!file.type.startsWith('image/')) {
                            alert('Please upload an image file');
                            return;
                        }
                        
                        // Preview image
                        const reader = new FileReader();
                        reader.onload = (e) => {
                            filePreview.innerHTML = `
                                <div style="position: relative; display: inline-block; width: 100%;">
                                    <img src="${e.target.result}" style="width: 100%; max-width: 300px; border-radius: 0.5rem; border: 1px solid var(--accent-cyan);">
                                    <button type="button" onclick="removeFile()" style="position: absolute; top: 5px; right: 5px; background: var(--accent-red); color: white; border: none; width: 30px; height: 30px; border-radius: 50%; cursor: pointer; font-size: 1rem;">
                                        ✕
                                    </button>
                                </div>
                            `;
                        };
                        reader.readAsDataURL(file);
                    }
                }
                
                function removeFile() {
                    fileInput.value = '';
                    filePreview.innerHTML = '';
                }
                
                reportForm.addEventListener('submit', (e) => {
                    e.preventDefault();
                    alert('Thank you for reporting! Our team will investigate shortly.');
                    reportForm.reset();
                    filePreview.innerHTML = '';
                });
            </script>
