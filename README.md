<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Will You Be My Valentine?</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      font-family: 'Arial', sans-serif;
      background-color: #ffe6e6;
      color: #ff3366;
      text-align: center;
      transition: background-color 0.3s ease; /* Smooth transition for background color */
    }

    .container {
      background-color: white;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    h1 {
      font-size: 36px;
      margin-bottom: 20px;
      color: #ff3366;
    }

    p {
      font-size: 18px;
      margin-bottom: 30px;
    }

    .button {
      padding: 10px 20px;
      font-size: 18px;
      color: white;
      background-color: #ff3366;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      text-decoration: none;
      margin: 10px; /* Add margin to space out the buttons */
    }

    .button:hover {
      background-color: #ff6699;
    }

    .no-button {
      margin-top: 20px;
      padding: 10px 20px;
      background-color: #cccccc;
      color: #333333;
      cursor: pointer;
    }

    .thank-you-message-container {
      display: none; /* Initially hidden */
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5); /* Semi-transparent background */
      justify-content: center;
      align-items: center;
      text-align: center;
    }

    .thank-you-message {
      background-color: white;
      border-radius: 15px;
      padding: 40px;
      color: purple;
      font-size: 28px;
      font-weight: bold;
    }

    .hearts {
      font-size: 40px;
      color: purple;
    }

    .emoji {
      font-size: 40px;
      margin-top: 20px;
    }

    /* Styling to make the buttons appear next to each other */
    .button-container {
      display: flex;
      justify-content: center; /* Center the buttons horizontally */
      gap: 20px; /* Add space between the buttons */
    }

  </style>
</head>
<body>
  <div class="container" id="container">
    <h1>Will You Be My Valentine?</h1>
    <p>Happy Valentine's Day! 💖</p>
    <button class="button" id="yes-button">Yes! 💌</button>
    <button class="no-button" id="no-button">No 💔</button>
    <div id="emoji-container"></div> <!-- This will display emojis based on clicks -->
  </div>

  <!-- The Popup Modal -->
  <div id="popup" class="thank-you-message-container">
    <div class="thank-you-message">
      <div class="hearts">❤️❤️❤️</div>
      <p>Thank you! I love you! 💖</p>
      <div class="hearts">❤️❤️❤️</div>
    </div>
  </div>

  <script>
    const yesButton = document.getElementById('yes-button');
    const noButton = document.getElementById('no-button');
    const container = document.getElementById('container');
    const emojiContainer = document.getElementById('emoji-container');
    const popup = document.getElementById('popup');
    let noButtonClicks = 0;  // Track how many times "No" has been clicked

    // Function to handle "No" button click
    noButton.addEventListener('click', function() {
      if (noButtonClicks < 10) {
        noButtonClicks++;

        // Darken the background with each "No" click
        let darknessLevel = 0.1 * noButtonClicks; // Increase darkness after each click
        if (darknessLevel >= 1) darknessLevel = 1; // Set maximum darkness (100% opacity)
        document.body.style.backgroundColor = `rgba(0, 0, 0, ${darknessLevel})`; // Adjust background color to black

        // Show emojis based on the number of "No" button clicks
        if (noButtonClicks === 5) {
          emojiContainer.innerHTML = "<div class='emoji'>😔</div>"; // Sad emoji after 5 clicks
        } else if (noButtonClicks === 7) {
          emojiContainer.innerHTML = "<div class='emoji'>😞</div>"; // Depressed emoji after 7 clicks
        } else if (noButtonClicks === 9) {
          emojiContainer.innerHTML = "<div class='emoji'>😡</div>"; // Angry emoji after 9 clicks
        }
      }

      // After 10 clicks, replace "No" with two "Yes" buttons next to each other
      if (noButtonClicks >= 10) {
        noButton.disabled = true; // Disable the "No" button
        noButton.style.display = 'none'; // Hide the "No" button

        // Create a container for the two "Yes" buttons
        const buttonContainer = document.createElement('div');
        buttonContainer.classList.add('button-container');

        // Add two "Yes" buttons next to each other
        const newYesButton1 = document.createElement('button');
        newYesButton1.classList.add('button');
        newYesButton1.textContent = 'Yes! 💌';
        newYesButton1.addEventListener('click', () => {
          // Open the modal (popup)
          popup.style.display = 'flex';
        });

        const newYesButton2 = document.createElement('button');
        newYesButton2.classList.add('button');
        newYesButton2.textContent = 'Yes! 💌';
        newYesButton2.addEventListener('click', () => {
          // Open the modal (popup)
          popup.style.display = 'flex';
        });

        // Add the buttons to the container
        buttonContainer.appendChild(newYesButton1);
        buttonContainer.appendChild(newYesButton2);

        // Add the button container to the main container
        container.appendChild(buttonContainer);
      }
    });

    // Function to handle initial "Yes" button click
    yesButton.addEventListener('click', function() {
      // Open the modal (popup)
      popup.style.display = 'flex';
    });

    // Close the popup if the user clicks on it (outside the message)
    popup.addEventListener('click', function(event) {
      if (event.target === popup) {
        popup.style.display = 'none';
      }
    });
  </script>
</body>
</html>
