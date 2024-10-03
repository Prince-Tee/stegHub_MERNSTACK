

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

To begin, Lauch an instance

![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/launch%20an%20instance%20on%20aws.png)

 SSH into your EC2 instance using Git Bash.

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
![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/server%20running%20on%20terminal%20node%20index.js.png)


### Opening Port 5000 on EC2 Security Groups



#### 1. Update Security Groups on AWS
- Log into your **AWS Management Console**.
- Navigate to **EC2 Dashboard**.
- Under **Network & Security**, select **Security Groups**.
- Choose the Security Group associated with your EC2 instance.
- Click **Edit inbound rules** and add a new rule:
  - **Type:** Custom TCP Rule
  - **Port Range:** 5000
  - **Source:** Anywhere 

  ![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/PORT%205000%20ON%20AWS.png)
  
#### 2. Access the Server
Once port 5000 is open, open a browser and try to access your server’s public IP or DNS name followed by `:5000`:

```bash
http://<PublicIP-or-PublicDNS>:5000
```

If configured properly, you should see the response from your Express server: **Welcome to Express**.

---
![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/WEB%20BROWSER%20AFTER%20CONFIGURE%20PORT%205000.png)

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
$ vim api.js
```
![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/routes%20created%20and%20apijs.png)
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

---


### Models

#### Step 1: Install Mongoose
Mongoose is a popular Node.js package that simplifies interaction with MongoDB.

1. First, navigate back to the **Todo** folder:

```bash
$ cd ..
```

2. Install **Mongoose** using npm:

```bash
$ npm install mongoose
```

#### Step 2: Create the `models` Folder
We will now create a folder to hold our models:

```bash
$ mkdir models
```

Change into the newly created `models` folder:

```bash
$ cd models
```

#### Step 3: Create the `todo.js` File
Inside the `models` folder, create a file named `todo.js` to define our To-Do model:

```bash
$ touch todo.js
```

For convenience, you can combine the above commands into a single line using `&&`:

```bash
$ mkdir models && cd models && touch todo.js
```

#### Step 4: Define the To-Do Schema and Model
Now, let's define the schema and model for our To-Do tasks. Open the `todo.js` file using Vim:

```bash
$ vim todo.js
```

Paste the following code into the file:

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

// Create schema for todo
const TodoSchema = new Schema({
  action: {
    type: String,
    required: [true, 'The todo text field is required']
  }
});

// Create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;
```

Save and exit the file with `:wq`.

---

### Updating the Routes to Use the New Model

Now that we have our **Todo** model, we need to update the **routes** to interact with the database. This will allow us to create, retrieve, and delete tasks directly from MongoDB.

#### Step 1: Modify the `api.js` File
Navigate back to the **routes** directory:

```bash
$ cd ../routes
```

Open the `api.js` file:

```bash
$ vim api.js
```

Clear the existing content using the command `:%d`, then paste the updated code below:

```javascript
const express = require('express');
const router = express.Router();
const Todo = require('../models/todo');

// Route to get all todos
router.get('/todos', (req, res, next) => {
  // This will return all the todos, exposing only the 'id' and 'action' fields to the client
  Todo.find({}, 'action')
    .then(data => res.json(data))
    .catch(next);
});

// Route to create a new todo
router.post('/todos', (req, res, next) => {
  if (req.body.action) {
    Todo.create(req.body)
      .then(data => res.json(data))
      .catch(next);
  } else {
    res.json({
      error: 'The input field is empty'
    });
  }
});

// Route to delete a todo by ID
router.delete('/todos/:id', (req, res, next) => {
  Todo.findOneAndDelete({ "_id": req.params.id })
    .then(data => res.json(data))
    .catch(next);
});

module.exports = router;
```

#### Explanation of the Updated Routes:
- **GET `/todos`**: Retrieves all To-Do items from the database and sends them to the client, displaying only the `id` and `action` fields.
- **POST `/todos`**: Creates a new To-Do item in the database if the `action` field is not empty.
- **DELETE `/todos/:id`**: Deletes a To-Do item by its unique ID from the database.

Save the file and exit Vim using `:wq`.

---
### Setting Up MongoDB Database

Now that our application is ready to store and manage data, let's integrate MongoDB as the database. We will use **MongoDB Atlas**, a cloud-hosted version of MongoDB, which makes it easy to set up and manage your database. Follow the steps below to set up your cluster, connect it to the application, and start managing your data.

