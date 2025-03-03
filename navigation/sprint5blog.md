---
layout: page
title: Sprint 5 Experience Blog
permalink: /sprint5/blog
---


### Purpose of our group code and site 

- Shows and teaches users about working with binary
- Our site is broken into multiple features that all relate to teaching aspects of binary through lessons, games, and quizzes.

### My Feture

- My page has lessons on the base aspects of Logic Gates
- Each lesson is followed by a quiz that shows that you understand each gate
- After finishing, you can count up your score, and imput it into a database so you can compare to other users or your previous scores

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
async function create_User() {
    const name = document.getElementById("name").value;
    const score = document.getElementById("score").value;

    if (!name || !score) {
        alert("Please fill in both fields!");
        return;
    }
}
```

## Selection

- When part of the data is asked for an action (Update/Delete) 
- This code makes sures it deletes the correct data entry rather than the entire database

```javascript
async function delete_User(userId) {
    if (!confirm("Are you sure you want to delete this user?")) {
        return; // Cancel the deletion if the user doesn't confirm
    }
}

    try {
        const response = await fetch("http://127.0.0.1:8887/api/lgate", {
            method: "DELETE",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({ id: userId }), // Send the ID to delete
        });
    }
```

## Iteration

```javascript
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
            });
}
```

- The Data.forEach() method is used to loop through each previous conversion fetch data from the backend and display it on the page.

# Parameters and return jsonify 

- In the backend, the POST request sends data to the server in the form of a JSON body containing values of 'name' and 'scoring',used by request.get_json(). 
- This data is then used to create and save a new user id, and the saved data is returned as a JSON response using jsonify(). 
- The GET request, on the other hand, does not have a request body, and it instead fetches all previously saved conversions from the database. These conversions are returned as a JSON array of dictionaries, also using jsonify(). 
- Both methods ensure that the data exchanged between the frontend and backend is in a structured JSON format, making it possible for the frontend to properly display the information

# Algorithm request

- In this system, the frontend communicates with the backend through an API to send and read the name and score values. 
- The POST request sends the conversion data as JSON, while the GET request returns a list of saved conversions in JSON format. If there's an error like no data is imputted, the frontend alerts the user, and the backend handles errors with appropriate responses. The system ensures smooth interaction between the frontend and backend through asynchronous API calls, data validation, and dynamic UI updates.

## Frontend Code Retrieval

```javascript
async function fetch_Data() {
    try {
        // Reference the table body
        const tableBody = document.querySelector("#dataTable tbody");
        tableBody.innerHTML = ""; // Clear any existing rows

        // Fetch data from the backend
        const response = await fetch("http://127.0.0.1:8887/api/lgate", {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
            },
        });
    }
}
```
