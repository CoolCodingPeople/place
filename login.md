---
layout: post
title: Log-In
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Account Login</title>
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
</style>

<body>
    <div class="container">
        <form action="javascript:login_user()">
            <input class="form-field" type="text" name="uid" id="uid" placeholder="Username" required>
            <input class="form-field" type="password" name="password" id="password" placeholder="Password" required>
            <button class="form-button">Login</button>
            <button id="signUpButton" class="form-button" onclick="signUpSwitch()">Sign Up</button>
        </form>
        <!-- Account Details Screen (Initially Hidden) -->
        <div id="accountDetails" style="display: none;">
            <!-- Account details will go here -->
            <p>Welcome to your account. Your account details are displayed here.</p>
        </div>
    </div>
</body>
<script>
        document.addEventListener("DOMContentLoaded", function () {
            // Check if the user is logged in (You need to define your own logic for this)
            if (localStorage.getItem("loggedIn") === "true") {
                showAccountDetails();
            } else {
                showLoginScreen();
            }
        });
        function showAccountDetails() {
            document.getElementById("loginScreen").style.display = "none";
            document.getElementById("signUpButton").style.display = "none";
            document.getElementById("accountDetails").style.display = "block";
            // Create and append the email and stock elements
            const emailDiv = document.createElement("div");
            emailDiv.innerHTML = "Username: " + localStorage.getItem("localUsername");
            document.getElementById("accountDetails").appendChild(emailDiv);
            // Create a button element
            const button = document.createElement('button');
            button.innerText = 'LOG OUT';
            button.addEventListener('click', () => {
                // Remove the loggedIn flag from localStorage
                localStorage.removeItem("localUsername");
                localStorage.removeItem("localPassword");
                localStorage.removeItem("loggedIn");
                // Show the login screen
                showLoginScreen();
            });
            // Append the logout button to the account details section
            document.getElementById("accountDetails").appendChild(button);
        }
        function showLoginScreen() {
            document.getElementById("loginScreen").style.display = "block";
            document.getElementById("signUpButton").style.display = "block";
            document.getElementById("accountDetails").style.display = "none";
        }
        function signUpSwitch() {
            window.location.href = "/place/accountsignup";
        }
        function login_user() {
            // You can make a POST request here to your authentication endpoint
            var url = "https://ccplace.stu.nighthawkcodingsociety.com";
            // Comment out next line for local testing
            // url = "http://localhost:8085";
            const login_url = url + '/authenticate';
            const body = {
                username: document.getElementById("uid").value,
                password: document.getElementById("password").value,
            };
            console.log(JSON.stringify(body));
            const requestOptions = {
                method: 'POST',
                mode: 'no-cors',
                cache: 'no-cache',
                credentials: 'include',
                body: JSON.stringify(body),
                headers: {
                    "content-type": "application/json",
                    "Access-Control-Allow-Credentials": "true",
                    "Access-Control-Allow-Origin": "*",
                },
            };
            // Fetch JWT
            fetch(login_url, requestOptions)
                .then(response => {
                    if (!response.ok) {
                        const errorMsg = 'Login error: ' + response.status;
                        console.log(errorMsg);
                        return;
                    }
                    // Success!!!
                    // Redirect to Database location
                    localStorage.setItem("localUsername", document.getElementById("uid").value);
                    localStorage.setItem("localPassword", document.getElementById("password").value);
                    console.log(localStorage.getItem("localUsername"));
                    console.log(localStorage.getItem("localPassword"));
                    localStorage.setItem("loggedIn", "true");
                    showAccountDetails();
                    window.location.href = "/place/channels";
                });
        }
    </script>