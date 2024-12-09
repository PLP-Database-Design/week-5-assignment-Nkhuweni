# Database Interacation in Web Applications

This demonstrates the cconnection of MySQL database and Node.js to create a simple API

## Requirements
- [Node.js](https://nodejs.org/) installed
-  MySQL installed and running
-  A code editor, like [Visual Studio Code](https://code.visualstudio.com/download)

## Setup
1. Clone the repository
2. Initialize the node.js environment
   ```
   npm init -y
   ```
3. Install the necessary dependancies
   ```
   npm install express mysql2 dotenv nodemon
   ```
4. Create a ``` server.js ``` and ```.env``` files
5. Basic ```server.js``` setup
   <br>
   
   ```js
   const express = require('express')
   const app = express()

   
   // Question 1 goes here

   // GET endpoint to retrieve all patients
app.get('/patients', (req, res) => {
  const query = 'SELECT patient_id, first_name, last_name, date_of_birth FROM patients';

  db.query(query, (err, results) => {
    if (err) {
      console.error('Error retrieving patients:', err);
      return res.status(500).json({ error: 'Failed to retrieve patients' });
    }
    res.json(results);
  });
});



   // Question 2 goes here

   // GET endpoint to retrieve all providers
app.get('/providers', (req, res) => {
  const query = 'SELECT first_name, last_name, provider_specialty FROM providers';

  db.query(query, (err, results) => {
    if (err) {
      console.error('Error retrieving providers:', err);
      return res.status(500).json({ error: 'Failed to retrieve providers' });
    }
    res.json(results);
  });
});



   // Question 3 goes here

   // GET endpoint to retrieve patients by their first name
app.get('/patients/:first_name', (req, res) => {
  const { first_name } = req.params; // Extract first_name from the request parameters
  const query = 'SELECT patient_id, first_name, last_name, date_of_birth FROM patients WHERE first_name = ?';

  db.query(query, [first_name], (err, results) => {
    if (err) {
      console.error('Error retrieving patients by first name:', err);
      return res.status(500).json({ error: 'Failed to retrieve patients' });
    }
    res.json(results);
  });
});



   // Question 4 goes here

   // GET endpoint to retrieve providers by their specialty
app.get('/providers/specialty/:specialty', (req, res) => {
  const { specialty } = req.params; // Extract the specialty from the route parameter
  const query = 'SELECT first_name, last_name, provider_specialty FROM providers WHERE provider_specialty = ?';

  db.query(query, [specialty], (err, results) => {
    if (err) {
      console.error('Error retrieving providers by specialty:', err);
      return res.status(500).json({ error: 'Failed to retrieve providers' });
    }
    if (results.length === 0) {
      return res.status(404).json({ message: 'No providers found for this specialty' });
    }
    res.json(results);
  });
});


   

   // listen to the server
   const PORT = 3000
   app.listen(PORT, () => {
     console.log(`server is runnig on http://localhost:${PORT}`)
   })
   ```
<br><br>

## Run the server
   ```
   nodemon server.js
   ```
<br><br>

## Setup the ```.env``` file
```.env
DB_USERNAME=root
DB_HOST=localhost
DB_PASSWORD=your_password
DB_NAME=hospital_db
```

<br><br>

## Configure the database connection and test the connection
Configure the ```server.js``` file to access the credentials in the ```.env``` to use them in the database connection

<br>

## 1. Retrieve all patients
Create a ```GET``` endpoint that retrieves all patients and displays their:
- ```patient_id```
- ```first_name```
- ```last_name```
- ```date_of_birth```

<br>

## 2. Retrieve all providers
Create a ```GET``` endpoint that displays all providers with their:
- ```first_name```
- ```last_name```
- ```provider_specialty```

<br>

## 3. Filter patients by First Name
Create a ```GET``` endpoint that retrieves all patients by their first name



<br>

## 4. Retrieve all providers by their specialty
Create a ```GET``` endpoint that retrieves all providers by their specialty

<br>


## NOTE: Do not fork this repository
