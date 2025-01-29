---
layout: page
title: Binary Converter Blog
permalink: /sprint5/blog
---


### Purpose of our group code and site 

- Shows and teaches users about working with binary
- Our site is broken into multiple features that all relate to teaching aspects of binary

### My Code 

- My page has lessons on the base aspects of Logic Gates
- Each lesson is followed by a quiz that shows that you understand each gate
- After finishing, you can count up your score, and imput it into a database so it can save into the backend

### Input / Output

```javascript

// Take the given data and POST into the database
async function create_User() {
    const name = document.getElementById("name").value;
    const score = document.getElementById("score").value;

    if (!name || !score) {
        alert("Please fill in both fields!");
        return;
    }

    const data = { name, score };

    try {
        const response = await fetch("http://127.0.0.1:8887/api/lgate", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(data),
        });

        const result = await response.json();

        if (response.ok) {
            alert("Data saved successfully!");
            console.log(result); // Optional: Log the response
        } else {
            alert(`Error: ${result.error}`);
        }
    } catch (error) {
        console.error("Error:", error);
        alert("Failed to connect to the server.");
    }
}
```

```javascript
// Retrive the data in the backend and GET to show to the frontend
async function fetch_Data() {
    try {
        // Reference the table body
        const tableBody = document.querySelector("#dataTable tbody");
        tableBody.innerHTML = "";

        // Fetch data from the backend
        const response = await fetch("http://127.0.0.1:8887/api/lgate", {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
            },
        });

        if (response.ok) {
            const data = await response.json();

            // Loop through the data to populate rows
            data.forEach((item) => {
                const row = document.createElement("tr");

                // Add Name cell
                const nameCell = document.createElement("td");
                nameCell.textContent = item.name;
                row.appendChild(nameCell);

                // Add Score cell
                const scoreCell = document.createElement("td");
                scoreCell.textContent = item.score;
                row.appendChild(scoreCell);

                // Add Action cell with delete button
                const actionCell = document.createElement("td");
                const deleteButton = document.createElement("button");
                deleteButton.textContent = "Delete";
                deleteButton.onclick = () => delete_User(item.id); // Pass the ID to the delete function
                actionCell.appendChild(deleteButton);
                row.appendChild(actionCell);

                // Append the row to the table body
                tableBody.appendChild(row);
            });
        } else {
            console.error("Failed to fetch data:", await response.text());
        }
    } catch (error) {
        console.error("Error fetching data:", error);
    }
}
```

- After imputing you data, the backend can retrive this and save
- Then press view other scores, which will then take the data from the backend and show the other scores recived from other users who have saved their score


### List Request Sample

```javascript
quizzes = [
            lgate(name="Jake", score="3"),
            lgate(name="Josh", score="4")
        ]
```

- The code looks for the values of 'name' and 'score'
- This data is taken and sent to the database as the default data
- When the frontend makes a GET request to the backend, it finds the previous scores, they displays when it is prompted on the frontend. 

## Algorithmic Function 

### Demonstration of sequencing, selection, and iteration 

## Sequencing

- When the user clicks the "Create User" button, the following happens step-by-step:

```javascript
data.forEach((item) => {
                const row = document.createElement("tr");

                // Add Name cell
                const nameCell = document.createElement("td");
                nameCell.textContent = item.name;
                row.appendChild(nameCell);

                // Add Score cell
                const scoreCell = document.createElement("td");
                scoreCell.textContent = item.score;
                row.appendChild(scoreCell);
});
```
- ! Note: this not the entire code
- Gets the user data that is imputed
- Makes sure the data is valid
- POST and save the user data into the user_management.db
- Fetches and displays previous conversions from the backend.

```javascript
if (decimalInput === '') {  // Check if input is empty
    alert('Please enter a decimal number!');
    return;
}
const decimalNumber = parseInt(decimalInput);
if (isNaN(decimalNumber) || decimalNumber < 0) {  // Check if input is a valid number
    alert('Please enter a positive decimal number.');
    return;
}
```

## Selection

- In the convertToBinary function, there are two places where selection is used:
  - If the input is empty, the function alerts the user and exits.
  - If the input is not a valid decimal number, the function alerts the user and exits.

- The event listener attached to the button also involves selection. The function convertToBinary is executed only when the Convert to Binary button is clicked, which is a form of conditional execution.

