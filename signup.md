---
layout: post
title: Sign-Up
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Account Sign Up</title>
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
        <form action="javascript:signUpRequest()">
            <input class="form-field" type="text" name="legalName" id="legalName" placeholder="Username" required>
            <input class="form-field" type="text" name="uid" id="uid" placeholder="Email" required>
            <input class="form-field" type="password" name="password" id="password" placeholder="Password" required>
            <input class="form-field" type="text" name="dofb" id="dofb" placeholder="Birth Date (01-02-1234)" required>
            <button class="form-button">Sign Up</button>
            <button class="form-button" id="logInButton" onclick="logInSwitch()">Log In</button>
        </form>
        <div id="accountDetails" style="display: none;">
            <!-- Account details will go here -->
            <p>Welcome to your account. Your account details are displayed here.</p>
        </div>
    </div>
</body>

<script>
    function logInSwitch() {
        window.location.href = "/place/login";
    }

    function signUpUser() {
        console.log("signUpUser() called");
    //  var url = "https://ccplace.stu.nighthawkcodingsociety.com";
        var url = "http://localhost:8085";
            // Comment out next line for local testing
            // url = "http://localhost:8085";
            const login_url = url + '/api/person/post'; 
            const body = {
                name: document.getElementById("legalName").value,
                email: document.getElementById("uid").value,
                password: document.getElementById("password").value,
                dob: document.getElementById("dob").value,
            };

            console.log(JSON.stringify(body));
            const requestOptions = {
                method: 'POST',
                mode: 'cors',
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
                    console.log("success")
                    window.location.href = "/place/accountlogin";
                });
    }

    function signUpRequest() {
        var requestOptions = {
            method: 'POST',
            mode: 'cors',
            cache: 'no-cache',
            credentials: 'include',
        };

        let fetchName = document.getElementById("legalName").value
        let fetchEmail = document.getElementById("uid").value
        let fetchPassword = document.getElementById("password").value
        let fetchDob = document.getElementById("dofb").value

        fetch(`ccplace.stu.nighthawkcodingsociety.com/api/person/post?name=${fetchName}&email=${fetchEmail}&password=${fetchPassword}@123&dob=${fetchDob}`, requestOptions)
        .then(response => {
            if (!response.ok) {
                const errorMsg = 'Login error: ' + response.status;
                console.log(errorMsg);
                return;
            }
            // Success!!!
            // Redirect to Database location
            console.log("success")
            window.location.href = "/place/login";
        });
    }
</script>
