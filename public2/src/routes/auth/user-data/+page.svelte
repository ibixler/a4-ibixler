<script>
  import { goto } from "$app/navigation";

  let data = false;
  function generateTable(data) {
    let table = "";
    table = "<table>";
    if (data) {
      table +=
        "<tr><th>name</th><th>Age</th><th>Coat</th><th>Solidity</th></tr>";
      data.forEach((item) => {
        table += `<tr><td>${item.name}</td><td>${item.age}</td><td>${item.coat}</td><td>${item.solidity}</td></tr>`;
      });
    }

    table += "</table>";
    return table;
  }
  /* const parseData = {
  toFloat: function(data){
    let ret = {

    };
    for (const [key, value] of Object.entries(data)){
      ret[key] = isNaN(+value) ? value : +value;
    }
    return ret; 
  }
}
*/
  async function checkAuth(event, endpoint) {
    if (event) event.preventDefault();
    const rsp = await fetch(endpoint, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${document.cookie.substring(6)}`,
      },
    });
    if (rsp.status === 403 || !(document.cookie)) {
      goto("/login");
    }
    await rsp.json();
  }

  function makeTable(data) {
    const tableContainer = document.getElementById("catData");
    tableContainer.innerHTML = "";
    tableContainer.innerHTML = generateTable(data);
  }

  window.onload = function () {
    checkAuth(event,"localhost:3001/auth/user-data/fetch-cats")
    /* getData(null) */
    /* const loginRedirectButton = document.querySelector("#login");
  loginRedirectButton.onclick = () => redirect(event, "/login");
  const registerButton = document.querySelector('#submit');
  registerButton.onclick = () => submit(event, "/register/new-user") */
    //checkAuth(null, "/auth/user-data").then(response => console.log("response: ",response))
    /* if(document.cookie){
    console.log("cookie exists")
  }else{
    redirect(null,"/login")
  } */
    /*  submit(event, "localhost:3001/auth/user-data/fetch-cats", false)
      .then((result) => makeTable(result))
      .catch((error) => errorHandler(error));
    if (localStorage.getItem("hasCodeRunBefore") === null) {
      localStorage.setItem("hasCodeRunBefore", true);
    }
    //data.concat(submit(event, "/auth/user-data/fetch-cats", false));
    const submitButton = document.querySelector("#submit");
    submitButton.onclick = () =>
      submit(event, "/auth/user-data/add-cat", "#catInfo")
        .then(() => submit(event, "/auth/user-data/fetch-cats", false))
        .then((result) => makeTable(result))
        .catch((error) => errorHandler(error));
    const logoutButton = document.querySelector("#logout");
    logoutButton.onclick = () => {
      document.cookie = "token= ; expires = Thu, 01 Jan 1970 00:00:00 GMT";
      redirect(null, "/login");
    };
    const deleteButton = document.querySelector("#delete");
    deleteButton.onclick = () =>
      submit(event, "/auth/user-data/delete-cat", "#catInfo")
        .then(() => submit(event, "/auth/user-data/fetch-cats", false))
        .then((result) => makeTable(result))
        .catch((error) => errorHandler(error)); */
    /* const deleteButton = document.querySelector("#delete");
  deleteButton.onclick = () => submit(event, "/delete"); */
  };
</script>

<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta
    name="description"
    content="Store cats with the amazing and user friendly Cat-abase. Do you have too many cats to remember their names at Cat-abase we have you back!!!!!!"
  />
  <title>Cat-abase User Details </title>
  <meta charset="utf-8" />
  <!-- <script type="module" src="js/main.js"></script>
  <script type="module" src="js/user.js"></script> -->
</head>
<body>
  <div class="flexbox">
    <h1>Welcome to Cat-abase</h1>
    <h2>Upload Information About a Cat</h2>
    <form id="catInfo">
      <input type="text" name="name" placeholder="Cat Name" /><br />
      <input type="number" name="age" placeholder="Age" /><br />
      <input type="text" name="coat" placeholder="Coat Information" /><br />
      <input type="number" name="solidity" placeholder="Solidity Factor" /><br
      />
      <div>
        <!-- <input type="file" id="file" accept="image/*"> -->
      </div>
    </form>
    <div>
      <button id="submit">Submit A Cat</button>
      <button id="delete">Delete A Cat</button>
      <button id="logout">Logout</button>
      <!-- <button id="upload">Upload</button> -->
    </div>
    <div id="image"></div>
    <h3>Your Cats</h3>
    <h4>About the functionality</h4>
    <p>
      You must fill out every field to do any interaction.<br /> You can edit a
      cat by entering their name and age <br /> and substitue new coat info or
      rotundity.<br />to Delete a cat is much the same<br /> enter all associated
      fields and press delete
    </p>
    <h4>About the fields!!</h4>
    <p>
      Here you can see data about each cat! <br /> Name is the name of the cat
      <br />
      Age is the age of the cat <br />Coat is a description of the cats coat(a
      few words) <br /> Solidity is a gentile way of inqiring about rotundity
    </p>
    <div id="catData"></div>
  </div>
</body>
