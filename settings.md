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
    </script>
</body>
</html>