```javascript
document.addEventListener('DOMContentLoaded', () => {
    document.getElementById('convert-button').addEventListener('click', convertToBinary);  // Selection
    fetchAndDisplayBinaryConversion();  // Selection: Fetch previous conversions
});
```

## Iteration

```javascript
argumentsData.forEach((convert) => {  // Iterating over the list of previous conversions
    const conversionElement = document.createElement('p');
    conversionElement.textContent = `${convert.decimal}: ${convert.binary}`;
    conversionContainer.appendChild(conversionElement);
});
```

- The argumentsData.forEach() method is used to loop through each previous conversion fetch data from the backend and display it on the page.

# Parameters and return jsonify 

- In the backend, the POST request sends data to the server in the form of a JSON body containing decimal and binary values, which is parsed using request.get_json(). 
- This data is then used to create and save a new BinaryConverter object, and the saved data is returned as a JSON response using jsonify(). 
- The GET request, on the other hand, does not have a request body, and it fetches all previously saved binary conversions from the database. These conversions are returned as a JSON array of dictionaries, also using jsonify(). 
- Both methods ensure that the data exchanged between the frontend and backend is in a structured JSON format, making it easy for the frontend to handle.

# Algorithm request

- In this system, the frontend communicates with the backend through an API to convert decimal numbers into binary and store these conversions. 
- The system features two primary operations: converting decimal to binary and saving the results to a database. It also allows the frontend to fetch and display a list of previous conversions. 
- The system involves a frontend and backend working together to convert decimal numbers to binary and store them. The frontend (HTML + JavaScript) allows users to input a decimal number, convert it to binary, and display the result in a table. 
- It uses JavaScript to validate input, convert numbers, and send POST requests to the backend (Flask API) to save the conversion. The frontend also fetches previous conversions with GET requests to display all stored conversions. The backend (Flask) handles POST requests by saving new conversions to a database and GET requests by fetching all stored conversions. 
- The POST request sends the conversion data as JSON, while the GET request returns a list of saved conversions in JSON format. If there's an error (e.g., invalid input or server failure), the frontend alerts the user, and the backend handles errors with appropriate responses. The system ensures smooth interaction between the frontend and backend through asynchronous API calls, data validation, and dynamic UI updates.

## Frontend Code

```javascript
async function convertToBinary() {
    const decimalInput = document.getElementById('decimal-input').value.trim();
    if (decimalInput === '' || isNaN(parseInt(decimalInput)) || parseInt(decimalInput) < 0) {
        alert('Please enter a valid positive decimal number!');
        return;
    }
    const decimalNumber = parseInt(decimalInput);
    const binaryNumber = decimalNumber.toString(2);
    const tableBody = document.querySelector('#binary-table tbody');
    const newRow = document.createElement('tr');
    newRow.innerHTML = `<td>${decimalNumber}</td><td>${binaryNumber}</td>`;
    tableBody.appendChild(newRow);
    document.getElementById('decimal-input').value = '';
    await saveConversion(decimalNumber, binaryNumber);
    fetchAndDisplayBinaryConversion();
}
```

## Sends data to the backend

```javascript
async function saveConversion(decimal, binary) {
    const conversionData = { decimal, binary };
    const response = await fetch(`${pythonURI}/api/binary-converter`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(conversionData),
    });
    if (!response.ok) {
        const errorText = await response.text();
        console.error(`Error saving conversion: ${errorText}`);
    }
}
```

## Fetches previous conversions 

- This function fetches previously saved conversions from the backend via a GET request and updates the UI with the results.

```javascript
async function fetchAndDisplayBinaryConversion() {
    try {
        const response = await fetch(`${pythonURI}/api/binary-converter`, {
            method: 'GET',
            headers: { 'Content-Type': 'application/json' }
        });
        if (!response.ok) {
            throw new Error(`Failed to fetch conversions: ${response.statusText}`);
        }
        const argumentsData = await response.json();
        argumentsData.reverse();
        const conversionContainer = document.getElementById('previousConversions');
        conversionContainer.innerHTML = "<p><strong>Previous Conversions:</strong></p>";
        argumentsData.forEach((convert) => {
            const conversionElement = document.createElement('p');
            conversionElement.textContent = `${convert.decimal}: ${convert.binary}`;
            conversionContainer.appendChild(conversionElement);
        });
    } catch (error) {
        console.error('Error fetching conversions:', error);
    }
}
```
