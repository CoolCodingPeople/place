---
layout: post
title: Settings
---

<!--This feature Belongs to: Mati -->

<html>
<head>
    <title>background color</title>
    <style>
        body {
            background-color: #ffffff; /* default background color */
        }
        .word-option {
            display: inline-block;
            width: 50px;
            height: 50px;
            margin: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Word Picker</h1>
    <div class="word-option"  onclick="changeBackgroundColor('#ff0000')">Red</div>
    <div class="word-option"  onclick="changeBackgroundColor('#00ff00')">Green</div>
    <div class="word-option"  onclick="changeBackgroundColor('#0000ff')">Blue</div>
    <script>
        function changeBackgroundColor(color) {
            document.body.style.backgroundColor = color;
            localStorage.setItem('backgroundColor', color);
        }

        // Check if there is a stored background color
        const storedColor = localStorage.getItem('backgroundColor');
        if (storedColor) {
            document.body.style.backgroundColor = storedColor;
        }

        // Array of colors to cycle through
        const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff'];
        let currentIndex = 0;

        // Function to change the background color every 0.1 seconds
        function autoChangeBackgroundColor() {
            changeBackgroundColor(colors[currentIndex]);
            currentIndex = (currentIndex + 1) % colors.length;
        }

        // Call the function every 0.1 seconds
        setInterval(autoChangeBackgroundColor, 100);
    </script>
</body>
</html>
