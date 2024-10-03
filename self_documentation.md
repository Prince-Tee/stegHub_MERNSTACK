

### Self-Study Documentation Summary

#### Project Overview
This project involves creating a To-Do application using the MERN (MongoDB, Express, React, Node.js) stack. The application allows users to create, delete, and view tasks via an intuitive user interface.

#### Backend Development
1. **Node.js and Express Setup**:
   - Created a RESTful API for handling To-Do tasks.
   - Configured routes for CRUD operations on tasks.

2. **Database Integration**:
   - Used MongoDB to store tasks.
   - Implemented Mongoose for schema creation and data modeling.

3. **Challenges and Solutions**:
   - **Connection Issues**: Resolved by ensuring the .env file was correctly formatted and restarting the server.
   - **API Testing**: Successfully tested endpoints using Postman.

#### Frontend Development
1. **React App Setup**:
   - Used Yarn to scaffold the React application with `yarn create react-app client`.
   - Installed necessary dependencies, including Axios for API calls.

2. **Component Creation**:
   - Created reusable components: `Input`, `ListTodo`, and `Todo`.
   - Implemented state management and lifecycle methods for data fetching.

3. **Proxy Configuration**:
   - Added a proxy in the `package.json` to simplify API calls to the backend.

5. **Challenges and Solutions**:
   - **Cross-Origin Requests**: Handled using the proxy configuration to avoid CORS issues.
   - **Component Communication**: Managed state effectively by passing functions and state down through props.

#### Summary of Challenges Faced
- **Connecting to MongoDB**: Fixed connection issues by checking the .env configuration.
- **Backend API Testing**: Used Postman effectively to ensure all endpoints were functional.
- **Frontend Setup Issues**: Used Yarn instead of npx for setting up the React app, which improved dependency management.

#### Conclusion
This project enhanced my understanding of full-stack development, particularly in integrating frontend and backend technologies. It provided hands-on experience in managing state, handling API requests, and addressing common challenges in web application development.

