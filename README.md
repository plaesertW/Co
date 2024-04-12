# Co 
<!DOCTYPE html>
<html>
<head>
    <title>Cookie Clicker</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Cookie Clicker</h1>
    <button id="cookieButton">Click me!</button>
    <div>
        Cookies: <span id="cookieCount">0</span>
    </div>
    <div>
        <h2>Upgrades:</h2>
        <div id="upgrades"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
CSS Styling: Add some basic styling to your website.

css
Copy code
/* styles.css */
body {
    text-align: center;
    font-family: Arial, sans-serif;
}
button {
    font-size: 24px;
    padding: 10px 20px;
}
JavaScript Functionality: Add JavaScript to handle the cookie clicking and upgrades.

javascript
Copy code
// script.js

let cookieCount = 0; // The number of cookies the user has
let cookiesPerClick = 1; // Number of cookies gained per click

// Function to update the cookie count display
function updateCookieCount() {
    const cookieCountElement = document.getElementById('cookieCount');
    cookieCountElement.innerText = cookieCount;
}

// Function to handle cookie clicks
function cookieClick() {
    cookieCount += cookiesPerClick;
    updateCookieCount();
}

// Attach the cookieClick function to the button
document.getElementById('cookieButton').addEventListener('click', cookieClick);

// Add upgrades functionality
const upgrades = [
    {name: 'Auto Clicker', cost: 50, effect: function() {
        setInterval(cookieClick, 1000);
    }},
    {name: 'Double Click', cost: 100, effect: function() {
        cookiesPerClick *= 2;
    }}
];

function createUpgradeButtons() {
    const upgradesDiv = document.getElementById('upgrades');
    upgrades.forEach((upgrade, index) => {
        const button = document.createElement('button');
        button.innerText = `${upgrade.name} (Cost: ${upgrade.cost})`;
        button.onclick = function() {
            if (cookieCount >= upgrade.cost) {
                cookieCount -= upgrade.cost;
                upgrade.effect();
                // Remove button after purchase to prevent multiple purchases
                button.remove();
                updateCookieCount();
            }
        };
        upgradesDiv.appendChild(button);
    });
}

// Create upgrade buttons on page load
createUpgradeButtons();
