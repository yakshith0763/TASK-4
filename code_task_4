index.html:
<!DOCTYPE html>
<html>
<head>
    <title>Server Management</title>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
    <h1>Server Management</h1>
    
    <!-- Create Server Form -->
    <h2>Create Server</h2>
    <form id="createServerForm">
        <input type="text" placeholder="Name" id="serverName" required>
        <input type="text" placeholder="Language" id="serverLanguage" required>
        <input type="text" placeholder="Framework" id="serverFramework" required>
        <button type="submit">Create Server</button>
    </form>

    <!-- Server List -->
    <h2>Server List</h2>
    <ul id="serverList"></ul>

    <script src="app.js"></script>
</body>
</html>
styles.css (for basic styling):
body {
    font-family: Arial, sans-serif;
    margin: 20px;
}

h1 {
    text-align: center;
}

h2 {
    margin-top: 20px;
}

form {
    display: flex;
    flex-direction: column;
    margin: 10px;
}

input {
    margin: 5px;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 3px;
}

button {
    margin-top: 10px;
    padding: 5px 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    border: 1px solid #ccc;
    border-radius: 3px;
    padding: 10px;
    margin-bottom: 10px;
}

li button {
    background-color: red;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
}
app.js (JavaScript to interact with the API):
document.addEventListener("DOMContentLoaded", () => {
    const createServerForm = document.getElementById("createServerForm");
    const serverList = document.getElementById("serverList");

    // Function to fetch and display servers
    function displayServers() {
        fetch("/servers")
            .then((response) => response.json())
            .then((data) => {
                serverList.innerHTML = "";
                data.forEach((server) => {
                    const li = document.createElement("li");
                    li.innerHTML = `
                        <strong>${server.name}</strong> (ID: ${server.id})<br>
                        Language: ${server.language}<br>
                        Framework: ${server.framework}<br>
                        <button data-id="${server.id}">Delete</button>
                    `;
                    serverList.appendChild(li);
                });

                // Add event listeners to delete buttons
                const deleteButtons = serverList.querySelectorAll("button");
                deleteButtons.forEach((button) => {
                    button.addEventListener("click", (event) => {
                        const serverId = event.target.getAttribute("data-id");
                        deleteServer(serverId);
                    });
                });
            });
    }

    // Function to create a server
    function createServer(name, language, framework) {
        fetch("/servers", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                name: name,
                language: language,
                framework: framework,
            }),
        })
            .then(() => {
                createServerForm.reset();
                displayServers();
            })
            .catch((error) => console.error("Error creating server:", error));
    }

    // Function to delete a server
    function deleteServer(id) {
        fetch(`/servers/${id}`, {
            method: "DELETE",
        })
            .then(() => {
                displayServers();
            })
            .catch((error) => console.error("Error deleting server:", error));
    }

    // Event listener for form submission
    createServerForm.addEventListener("submit", (event) => {
        event.preventDefault();
        const name = document.getElementById("serverName").value;
        const language = document.getElementById("serverLanguage").value;
        const framework = document.getElementById("serverFramework").value;
        createServer(name, language, framework);
    });

    // Initial display of servers
    displayServers();
});
