# Web UI

This is React app is for performing GET/POST/DELETE operations. The app communicates with a backend API built with Spring Boot and MongoDB.

## Features
- Get all items
- Get item by ID
- Get items by name
- Add new item
- Delete item by ID

## Technology used
- React
- Material UI
- Axios
- SpringBoot
- MongoDB

## Backend API
The backend API for this app is built with Spring Boot and MongoDB. The source code for the backend API can be found in a separate repository at https://github.com/Anant1711/Task-1-Java-Rest-API

## How to Use
- Clone this repository to your local machine.
- Navigate to the project directory and install the dependencies by running `npm install`.
- Start the app by running `npm start`.
- Open the app in your browser at `http://localhost:3000`
- Make sure you clone `git clone https://github.com/Anant1711/Task-1-Java-Rest-API` this repository and run it with mongoDB. 
- Use the app to perform operations on the database.

## Usage

<h3>1. All details</h3>

<img src="/Screenshots/alldetail.jpg" alt="All details"/>

```js
//Function for getting all queries from DB
    useEffect(() => {
        fetch("http://localhost:8080/")
            .then(res => res.json())
            .then((result) => {
                setServer(result);
            }
            )
    }, [])
```

This code is a React component that displays a table of server details. The `useEffect` hook is used to make a `GET` request to the backend server (running on http://localhost:8080/) to retrieve an array of server details, which is stored in the server state variable using the `setServer` function.

<h3>2. Add Details to DB</h3>

I've created this Add details page where all 4 fields are required otherwise it throuh error and not take empty request from user. 

<img src="/Screenshots/add1.jpg" alt="All details"/>

After enter all fields and click on send button, it will trigger `handled` function and save it to the db and refresh the page automatically.

<img src="/Screenshots/addS.jpg" alt="All details"/>

As you can see server detail save successfully in db with ID number `005`

<img src="/Screenshots/add3.jpg" alt="All details"/>

```js
//For POST request, for sending data to Mongodb Database
    fetch("http://localhost:8080", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(server)
    }).then(() => {
      alert("Added Successfully")
    })
    window.location.reload(false);
```

This code sends a `POST` request to the server with the data in the server variable. It specifies the request method as **"POST"** and the content type of the request body as **"application/json"** in the request headers. The `JSON.stringify()` method is used to convert the data in the server variable to a JSON string format.

Once the server has successfully processed the request, an alert is displayed to indicate that a `Added Successfully`. Finally, `window.location.reload(false)` is called to reload the current page and update the list of Server with the new Server added.

<h3>3. Delete by ID</h3>

On this page, we can delete server details by their id number. If ID number exist in db it delete it and throw a alert box which stated that `Item deleted successfully` and if ID number is not exist it db it will give `404 NOT FOUND` status.

Let's try to delete server detail with ID number `005` that we added earlier.

<img src="/Screenshots/delete1.jpg" alt="All details"/>

It shows `Item deleted successfully` and we can also check in all items page that ID number `005` is deleted.

<img src="/Screenshots/delete2.jpg" alt="All details"/>

```js
//Delete method for delete item from ID
  async function handleDeleteById() {
    const response = await fetch(`http://localhost:8080/${id}`, {
      method: 'DELETE',
    });

    if (!response.ok) {
      if (response.status === 404) {
        alert("404 NOT FOUND");
      } else {
        alert('An error occurred');
      }
      return;
    }
    alert('Item deleted successfully');
    window.location.reload(false);
  }
```

This is async function, it first sends a DELETE request to the server at the specified endpoint `http://localhost:8080/${id}`, which is the ID of the item to be deleted.

If the response is not ok (i.e., the request was not successful), it checks the status code of the response. If the status code is `404`, it means that the item with the specified ID was not found, so it shows an alert message.

If the response is successful, it shows an alert message to indicate that the item was deleted successfully, and reloads the page to update the displayed data.

<h3>4. Get By ID</h3>

In this page we can retrieve server detail by their ID number.If ID number is not exist in db it will show `404 NOT FOUND`.

<img src="/Screenshots/gid.jpg" alt="All details"/>

```js
async function handleGetById() {
    const response = await fetch(`http://localhost:8080/${id}`);

    if (!response.ok) {
      if (response.status === 404) {
        alert("404 NOT FOUND");
        window.location.reload(false);
      } else {
        alert('An error occurred');
      }
      return;
    }

    const data = await response.json();
    setData(data);
  }
```
This is an async function called `handleGetById()`, which sends a `GET` request to the server to retrieve data for a specific ID. 

If the response is `OK`, the function parses the response body as JSON data using the `response.json()` method, and sets the resulting data to the data state variable using the `setData()` function.

<h3>4. Get By Name</h3>

In this page we can retrieve **all** server detail by their Name.If Name is not exist in db it will show `404 NOT FOUND`.

<img src="/Screenshots/gnm.jpg" alt="All details"/>

```js
async function handleGetByName() {
    const response = await fetch(`http://localhost:8080/name/${name}`);

    if (!response.ok) {
      if (response.status === 404) {
        alert("404 NOT FOUND");
        window.location.reload(false);
      } else {
        alert('An error occurred');
      }
      return;
    }

    const data = await response.json();
    setData(data);
  }
```

This is an async function that retrieves data from the server by making a `GET` request to the endpoint with the specified name parameter. If name does not exist it shows alert `404 not found`. If the name exists, the data is extracted from the response body using `response.json()` and stored in the data variable using the `setData` function.