#### Step 1: Create a New Project
1. Log in to [MongoDB Atlas](https://cloud.mongodb.com/).
2. Click on **"New Project"** to create a project for your cluster.
3. Name your project (e.g., "Todo App Project") and click **"Next"**.

![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/creating%20a%20project%20for%20mongodb.png)

---

#### Step 2: Create a Free Cluster
1. In the new project, click **"Build a Cluster"**.
2. Choose **"Shared Clusters"** and select the **Free Tier (M0)**.
3. Configure the cloud provider (choose **AWS**) and select a region closest to you that offers free-tier options.
4. Allow access to the MongoDB database from **anywhere** (ideal for testing purposes).
![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/allow%20access%20from%20anywhere%20for%20ip%20address.png)
5. Set the deletion timer for entries from **6 hours** to **1 week** for testing.

![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/cluster%20created.png)

---

#### Step 3: Set Up MongoDB User and Network Access
1. After creating the cluster, a pop-up will appear where you can set up **Network Access** and **Database User**.

##### Set Up MongoDB User:
1. Go to **"Database Access"** and click **"Add New Database User"**.
2. Choose **"Password"** as the authentication method.
3. Set the username and password (use a strong password for production).

![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/creating%20database.png)

##### Set IP Whitelist:
1. Navigate to **"Network Access"**, then click **"Add IP Address"**.
2. To allow access from anywhere, enter `0.0.0.0/0`. This is ideal for testing, but ensure stricter measures for production environments.

![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/allow%20access%20from%20anywhere%20for%20ip%20address.png)

---

#### Step 4: Get Connection String
1. After setting up the database user and network access, close the pop-up.
2. On the MongoDB Atlas dashboard, click **"Get connection string"**.
3. Choose the connection method for **Node.js** and copy the connection string.

The connection string will look like this:

```bash
mongodb+srv://username:<db_password>@todo-app-cluster.vj1ly.mongodb.net/?retryWrites=true&w=majority&appName=todo-app-cluster
```

#### Step 5: Create an Environment Variable File
To keep sensitive data such as the database connection string secure, we use an environment variable file (`.env`).

1. In your **Todo** directory, create an `.env` file using:

```bash
$ nano .env
```

2. Add the connection string to the `.env` file, replacing `<db_password>` with your actual database password:

```bash
DB = mongodb+srv://username:<db_password>@todo-app-cluster.vj1ly.mongodb.net/?retryWrites=true&w=majority&appName=todo-app-cluster
```


#### Step 6: Update `index.js` for MongoDB Connection

To connect your application to the MongoDB database, we need to update the `index.js` file. Delete the existing content in the file and replace it with the following code:

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

// Connect to the Database
mongoose.connect(process.env.DB, { 
  useNewUrlParser: true,
  useUnifiedTopology: true 
})
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

// Since mongoose promise is deprecated, we override it with node's promise
mongoose.Promise = global.Promise;

// Middleware to handle CORS
app.use((req, res, next) => {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
  next();
});

// Body parser middleware
app.use(bodyParser.json());

// Define routes
app.use('/api', routes);

// Error handling middleware
app.use((err, req, res, next) => {
  console.log(err);
  next();
});

// Start the server
app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```
![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/changing%20api%20js%20content.png)

#### Step 7: Start the Node.js Server

Finally, run the following command to start the server:

```bash
$ node index.js
```

This will start the server and connect the application to the MongoDB database.
![sudo apt upgrade](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/database%20connectned.png)


## 5. Testing Backend Code using Postman

Before building the frontend, we will test our backend API using Postman.

- **POST Request (Add To-Do)**

  URL: `http://your-ec2-url/api/todos`  
  Method: POST  
  Body: `{ "action": "finsih project 8 and 9" }`

  **Screenshot Placeholder:**  
  ![Postman POST](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/adding%20a%20body%20to%20the%20request.png)
  ![Postman POST](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/get200okay%20.png)
  

- **GET Request (Retrieve To-Dos)**

  URL: `http://your-ec2-url/api/todos`  
  Method: GET

  **Screenshot Placeholder:**  
  ![Postman GET](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/get%20request%20showing%20200%20ok.png)

- **DELETE Request (Delete To-Do)**

  URL: `http://your-ec2-url/api/todos/:id`  
  Method: DELETE

  **Screenshot Placeholder:**  
  ![Postman DELETE](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/delete%20operation%20worked%20by%20deleting%20using%20the%20ID.png)

---

### Frontend Creation for the To-Do App

Now that we’ve completed the backend functionality and API setup, it's time to create the user interface that will allow users to interact with our application via the API. We will use **React** to build the frontend of the To-Do app.

#### Step 1: Scaffold the React App
1. Open your terminal and navigate to the **Todo** directory (the root directory where your backend code resides).
2. Run the following command to scaffold a new React app within the `client` folder:

```bash
$ yarn create-react-app client
```

This will create a new folder called **client** inside the `Todo` directory, where all your React code will reside.

---

#### Step 2: Install Necessary Dependencies

Before running the React app, we need to install some dependencies to streamline our development process.

1. **Concurrently**: This package allows us to run both the backend and frontend servers simultaneously from a single terminal window.
   
   Install it by running:

   ```bash
   $ yarn add install concurrently --save-dev
   ```

2. **Nodemon**: This tool automatically restarts the Node.js server when code changes are detected, making development more efficient.

   Install it by running:

   ```bash
   $ yarn add install nodemon --save-dev
   ```

---

#### Step 3: Update `package.json` Scripts

To ensure that both the backend and frontend servers run concurrently, we need to modify the scripts in the `package.json` file in the **Todo** directory.

1. Open the **package.json** file located in the **Todo** folder.
2. Replace the `"scripts"` section with the following code:

```json
"scripts": {
  "start": "node index.js",
  "start-watch": "nodemon index.js",
  "dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
}
```

- **start**: This runs the backend server using Node.js.
- **start-watch**: This runs the backend server using Nodemon to automatically restart on changes.
- **dev**: This command runs both the backend and frontend servers concurrently.

---

#### Step 4: Configure Proxy for API Calls

To simplify how we call the backend API from the frontend, we can configure a proxy in the **client** folder.

1. Navigate to the **client** directory:

   ```bash
   $ cd client
   ```

2. Open the **package.json** file located in the **client** folder:

   ```bash
   $ nano package.json
   ```

3. Add the following key-value pair to the file:

```json
"proxy": "http://localhost:5000"
```

This configuration allows the React app to access the backend API by making requests directly to `http://localhost:5000` without needing to include the `/api/todos` path every time.

---

#### Step 5: Run the Application

Now that everything is configured, you can run the application and access it via the browser.

1. Ensure you are in the **Todo** directory:

   ```bash
   $ cd ../Todo
   ```

2. Start both the backend and frontend servers with the following command:

   ```bash
   $ npm run dev
   ```

The app should automatically open and start running on **localhost:3000**.

---
![Postman POST](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/application%20started.PNG)

### Important Note: Opening TCP Port 3000 on EC2

If you're running this app on an EC2 instance, ensure that **TCP port 3000** is open in your security group. You can add a new rule to your security group to allow access to the application from the Internet. Here's how:

1. Go to your AWS Management Console.
2. Navigate to **EC2 > Security Groups**.
3. Select the security group associated with your EC2 instance.
4. Edit the inbound rules and add a rule to allow traffic on port **3000**.

This will allow users to access your frontend on port 3000.

---

#### Create React Components

One of the advantages of React is its use of components, which promotes code reuse and modularity. For our To-Do app, we will create two stateful components and one stateless component.

1. Navigate to the **src** directory within the **client** folder:

```bash
cd src
```

2. Create a new folder called **components**:

```bash
mkdir components
```

3. Move into the **components** directory:

```bash
cd components
```

4. Inside the **components** directory, create three files: `Input.js`, `ListTodo.js`, and `Todo.js`:

```bash
touch Input.js ListTodo.js Todo.js
```

---

#### Step 6: Implement the Input Component

1. Open the **Input.js** file:

```bash
vi Input.js
```

2. Copy and paste the following code into the file:

```javascript
import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {
  state = {
    action: ""
  }

  addTodo = () => {
    const task = { action: this.state.action }

    if (task.action && task.action.length > 0) {
      axios.post('/api/todos', task)
        .then(res => {
          if (res.data) {
            this.props.getTodos();
            this.setState({ action: "" })
          }
        })
        .catch(err => console.log(err))
    } else {
      console.log('input field required')
    }
  }

  handleChange = (e) => {
    this.setState({
      action: e.target.value
    })
  }

  render() {
    let { action } = this.state;
    return (
      <div>
        <input type="text" onChange={this.handleChange} value={action} />
        <button onClick={this.addTodo}>add todo</button>
      </div>
    )
  }
}

export default Input;
```

3. To use Axios, which is a Promise-based HTTP client for the browser and Node.js, run the following command in your terminal:

```bash
$ npm install axios
```

---

####  Implement the ListTodo Component

1. Open the **ListTodo.js** file:

```bash
vi ListTodo.js
```

2. Copy and paste the following code into the file:

```javascript
import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {
  return (
    <ul>
      {
        todos && todos.length > 0 ?
          (
            todos.map(todo => {
              return (
                <li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
              )
            })
          )
          :
          (
            <li>No todo(s) left</li>
          )
      }
    </ul>
  )
}

export default ListTodo;
```

---

#### Step 8: Implement the Todo Component

1. Open the **Todo.js** file:

```bash
nano Todo.js
```

2. Copy and paste the following code into the file:

```javascript
import React, { Component } from 'react';
import axios from 'axios';

import Input from './Input';
import ListTodo from './ListTodo';

class Todo extends Component {
  state = {
    todos: []
  }

  componentDidMount() {
    this.getTodos();
  }

  getTodos = () => {
    axios.get('/api/todos')
      .then(res => {
        if (res.data) {
          this.setState({
            todos: res.data
          })
        }
      })
      .catch(err => console.log(err))
  }

  deleteTodo = (id) => {
    axios.delete(`/api/todos/${id}`)
      .then(res => {
        if (res.data) {
          this.getTodos()
        }
      })
      .catch(err => console.log(err))
  }

  render() {
    let { todos } = this.state;

    return (
      <div>
        <h1>My Todo(s)</h1>
        <Input getTodos={this.getTodos} />
        <ListTodo todos={todos} deleteTodo={this.deleteTodo} />
      </div>
    )
  }
}

export default Todo;
```

---

#### Step 9: Update the App Component

1. Navigate back to the **src** directory:

```bash
cd ..
```

2. Open the **App.js** file:

```bash
nano App.js
```

3. Copy and paste the following code into the file:

```javascript
import React from 'react';

import Todo from './components/Todo';
import './App.css';

const App = () => {
  return (
    <div className="App">
      <Todo />
    </div>
  );
}

export default App;
```

---

#### Step 10: Style the App

1. Open the **App.css** file:

```bash
vi App.css
```

2. Paste the following CSS code into the file:

```css
.App {
  text-align: center;
  font-size: calc(10px + 2vmin);
  width: 60%;
  margin-left: auto;
  margin-right: auto;
}

input {
  height: 40px;
  width: 50%;
  border: none;
  border-bottom: 2px #101113 solid;
  background: none;
  font-size: 1.5rem;
  color: #787a80;
}

input:focus {
  outline: none;
}

button {
  width: 25%;
  height: 45px;
  border: none;
  margin-left: 10px;
  font-size: 25px;
  background: #101113;
  border-radius: 5px;
  color: #787a80;
  cursor: pointer;
}

button:focus {
  outline: none;
}

ul {
  list-style: none;
  text-align: left;
  padding: 15px;
  background: #171a1f;
  border-radius: 5px;
}

li {
  padding: 15px;
  font-size: 1.5rem;
  margin-bottom: 15px;
  background: #282c34;
  border-radius: 5px;
  overflow-wrap: break-word;
  cursor: pointer;
}

@media only screen and (min-width: 300px) {
  .App {
    width: 80%;
  }

  input {
    width: 100%
  }

  button {
    width: 100%;
    margin-top: 15px;
    margin-left: 0;
  }
}

@media only screen and (min-width: 640px) {
  .App {
    width: 60%;
  }

  input {
    width: 50%;


  }

  button {
    width: 25%;
  }
}
```

---

#### Step 11: Start the Application

1. Navigate back to the **Todo** directory:

```bash
cd ..
```

2. Start both the backend and frontend servers using the following command:

```bash
$ npm run dev
```

---

### Testing Your Application

1. Open your browser and navigate to `http://<ip address>:3000`.
2. You should see your To-Do application interface, where you can add tasks, delete tasks, and see your tasks listed.
![Postman POST](https://github.com/Prince-Tee/stegHub_MERNSTACK/blob/main/screenshots_from_my_local_env/todo%20list.PNG)


### Conclusion

Congratulations! You've successfully created a full-stack To-Do application using the MERN stack. Your application allows users to add, view, and delete tasks through a user-friendly interface, all while communicating with a Node.js and MongoDB backend.

This documentation provides a comprehensive guide to setting up a MERN stack To-Do application on AWS EC2, including backend configuration, testing using Postman, and frontend creation with React.

---

