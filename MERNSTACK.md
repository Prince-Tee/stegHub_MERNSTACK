Here’s the detailed markdown file structure following the format you provided for your GitHub documentation of the MERN stack project.

---

# MERN Stack To-Do Application Documentation

This project is a full-stack To-Do application developed using MongoDB, Express.js, React.js, and Node.js (MERN Stack). The backend is set up on AWS EC2, and MongoDB is hosted on MongoDB Atlas.

---

## Table of Contents

1. [SSH into the EC2 Instance from Git Bash](#ssh-into-the-ec2-instance-from-git-bash)
2. [Backend Configuration](#backend-configuration)
   - [MongoDB Setup](#mongodb-setup)
3. [Installing ExpressJS](#installing-expressjs)
4. [Models](#models)
5. [Testing Backend Code using Postman](#testing-backend-code-using-postman)
6. [Frontend Creation](#frontend-creation)
7. [Running npm Concurrently](#running-npm-concurrently)

---

## 1. SSH into the EC2 Instance from Git Bash

To begin, SSH into your EC2 instance using Git Bash.

```bash
ssh -i "your-key.pem" ubuntu@ec2-your-instance-url.compute.amazonaws.com
```

**Screenshot Placeholder:**  
![SSH Access](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/ssh%20into%20the%20instance%20through%20git%20bash.png)

---

## 2. Backend Configuration


#### 1. Update and Upgrade Ubuntu
To ensure your Ubuntu server is up-to-date, first run the following commands:

```bash
sudo apt update
sudo apt upgrade
```
![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/running%20sudo%20apt%20upgrade.png)
#### 2. Install Node.js and npm
We'll install Node.js version 18 and npm (which is included) from the NodeSource repository.

Add the NodeSource repository:

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

Install Node.js:

```bash
sudo apt-get install -y nodejs
```

Verify the installation of Node.js and npm by checking their versions:

```bash
node -v
npm -v
```

#### 3. Set Up Application Code
Create a directory for your To-Do project:

```bash
mkdir Todo
```

Verify that the directory was created:

```bash
ls
```

#### 4. View Detailed Directory Information
To see more useful details about the files and directories, use the following command:

```bash
ls -lih
```

This command will show different properties of files and directories, including their size in a human-readable format. You can also explore more useful options for the `ls` command by running:

```bash
ls --help
```

#### 5. Change Directory to Your Project Folder
After creating the `Todo` directory, change your current working directory to `Todo`:

```bash
cd Todo
```

#### 6. Initialize Your Project with `npm init`
Now, initialize your project by creating a `package.json` file that will contain metadata and dependencies required for the application. Run:

```bash
npm init
```

Follow the prompts that appear. You can press `Enter` several times to accept the default values. At the end, confirm by typing `yes` to generate the `package.json` file.

---
![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/mkdir%20todo-npm%20init-packagejson.png)

2. **Configure MongoDB** by creating a `.env` file with the MongoDB URI.

3. **MongoDB Setup on Atlas**

   - Go to [MongoDB Atlas](https://cloud.mongodb.com/).
   - Create a cluster and a database.
   - Add your EC2 IP address to the whitelist in MongoDB Atlas under "Network Access".

   **Screenshot Placeholders:**  
   ![MongoDB Cluster Setup](path/to/mongodb-cluster-setup.png)  
   ![IP Whitelist](path/to/ip-whitelist.png)

---

#### . Install Express
To use Express, install it in your project by running the following command:

```bash
npm install express
```

#### 2. Create the `index.js` File
Next, create a file named `index.js` in your project directory:

```bash
touch index.js
```

Verify that the `index.js` file has been created by running the `ls` command:

```bash
ls
```

#### 3. Install the `dotenv` Module
The `dotenv` module allows you to load environment variables from a `.env` file into your application. Install it with the following command:

```bash
npm install dotenv
```

#### 4. Open and Edit `index.js`
Now, open the `index.js` file for editing:

```bash
nano index.js
```

Once the file is open, add the following code into it:

```javascript
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
  next();
});

app.use((req, res, next) => {
  res.send('Welcome to Express');
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

#### 5. Start the Server
Once you’ve saved your changes, start the Express server with the following command:

```bash
node index.js
```

If everything works correctly, you should see the following message in your terminal:

```
Server running on port 5000
```
### Opening Port 5000 on EC2 Security Groups

![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/server%20running%20on%20terminal%20node%20index.js.png)

#### 1. Update Security Groups on AWS
- Log into your **AWS Management Console**.
- Navigate to **EC2 Dashboard**.
- Under **Network & Security**, select **Security Groups**.
- Choose the Security Group associated with your EC2 instance.
- Click **Edit inbound rules** and add a new rule:
  - **Type:** Custom TCP Rule
  - **Port Range:** 5000
  - **Source:** Anywhere 
  
#### 2. Access the Server
Once port 5000 is open, open a browser and try to access your server’s public IP or DNS name followed by `:5000`:

```bash
http://<PublicIP-or-PublicDNS>:5000
```

If configured properly, you should see the response from your Express server: **Welcome to Express**.

---

### Creating Routes for the To-Do Application

Now that the server is running, it's time to create the backend routes for the core functionality of the To-Do app.

#### 1. Creating the `routes` Folder
First, let's create a directory named `routes` to store our route files:

```bash
$ mkdir routes
```

#### 2. Navigate to the `routes` Folder
Now, change into the newly created `routes` directory:

```bash
$ cd routes
```

#### 3. Create the `api.js` File
Next, we’ll create a file named `api.js` inside the `routes` folder:

```bash
$ touch api.js
```

#### 4. Define the Routes in `api.js`
Now, open the `api.js` file using Vim:

```bash
$ nano api.js
```

Copy and paste the following code into the file:

```javascript
const express = require('express');
const router = express.Router();

// Route to display all tasks (GET)
router.get('/todos', (req, res, next) => {
  // Code to fetch and return all tasks goes here
});

// Route to create a new task (POST)
router.post('/todos', (req, res, next) => {
  // Code to create a new task goes here
});

// Route to delete a task (DELETE)
router.delete('/todos/:id', (req, res, next) => {
  // Code to delete a task by its ID goes here
});

module.exports = router;
```

#### Explanation of the Code:
- **GET** `/todos`: This route will be responsible for fetching and displaying all the tasks in the To-Do list.
- **POST** `/todos`: This route will allow users to create a new task.
- **DELETE** `/todos/:id`: This route will delete a task by its ID.

Use `:w` to save the file and `:qa` to exit Vim.

#### 5. Integrating Routes in `index.js`
Finally, we need to link these routes to our main application. Open the `index.js` file and update it to include the routes we just created:

```javascript
const express = require('express');
require('dotenv').config();

const app = express();

// Middleware to handle JSON data
app.use(express.json());

const port = process.env.PORT || 5000;

// Import the routes
const apiRoutes = require('./routes/api');

// Use the imported routes
app.use('/api', apiRoutes);

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

This updates the server to use the `api.js` routes we just created.

---


## 4. Models

We will create the MongoDB models for storing our To-Do tasks.

1. Create a `models` directory and a `Todo.js` file:

   ```bash
   mkdir models
   touch models/Todo.js
   ```

2. Define the model schema:

   ```javascript
   const mongoose = require('mongoose');

   const TodoSchema = new mongoose.Schema({
     action: {
       type: String,
       required: true
     }
   });

   module.exports = mongoose.model('Todo', TodoSchema);
   ```

**Screenshot Placeholder:**  
![Todo Model](path/to/model-structure.png)

---

## 5. Testing Backend Code using Postman

Before building the frontend, we will test our backend API using Postman.

- **POST Request (Add To-Do)**

  URL: `http://your-ec2-url/api/todos`  
  Method: POST  
  Body: `{ "action": "Sample To-Do Task" }`

  **Screenshot Placeholder:**  
  ![Postman POST](path/to/postman-post.png)

- **GET Request (Retrieve To-Dos)**

  URL: `http://your-ec2-url/api/todos`  
  Method: GET

  **Screenshot Placeholder:**  
  ![Postman GET](path/to/postman-get.png)

- **DELETE Request (Delete To-Do)**

  URL: `http://your-ec2-url/api/todos/:id`  
  Method: DELETE

  **Screenshot Placeholder:**  
  ![Postman DELETE](path/to/postman-delete.png)

---

## 6. Frontend Creation

For the frontend, we will be using React.

1. Move to the client directory:

   ```bash
   cd client
   ```

2. Create React components:

   ```bash
   mkdir src/components
   touch src/components/Input.js src/components/ListTodo.js src/components/Todo.js
   ```

3. **Input Component (`Input.js`)**:
   This handles input for new To-Dos and sends them to the backend.

   ```javascript
   import React, { Component } from 'react';
   import axios from 'axios';

   class Input extends Component {
     state = { action: "" }

     addTodo = () => {
       const task = { action: this.state.action };
       if (task.action && task.action.length > 0) {
         axios.post('/api/todos', task).then(res => {
           if (res.data) {
             this.props.getTodos();
             this.setState({ action: "" });
           }
         }).catch(err => console.log(err));
       } else {
         console.log('Input field required');
       }
     }

     handleChange = (e) => {
       this.setState({ action: e.target.value });
     }

     render() {
       return (
         <div>
           <input type="text" onChange={this.handleChange} value={this.state.action} />
           <button onClick={this.addTodo}>Add Todo</button>
         </div>
       );
     }
   }

   export default Input;
   ```

4. **Todo List Component (`ListTodo.js`)**:
   This component displays all To-Do tasks and allows for deletion.

   ```javascript
   import React from 'react';

   const ListTodo = ({ todos, deleteTodo }) => (
     <ul>
       {todos && todos.length > 0 ? (
         todos.map(todo => (
           <li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
         ))
       ) : (
         <li>No todo(s) left</li>
       )}
     </ul>
   );

   export default ListTodo;
   ```

5. **Main Todo Component (`Todo.js`)**:
   This is the main component that integrates both input and list components.

   ```javascript
   import React, { Component } from 'react';
   import axios from 'axios';
   import Input from './Input';
   import ListTodo from './ListTodo';

   class Todo extends Component {
     state = { todos: [] }

     componentDidMount() {
       this.getTodos();
     }

     getTodos = () => {
       axios.get('/api/todos').then(res => {
         if (res.data) {
           this.setState({ todos: res.data });
         }
       }).catch(err => console.log(err));
     }

     deleteTodo = (id) => {
       axios.delete(`/api/todos/${id}`).then(res => {
         if (res.data) {
           this.getTodos();
         }
       }).catch(err => console.log(err));
     }

     render() {
       return (
         <div>
           <h1>My Todo(s)</h1>
           <Input getTodos={this.getTodos} />
           <ListTodo todos={this.state.todos} deleteTodo={this.deleteTodo} />
         </div>
       );
     }
   }

   export default Todo;
   ```

**Screenshot Placeholder:**  
![React Components Setup](path/to/react-setup.png)

---

## 7. Running npm Concurrently

To run the backend and frontend concurrently, you need to configure `concurrently`:

1. Install `concurrently`:

   ```bash
   yarn add concurrently --save-dev
   ```

2. Update the `package.json` file:

   ```json
   "scripts": {
     "start": "node server.js",
     "client": "cd client && yarn start",
     "dev": "concurrently \"yarn run server\" \"yarn run client\""
   }
   ```

3. Run the following command to start both backend and frontend:

   ```bash
   yarn run dev
   ```

**Screenshot Placeholder:**  
![Running Concurrently](path/to/concurrently.png)

---

## Conclusion

This documentation provides a comprehensive guide to setting up a MERN stack To-Do application on AWS EC2, including backend configuration, testing using Postman, and frontend creation with React.

---

Feel free to let me know if you need to adjust or refine anything further!
