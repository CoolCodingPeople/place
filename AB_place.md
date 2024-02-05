---
layout: page
title: login
---
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
        function updateChat() {
      getMessages();
      setTimeout(updateChat, 2000); // Fetch messages every 2 seconds
    }
    function getMessages() {
      //fetch('https://place.stu.nighthawkcodingsociety.com/post')
         fetch('http://localhost:8765/post')
        .then(response => response.json())
        .then(messages => {
          // Reverse the order of messages so the newest is displayed at the top
          messages.reverse();
          const messagesContainer = document.getElementById('messages');
          messagesContainer.innerHTML = ''; // Clear existing messages
          messages.forEach(message => {
            displayMessage(message.writer, message.time, message.text);
          });
        })
        .catch(error => {
          console.error('Error fetching messages:', error);
        });
    }
    function sendMessage() {
      var inputMessage = document.getElementById('input-message').value;
      document.getElementById('input-message').value = '';
      var username = document.getElementById('username-input').value;
      // Get the current time
      var currentTime = getCurrentTime();
      const chatData = {
        "writer": username,
        "time": currentTime,
        "text": inputMessage
      };
      try {
        //fetch('https://place.stu.nighthawkcodingsociety.com/post', {
           fetch('http://localhost:8765/post', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(chatData),
        })
          .then(response => response.json())
          .then(result => {
            if (result.success) {
              // Display the sent message immediately
              displayMessage(username, currentTime, inputMessage);
            }
          })
          .catch(error => {
            console.error('Error:', error);
          });
      } catch (error) {
        console.error('Error:', error);
      }
      getMessages();
    }
    function getCurrentTime() {
      const now = new Date();
      const hours = now.getHours().toString().padStart(2, '0');
      const minutes = now.getMinutes().toString().padStart(2, '0');
      return `${hours}:${minutes}`;
    }
    // Call the updateChat function to start periodic updates
    updateChat();
    function displayMessage(writer, title, content) {
      const messageElement = document.createElement('div');
      messageElement.classList.add('message');
      const userElement = document.createElement('span');
      userElement.classList.add('user');
      userElement.textContent = writer + ': ';
      // Generate a random color for the user's name
      const randomColor = getRandomColor();
      userElement.style.color = randomColor;
      const userMessageElement = document.createElement('span');
      userMessageElement.classList.add('user-message');
      userMessageElement.textContent = content;
      const timestampElement = document.createElement('span');
      timestampElement.classList.add('timestamp');
      timestampElement.textContent = title;
      messageElement.appendChild(userElement);
      messageElement.appendChild(userMessageElement);
      messageElement.appendChild(timestampElement);
      const messagesContainer = document.getElementById('messages');
      messagesContainer.appendChild(messageElement);
      // Scroll to the bottom to show the latest messages
      messagesContainer.scrollTop = messagesContainer.scrollHeight;
    }
    // Function to generate a random color
    function getRandomColor() {
      const list = ["#FF5733", "#FFC300", "#5DBB63", "#6B66B5", "#4183D7"];
      const randomIndex = Math.floor(Math.random() * list.length);
      return list[randomIndex];
    } (edited) 
    </script>
</body>
</html>
