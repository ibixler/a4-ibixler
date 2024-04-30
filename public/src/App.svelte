<script>
  import { Route, Router, Link } from "svelte-routing";
  import Login from "./routes/Login.svelte";
  import UserData from "./User-Data.svelte";
  let basepath = "/";
  let path = location.pathname;
</script>

<Router {basepath}>
  <div on:click={() => (path = location.pathname)}>
    <Link to="/">Go to home</Link>
    <Link to="/login">login</Link>

  </div>
  <main>
    <Route path="/login" component={Login}/>
    <Route path="/auth/user-data" component={UserData}></Route>
  </main>
</Router>

<style> 
  
</style>
