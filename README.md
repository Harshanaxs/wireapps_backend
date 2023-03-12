# wireapps_backend

#Q1
| HTTP Method | URL                        | Description                                                             |
|-------------|----------------------------|-------------------------------------------------------------------------|
| POST        | /login                     | Authenticate a user by username and password                            |
| GET         | /medications               | Retrieve a list of all medications                                       |
| GET         | /medications/{id}          | Retrieve a specific medication by ID                                     |
| POST        | /medications               | Add a new medication (Only the Owner can perform this action)            |
| PUT         | /medications/{id}          | Update an existing medication (Managers and Cashiers can perform this action)|
| PATCH       | /medications/{id}          | Soft delete a medication record (Managers and Cashiers can perform this action)|
| DELETE      | /medications/{id}          | Permanently delete a medication record (Only the Owner can perform this action)|
| GET         | /customers                 | Retrieve a list of all customers                                         |
| GET         | /customers/{id}            | Retrieve a specific customer by ID                                       |
| POST        | /customers                 | Add a new customer (Only the Owner can perform this action)              |
| PUT         | /customers/{id}            | Update an existing customer (Managers and Cashiers can perform this action)|
| PATCH       | /customers/{id}            | Soft delete a customer record (Managers and Cashiers can perform this action)|
| DELETE      | /customers/{id}            | Permanently delete a customer record (Only the Owner can perform this action)|

#Q2 PDF Uploaded to Repo.

#Q3

| Name of the package                       |What would you accomplish using that?                                    |                                                   
|------------------------------------------|-------------------------------------------------------------------------|
| Express JS                               | manage servers and routes                                                |
| React                             | Build UI                                                 |
| Nest JS                                  | Good architecture and fast development                                                |
| Type ORM                               | Handle Database Queries , Migrations , Build a Schema using Typescript instead of SQL     |
| Supabase                               | Handle Authentication , Database (Postgres)                                                |

#Q4

| Name of the program                       |What would you accomplish using that?                                    |                                                  |------------------------------------------|-------------------------------------------------------------------------|
| VS CODE                             | IDE                                               |
| Docker                               | Hassle free Deployment                                                |
| Caprover                               | Manage Server and One click dockerized service deployment            |

#Q5 

#1 Make a list of user roles that determine what permissions a user has. Common roles include Owner, Manager, and Cashier.

#2 Define the permissions for each role: For each role, define what permissions users should have. It could include permissions like create, read, update, and delete for different resources like users, medications, and customers.

#3 Make a permissions table in the database to store each role's permissions. There should be columns for the role name, the resource name, and the permissions for that role and resource.

#4 Assign roles to users: Make it easy to assign roles. It could be done with a user interface or code. 

#5 When a user tries to perform an action, check their role and the permissions associated with that role. If the user has the required permissions, allow the action. If not, show an error message.

#6Implement Access Control: Implement access control on the server-side to ensure that users can't bypass the permission checks by manipulating the client-side code. Using middleware and JWT validation in a Node.js app to check user permissions before allowing a request to be processed.


```
const express = require('express');
const app = express();

// middleware to check user permissions
function checkPermissions(req, res, next) {
  const userRole = req.user.role;
  const resource = req.params.resource;
  const requiredPermissions = getPermissions(userRole, resource);
  const userPermissions = req.user.permissions[resource];

  // check if the user has all required permissions for the resource
  const hasPermissions = requiredPermissions.every(permission => userPermissions.includes(permission));

  if (hasPermissions) {
    next(); // user has permissions, allow the request to continue
  } else {
    res.status(403).send('Access denied'); // user does not have permissions, show error message
  }
}

// example route that requires permissions to access
app.get('/posts/:id', checkPermissions, (req, res) => {
  // code to fetch and return post with the given ID
});

// example function to get permissions for a role and resource this can be replace with database and dynamic 
function getPermissions(role, resource) {
  const permissions = {
    owner: {
      medication: ['insert', 'read', 'update','soft-delete', 'delete'],
      medication: ['insert', 'read', 'update','soft-delete', 'delete'],
    },
    manager: {
        medication: [ 'read', 'update','soft-delete'],
        customer: [, 'read', 'update','soft-delete']
    },
    cashier: {
        medication: [ 'read', 'update'],
        customer: [ 'read', 'update']
  };

  return permissions[role][resource];
}
```

