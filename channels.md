<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Create Channel Prototype</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="app-container">
        <header>
            <h1>PLACE 🏠 Server: Example Server</h1>
        </header>
        <aside class="sidebar">
            <h2>Channels</h2>
            <ul id="channelList">
                <!-- Channels will be added here -->
            </ul>
            <button id="createChannelBtn">+ Create Channel</button>
        </aside>
        <main class="content">
            <div id="chatArea">
                <h2 id="selectedChannel">Welcome to Example Server!</h2>
                <div id="messages" class="messages"></div>
            </div>
            <form id="messageForm" class="message-form">
                <input type="text" id="messageInput" placeholder="Write a message..." autocomplete="off" required>
                <button type="submit">Send</button>
            </form>
        </main>
    </div>

    <!-- Create Channel Modal -->
    <div id="createChannelModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <form id="createChannelForm">
                <label for="channelName">Channel Name:</label>
                <input type="text" id="channelName" name="channelName" required>
                <input type="text" id="channelDesc" name="channelDesc" required>
                <button type="submit">Create Channel</button>
            </form>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>
<style>
body, html {
    margin: 0;
    padding: 0;
    font-family: Arial, sans-serif;
}

.app-container {
    display: flex;
    height: 100vh;
}

header {
    background-color: #7289da;
    color: white;
    padding: 10px;
    text-align: center;
}

.sidebar {
    background-color: #2c2f33;
    color: white;
    width: 240px;
    padding: 20px;
}

.sidebar h2, .content h2 {
    margin-top: 0;
}

.content {
    flex-grow: 1;
    padding: 20px;
}

.modal {
    display: none;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0,0,0,0.4);
}

.modal-content {
    background-color: #fefefe;
    margin: 15% auto;
    padding: 20px;
    border: 1px solid #888;
    width: 80%;
    max-width: 500px;
}

.close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
}

.close:hover,
.close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
}

#channelList {
    list-style: none;
    padding: 0;
}

#channelList li {
    padding: 10px 0;
    border-bottom: 1px solid #444;
    cursor: pointer;
}

.messages {
    border: 1px solid #ccc;
    margin-bottom: 10px;
    height: 300px;
    overflow-y: auto;
    padding: 10px;
    background-color: #f9f9f9;
}

.message-form {
    display: flex;
}

#messageInput {
    flex-grow: 1;
    padding: 10px;
    margin-right: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

#messageForm button {
    padding: 10px 20px;
    background-color: #7289da;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

#messageForm button:hover {
    background-color: #5b6eae;
}
</style>
<script>
document.getElementById('createChannelBtn').addEventListener('click', function() {
    document.getElementById('createChannelModal').style.display = 'block';
});

document.querySelector('.close').addEventListener('click', function() {
    document.getElementById('createChannelModal').style.display = 'none';
});

document.getElementById('createChannelForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const channelName = document.getElementById('channelName').value;
    const channelDesc = document.getElementById('channelDesc').value;
    if (channelName) {
        const li = document.createElement('li');
        li.textContent = channelName;
        document.getElementById('channelList').appendChild(li);
        document.getElementById('createChannelModal').style.display = 'none';
        document.getElementById('channelName').value = ''; // Reset input field
    }
    if (channelDesc) {
        const li = document.createElement('li');
        li.textContent = channelDesc;
        document.getElementById('channelList').appendChild(li);
        document.getElementById('createChannelModal').style.display = 'none';
        document.getElementById('channelDesc').value = ''; // Reset input field
    }
});

let selectedChannelName = '';

document.getElementById('messageForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const messageInput = document.getElementById('messageInput');
    const message = messageInput.value;
    if (message && selectedChannelName) {
        const messageElement = document.createElement('p');
        messageElement.textContent = `${selectedChannelName}: ${message}`;
        document.getElementById('messages').appendChild(messageElement);
        messageInput.value = ''; // Reset input field
    } else {
        alert('Please select a channel first.');
    }
});

document.getElementById('channelList').addEventListener('click', function(e) {
    if (e.target.tagName === 'LI') {
        selectedChannelName = e.target.textContent;
        document.getElementById('selectedChannel').textContent = `Channel: ${selectedChannelName}`;
        document.getElementById('messages').innerHTML = ''; // Clear previous messages
    }
});
</script>