---
layout: default
title: Servers
---

<!--This feature Belongs to: Orlando-->


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Texting App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .messages {
            border: 1px solid #ccc;
            padding: 10px;
            max-height: 300px;
            overflow-y: scroll;
        }
        .input-container {
            margin-top: 10px;
        }
        .message-input{
            width: 1000px
            height: 100px
        }
    </style>
</head>
<body>
    <div id="messages"></div>
    <div id="input-container">
        <input type="text" id="messageInput" placeholder="Type your message...">
        <button onclick="sendMessage()">Send</button>
    </div>
    <script>
        function sendMessage() {
            const messageInput = document.getElementById('messageInput');
            const message = messageInput.value.trim();
            if (message !== '') {
                appendMessage('You', message);
                messageInput.value = '';
            }
        }
        function appendMessage(sender, text) {
            const messagesContainer = document.getElementById('messages');
            const messageElement = document.createElement('div');
            messageElement.innerHTML = `<strong>${sender}:</strong> ${text}`;
            messagesContainer.appendChild(messageElement);
            messagesContainer.scrollTop = messagesContainer.scrollHeight;
        }
    </script>
</body>
</html>
