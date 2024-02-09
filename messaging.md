---
layout: post
title: channel test
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Messaging System</title>
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            background-color: #ffffff;
            border-radius: 10px;
            box-shadow: 0px 14px 32px rgba(0, 0, 0, 0.1);
            padding: 40px;
            width: 80%;
            max-width: 500px;
        }

        .form-field {
            background-color: #f5f5f5;
            border: none;
            border-radius: 5px;
            margin-bottom: 20px;
            padding: 12px 20px;
            width: 100%;
        }

        .form-button {
            background-color: #6200ee;
            border: none;
            border-radius: 5px;
            color: #ffffff;
            cursor: pointer;
            padding: 12px 20px;
            text-transform: uppercase;
            width: 100%;
        }

        .form-button:hover {
            background-color: #3700b3;
        }

        .message-container {
            margin-bottom: 20px;
        }

        .message {
            background-color: #f5f5f5;
            border-radius: 5px;
            padding: 10px;
            margin-bottom: 10px;
        }

        .message .writer {
            font-weight: bold;
        }

        .message .time {
            font-size: 0.8em;
            color: #888888;
        }
    </style>
</head>

<body>
    <div class="container">
        <h1>Messaging System</h1>

        <div id="messagesContainer"></div>

        <form id="messageForm">
            <select id="channelSelect"></select>
            <input class="form-field" type="text" name="messageText" id="messageText" placeholder="Type your message"
                required>
            <button class="form-button">Send</button>
        </form>
    </div>

    <script>
        // Fetch available channels
        fetch('https://ccplace.stu.nighthawkcodingsociety.com/channel')
    //  fetch('localhost:8765/channel')
            .then(response => response.json())
            .then(data => {
                const channelSelect = document.getElementById('channelSelect');

                // Add options to the channel select dropdown
                data.channels.forEach(channel => {
                    const option = document.createElement('option');
                    option.value = channel.id;
                    option.text = channel.name;
                    channelSelect.appendChild(option);
                });
            })
            .catch(error => console.log('Error:', error));

        // Fetch and display messages
        function fetchMessages() {
            fetch('https://ccplace.stu.nighthawkcodingsociety.com/message')
                .then(response => response.json())
                .then(data => {
                    const messagesContainer = document.getElementById('messagesContainer');
                    messagesContainer.innerHTML = '';

                    // Display each message
                    data.messages.forEach(message => {
                        const messageDiv = document.createElement('div');
                        messageDiv.classList.add('message');

                        const writerSpan = document.createElement('span');
                        writerSpan.classList.add('writer');
                        writerSpan.textContent = message.writer;

                        const timeSpan = document.createElement('span');
                        timeSpan.classList.add('time');
                        timeSpan.textContent = message.time;

                        const textParagraph = document.createElement('p');
                        textParagraph.textContent = message.text;

                        messageDiv.appendChild(writerSpan);
                        messageDiv.appendChild(timeSpan);
                        messageDiv.appendChild(textParagraph);

                        messagesContainer.appendChild(messageDiv);
                    });
                })
                .catch(error => console.log('Error:', error));
        }

        // Periodically fetch messages every 2 seconds
        setInterval(fetchMessages, 2000);

        // Send a message
        const messageForm = document.getElementById('messageForm');
        messageForm.addEventListener('submit', function (event) {
            event.preventDefault();

            const channelId = document.getElementById('channelSelect').value;
            const messageText = document.getElementById('messageText').value;
            const writer = localStorage.getItem('localUsername');
            const time = new Date().toLocaleTimeString();

            const message = {
                text: messageText,
                writer: writer,
                time: time,
                channelId: channelId
            };

            const requestOptions = {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(message)
            };

            fetch('https://ccplace.stu.nighthawkcodingsociety.com/message', requestOptions)
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Error sending message');
                    }
                    document.getElementById('messageText').value = '';
                    fetchMessages();
                })
                .catch(error => console.log('Error:', error));
        });
    </script>
</body>

</html>