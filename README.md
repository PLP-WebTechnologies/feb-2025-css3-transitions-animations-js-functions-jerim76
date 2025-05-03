# CSS3 Transitions, Animations, and Advanced JavaScript Functions

## Objectives

Create smooth CSS transitions and animations.
Use JavaScript functions for dynamic behavior.
Implement local storage for data persistence.

## Instructions
Add CSS animations to elements like buttons or images.

>[!NOTE]
> - Write a JavaScript function that:
> - Stores and retrieves user preferences using localStorage.
> - Implements an animation triggered by user actions.

## Tasks

Create a CSS animation.
Store data in localStorage.
Apply JavaScript to trigger animations.

Happy Coding! 💻✨


HTML Structutre
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS Animations & localStorage Demo</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Animation & Preferences Demo</h1>
        
        <div class="preferences">
            <h2>User Preferences</h2>
            <div class="form-group">
                <label for="username">Username:</label>
                <input type="text" id="username" placeholder="Enter your name">
            </div>
            <div class="form-group">
                <label for="theme">Theme:</label>
                <select id="theme">
                    <option value="light">Light</option>
                    <option value="dark">Dark</option>
                    <option value="blue">Blue</option>
                </select>
            </div>
            <button id="savePrefs">Save Preferences</button>
            <button id="clearPrefs">Clear Preferences</button>
        </div>
        
        <div class="animation-area">
            <h2>Animation Controls</h2>
            <button id="animateBtn">Trigger Animation</button>
            <div class="animated-box" id="animatedElement">
                Watch me move!
            </div>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
Css style

/* Base styles */
body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    margin: 0;
    padding: 20px;
    transition: background-color 0.5s ease, color 0.5s ease;
}

.container {
    max-width: 800px;
    margin: 0 auto;
}

/* Theme styles */
.light {
    background-color: #f4f4f4;
    color: #333;
}

.dark {
    background-color: #333;
    color: #f4f4f4;
}

.blue {
    background-color: #e6f2ff;
    color: #003366;
}

/* Form styles */
.preferences {
    background: #fff;
    padding: 20px;
    margin-bottom: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.form-group {
    margin-bottom: 15px;
}

label {
    display: block;
    margin-bottom: 5px;
}

input, select {
    width: 100%;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
}

button {
    background: #007bff;
    color: white;
    border: none;
    padding: 10px 15px;
    margin-right: 10px;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s ease;
}

button:hover {
    background: #0056b3;
    transform: translateY(-2px);
}

/* Animation area styles */
.animation-area {
    background: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.animated-box {
    width: 150px;
    height: 150px;
    background: #007bff;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 30px auto;
    border-radius: 8px;
    transition: all 0.5s ease;
}

/* CSS Animation */
@keyframes slideAndBounce {
    0% {
        transform: translateX(0) scale(1);
    }
    25% {
        transform: translateX(100px) scale(1.1);
    }
    50% {
        transform: translateX(-100px) scale(1.2);
    }
    75% {
        transform: translateX(50px) scale(1.1);
    }
    100% {
        transform: translateX(0) scale(1);
    }
}

.animate {
    animation: slideAndBounce 1s ease-in-out;
}

/* Hover transition */
.animated-box:hover {
    transform: scale(1.05);
    background: #0056b3;
}
java
document.addEventListener('DOMContentLoaded', function() {
    // DOM Elements
    const usernameInput = document.getElementById('username');
    const themeSelect = document.getElementById('theme');
    const savePrefsBtn = document.getElementById('savePrefs');
    const clearPrefsBtn = document.getElementById('clearPrefs');
    const animateBtn = document.getElementById('animateBtn');
    const animatedElement = document.getElementById('animatedElement');
    const body = document.body;

    // Load saved preferences
    loadPreferences();

    // Save preferences to localStorage
    savePrefsBtn.addEventListener('click', function() {
        const preferences = {
            username: usernameInput.value,
            theme: themeSelect.value
        };
        
        localStorage.setItem('userPreferences', JSON.stringify(preferences));
        applyTheme(preferences.theme);
        
        // Show feedback animation
        this.textContent = 'Saved!';
        this.style.backgroundColor = '#28a745';
        setTimeout(() => {
            this.textContent = 'Save Preferences';
            this.style.backgroundColor = '#007bff';
        }, 1000);
    });

    // Clear preferences
    clearPrefsBtn.addEventListener('click', function() {
        localStorage.removeItem('userPreferences');
        usernameInput.value = '';
        themeSelect.value = 'light';
        applyTheme('light');
        
        // Show feedback animation
        this.textContent = 'Cleared!';
        this.style.backgroundColor = '#dc3545';
        setTimeout(() => {
            this.textContent = 'Clear Preferences';
            this.style.backgroundColor = '#007bff';
        }, 1000);
    });

    // Trigger animation
    animateBtn.addEventListener('click', function() {
        // Add animation class
        animatedElement.classList.add('animate');
        
        // Remove the class after animation completes to allow re-triggering
        setTimeout(() => {
            animatedElement.classList.remove('animate');
        }, 1000);
    });

    // Theme change handler
    themeSelect.addEventListener('change', function() {
        applyTheme(this.value);
    });

    // Load preferences from localStorage
    function loadPreferences() {
        const savedPrefs = localStorage.getItem('userPreferences');
        if (savedPrefs) {
            const preferences = JSON.parse(savedPrefs);
            usernameInput.value = preferences.username || '';
            themeSelect.value = preferences.theme || 'light';
            applyTheme(preferences.theme);
        }
    }

    // Apply theme to the page
    function applyTheme(theme) {
        // Remove all theme classes first
        body.classList.remove('light', 'dark', 'blue');
        
        // Add the selected theme class
        if (theme) {
            body.classList.add(theme);
        } else {
            body.classList.add('light');
        }
    }
});
