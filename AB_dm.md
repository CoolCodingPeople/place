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
            max-width: 600px;
            margin: 50px auto;
            border: 1px solid #ccc;
            border-radius: 10px;
            overflow: hidden;
        }
        .chat-window {
            height: 300px;
            overflow-y: scroll;
            padding: 10px;
        }
        .message-input {
            display: flex;
            padding: 10px;
        }
        input {
            flex: 1;
            padding: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            padding: 5px 10px;
            margin-left: 10px;
            cursor: pointer;
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
            <button onclick="sendMessage()">Send</button>
        </div>
    </div>
    <script src="script.js">
        function sendMessage() {
    var messageInput = document.getElementById("messageInput");
    var message = messageInput.value;
    if (message.trim() !== "") {
        var chatWindow = document.getElementById("chat-window");
        var newMessage = document.createElement("div");
        newMessage.className = "message";
        newMessage.textContent = message;
        chatWindow.appendChild(newMessage);
    }
}
    </script>
</body>
</html>
