This application integrates with a Microsoft SQL Server database, which is set up in a Docker container on MacOS. Below are the instructions for setting up the database, API endpoints, and other key aspects of the project.

**Prerequisites**
- **Docker**: Ensure Docker is installed and running on your machine.
- **MacOS**: This setup assumes MacOS as the operating system.
- **4 GB RAM**: It is recommended to allocate at least 4 GB of RAM to Docker for the SQL Server container to run smoothly.

**Database Setup with Docker**

1. **Increase RAM to 4 GB for Docker**:
   - Open Docker settings and set the memory allocation to 4 GB.

2. **Pull the SQL Server Image and Create a Container**:
   Run the following command in your terminal to set up Microsoft SQL Server on Docker:
   
   ```bash
   docker run -e "ACCEPT_EULA=1" \
              -e "MSSQL_USER=YOURUSERNAME" \
              -e "MSSQL_SA_PASSWORD=YOURPASSWORD" \
              -e "MSSQL_PID=Developer" \
              -p 1433:1433 \
              -d --name=sql_connect \
              mcr.microsoft.com/azure-sql-edge
   ```

3. **Manage the Docker Container**:
   - To stop the running container, use the following command:
     ```bash
     docker stop sql_connect
     ```
   - To start the container again, use:
     ```bash
     docker start sql_connect
     ```
   - To check if the container is running:
     ```bash
     docker container ls -a
     ```

## API Endpoints
### Auth
- **POST** `/Auth/Register` - Register a new user
- **PUT** `/Auth/ResetPassword` - Reset user password
- **POST** `/Auth/Login` - User login
- **GET** `/Auth/RefreshToken` - Refresh JWT token

### Post
- **GET** `/Post/Posts/{postId}/{userId}/{searchParam}` - Get post details with search parameters
- **GET** `/Post/MyPosts` - Retrieve the posts created by the user
- **PUT** `/Post/UpsertPost` - Create or update a post
- **DELETE** `/Post/Post/{postId}` - Delete a post by its ID

### UserComplete
- **GET** `/UserComplete/TestConnection` - Test the connection to the user management service
- **GET** `/UserComplete/GetUsers/{userId}/{isActive}` - Get users by ID and active status
- **PUT** `/UserComplete/UpsertUser` - Create or update user details
- **DELETE** `/UserComplete/DeleteUser/{userId}` - Delete a user by ID

## Running the App

1. **Start the SQL Server Container**:
   Make sure your SQL Server Docker container is running by starting it if necessary:
   
   ```bash
   docker start sql_connect
   ```

2. **Check the Container**:
   Confirm that the container is active:
   
   ```bash
   docker container ls -a
   ```

3. **API Usage**:
   Use the provided API routes to interact with the app, ensuring that the SQL Server is correctly connected.
