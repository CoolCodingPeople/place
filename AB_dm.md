---
layout: default
title: Direct Messaging
---
<html lang="en">
<head>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        .chat-container {
            max-width: 800px; 
            margin: 50px auto;
            border: 1px solid #ccc;
            border-radius: 10px;
            overflow: hidden; 
        }
        .chat-window {
            height: 400px; 
            overflow-y: scroll;
            padding: 10px;
        }
        .message-input {
            display: flex;
            padding: 10px;
        }
        input {
            flex: 1;
            padding: 10px; 
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            padding: 10px 20px; 
            margin-left: 10px;
            cursor: pointer;
        }
        .message {
            margin-bottom: 10px;
        }
        .user1 {
            background-color: #c2e1f6;
        }
        .user2 {
            background-color: #f5f5f5;
        }
        button {
            padding: 10px 20px;
            margin-left: 10px;
            cursor: pointer;
            font-size: 16px;
        }
    </style>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Person-to-Person Messaging</title>
</head>
<body>
    <div class="chat-container">
        <div class="chat-window" id="chat-window"></div>
        <div class="message-input">
            <input type="text" id="messageInput" placeholder="Type your message...">
            <button onclick="sendMessage">&#10148;</button>
        </div>
    </div>
    <script src="script.js"></script>
    <script>
        function sendMessage() {
            var messageInput = document.getElementById("messageInput");
            var message = messageInput.value;
            if (message.trim() !== "") {
                fetch('http://localhost:8080/messages', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({ user: 'User1', text: message }), 
                })
                .then(response => response.json())
                .then(data => {
                    displayMessage(data);
                    messageInput.value = "";
                })
                .catch(error => console.error('Error:', error));
            }
        }
        document.addEventListener('DOMContentLoaded', function() {
            fetch('http://localhost:8080/messages')
                .then(response => response.json())
                .then(messages => {
                    messages.forEach(message => displayMessage(message));
                })
                .catch(error => console.error('Error:', error));
        });
        document.getElementById("messageInput").addEventListener("keyup", function(event) {
            if (event.key === "Enter") {
                sendMessage();
            }
        });
    </script>
</body>
</html>
