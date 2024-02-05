---
layout: home
search_exclude: true
---

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PLACE 🏠</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
<link rel="stylesheet" href="style.css">
</head>
<body>
<nav id="navbar">
    <div class="logo">
        <h2>PLACE 🏠</h2>
    </div>
    <div class="nav-links">
        <a href="#login">Log in/Sign Up</a>
        <a href="#chatbot">Chatbot</a>
        <a href="#about">About Us</a>
    </div>
</nav>

<section id="hero">
    <h1>Welcome to PLACE</h1>
    <p>Your decentralized community space without paywalls.</p>
</section>

<section id="features">
    <div class="feature-box">
        <h3>Customizable Servers</h3>
        <p>With PLACE, you have the freedom to customize your servers for any purpose, without restrictions.</p>
    </div>
    <div class="feature-box">
        <h3>Decentralized Ecosystem</h3>
        <p>Experience a fully decentralized platform that puts the power back in the hands of the community.</p>
    </div>
    <div class="feature-box">
        <h3>Free to Use</h3>
        <p>Enjoy unlimited access to all features without any paywalls. PLACE is free for everyone.</p>
    </div>
</section>

<script src="script.js"></script>
</body>
</html>
<style>
body, html {
margin: 0;
padding: 0;
font-family: 'Poppins', sans-serif;
}
#navbar {
display: flex;
justify-content: space-between;
align-items: center;
background-color: #333;
color: #fff;
padding: 0 20px;
}
.nav-links a {
color: #fff;
text-decoration: none;
margin-left: 20px;
}
#hero {
background-color: #007bff;
color: #ffffff;
text-align: center;
padding: 50px 20px;
}
#features {
display: flex;
justify-content: space-around;
flex-wrap: wrap;
padding: 20px;
}
.feature-box {
width: 30%;
margin: 10px;
box-shadow: 0 0 10px rgba(0,0,0,0.1);
padding: 20px;
border-radius: 8px;
}
@media (max-width: 768px) {
.feature-box {
    width: 100%;
}
}
</style>
<script>
// Example of future JavaScript to enhance interactivity
document.addEventListener('DOMContentLoaded', () => {
// Placeholder for any JS-based interactivity you might want to add
});
</script>