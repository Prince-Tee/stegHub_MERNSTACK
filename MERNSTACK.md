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
![SSH Access](path/to/ssh-screenshot.png)

---

## 2. Backend Configuration

We will start by configuring the backend of the application.

1. **Install necessary dependencies** using Yarn:

   ```bash
   yarn init
   yarn add express mongoose dotenv nodemon
   ```

2. **Configure MongoDB** by creating a `.env` file with the MongoDB URI.

3. **MongoDB Setup on Atlas**

   - Go to [MongoDB Atlas](https://cloud.mongodb.com/).
   - Create a cluster and a database.
   - Add your EC2 IP address to the whitelist in MongoDB Atlas under "Network Access".

   **Screenshot Placeholders:**  
   ![MongoDB Cluster Setup](path/to/mongodb-cluster-setup.png)  
   ![IP Whitelist](path/to/ip-whitelist.png)

---

## 3. Installing ExpressJS

To handle the backend API routes, install ExpressJS:

```bash
yarn add express
```

**Screenshot Placeholder:**  
![Express Installation](path/to/express-install.png)

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
