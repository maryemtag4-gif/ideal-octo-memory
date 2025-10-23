<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>User Registration Form</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <form id="registration-form">
        <label for="username">Username:</label>
        <input type="text" id="username" required>

        <label for="email">Email:</label>
        <input type="email" id="email" required>

        <label for="password">Password:</label>
        <input type="password" id="password" required>

        <button type="submit">Register</button>
        <div id="form-feedback"></div>body {
    font-family: 'Arial', sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f5f5f5;
    margin: 0;
}

form {
    background: #ffffff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    width: 100%;
    max-width: 400px;
}

label {
    margin-bottom: 5px;
    font-weight: bold;
    color: #333;
}

input {
    padding: 10px;
    margin-bottom: 20px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: calc(100% - 22px); /* Adjust width to account for padding and border */
    box-sizing: border-box; /* Include padding and border in element's total width and height */
}

button {
    background-color: #007bff;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    width: 100%;
    box-sizing: border-box;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: #0056b3;
}

#form-feedback {
    margin-top: 10px;
    padding: 10px;
    color: #d8000c;
    background-color: #ffbaba;
    border-radius: 4px;
    display: none; /* Initially hide the feedback div */
}
    </form>
    <script src="script.js"></script>
</body>
</html># ideal-octo-memory// Setup and Initial Code Structure: Wrap the script in a DOMContentLoaded event listener.
document.addEventListener('DOMContentLoaded', () => {
    // Form Selection: Select the form and feedback div.
    const form = document.getElementById('registration-form');
    const feedbackDiv = document.getElementById('form-feedback');

    // Form Submission and Event Prevention: Add an event listener for form submission.
    form.addEventListener('submit', (event) => {
        // Prevent default form submission behavior.
        event.preventDefault();

        // Input Retrieval and Trimming: Get input values and trim whitespace.
        const usernameInput = document.getElementById('username');
        const emailInput = document.getElementById('email');
        const passwordInput = document.getElementById('password');

        const username = usernameInput.value.trim();
        const email = emailInput.value.trim();
        const password = passwordInput.value.trim();

        // Validation Logic: Initialize validation variables.
        let isValid = true;
        const messages = [];

        // Reset feedback div appearance before running validations
        // This is a good practice to clear previous error styling
        feedbackDiv.style.color = '#d8000c'; // Default error color
        feedbackDiv.style.backgroundColor = '#ffbaba'; // Default error background

        // --- Username Validation ---
        // Check if username.length is less than 3.
        if (username.length < 3) {
            isValid = false;
            messages.push("Username must be at least 3 characters long.");
        }

        // --- Email Validation ---
        // Check if email includes both '@' and '.' characters.
        // NOTE: This is a basic check; a real-world application would use a more robust regex.
        if (!email.includes('@') || !email.includes('.')) {
            isValid = false;
            messages.push("Please enter a valid email address (must contain '@' and '.').");
        }

        // --- Password Validation ---
        // Ensure password.length is at least 8.
        if (password.length < 8) {
            isValid = false;
            messages.push("Password must be at least 8 characters long.");
        }

        // Displaying Feedback: Logic to show success or error messages.
        // Make feedbackDiv visible.
        feedbackDiv.style.display = "block";

        if (isValid) {
            // Success Message
            feedbackDiv.textContent = "Registration successful!";
            feedbackDiv.style.color = "#28a745"; // Success text color
            feedbackDiv.style.backgroundColor = "#d4edda"; // Success background color
            
            // OPTIONAL: Clear the form fields after successful submission
            form.reset();
        } else {
            // Error Messages
            // Join messages with <br> and assign to innerHTML.
            feedbackDiv.innerHTML = messages.join('<br>');
            // Error colors were set before validation, but we explicitly set them here 
            // to ensure consistency if the initial setup was different.
            feedbackDiv.style.color = "#dc3545"; // Error text color (from requirements)
            feedbackDiv.style.backgroundColor = "#ffbaba"; // Error background color (from requirements)
        }
    });
});
