# Github_explorer
GitHub Explorer is a web application that allows you to explore and retrieve details about GitHub users. By simply entering a GitHub username, you can use this application to fetch various information using the GitHub API.  The application is built using JavaScript,.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Github Explorer</title>
    <link rel="stylesheet" href="github.css">
  <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
</head>
<body>
    <h1>Github Explorer</h1>
  <input type="text" id="usernameInput" placeholder="Enter Github username">
  <button onclick="fetchUserDetails()">Fetch User Details</button>

  <div id="result"></div>

  <script>
    function fetchUserDetails() {
      var username = document.getElementById("usernameInput").value;
      var url = "https://api.github.com/users/" + username;

      axios.get(url)
        .then(function (response) {
          var user = response.data;
          var resultDiv = document.getElementById("result");
          resultDiv.innerHTML = "";
          
          var nameElement = document.createElement("p");
          nameElement.innerHTML = "Name: " + user.name;
          resultDiv.appendChild(nameElement);
          
          var repoCountElement = document.createElement("p");
          repoCountElement.innerHTML = "Number of Repositories: " + user.public_repos;
          resultDiv.appendChild(repoCountElement);
          
          var followersElement = document.createElement("p");
          followersElement.innerHTML = "Number of Followers: " + user.followers;
          resultDiv.appendChild(followersElement);

          var profileLink = document.createElement("a");
          profileLink.href = user.html_url;
          profileLink.target = "_blank";
          profileLink.innerHTML = "Go to Github Profile";
          resultDiv.appendChild(profileLink);
        })
        .catch(function (error) {
          console.log(error);
          var resultDiv = document.getElementById("result");
          resultDiv.innerHTML = "Error occurred while fetching user details.";
        });
    }
  </script>
</body>
</html>



body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 20px;
  }
  
  h1 {
    text-align: center;
  }
  
  input[type="text"] {
    width: 300px;
    padding: 10px;
    margin-right: 10px;
  }
  button {
    padding: 10px 20px;
    background-color: #007bff;
    color: #fff;
    border: none;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  #result {
    margin-top: 20px;
    border: 1px solid #ccc;
    padding: 10px;
    background-color: #f5f5f5;
  }
  
  #result p {
    margin: 0;
    padding: 5px 0;
  }
  #result a {
    display: block;
    margin-top: 10px;
    text-decoration: none;
    color: #007bff;
  }
  
  #result a:hover {
    text-decoration: underline;
  }
