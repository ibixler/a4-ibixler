
<script>
  import { goto } from '$app/navigation';

  let username = "";
  let password = "";

  async function submitForm() {
    try {
      const response = await fetch("http://localhost:3001/login/auth", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ username, password }),
      });

      if (response.ok) {
        const data = await response.text();
        console.log(data);
        console.log("setting cookie");
        document.cookie = `token=${data}`;
      } else {
        throw new Error("Login failed");
      }
    } catch (error) {
      // Handle fetch or other errors
      console.error(error);
    }
  }
</script>

<main>
  <h1>Cat-abase Login</h1>
  <form on:submit|preventDefault={submitForm}>
    <input type="text" bind:value={username} placeholder="Username" /><br />
    <input type="password" bind:value={password} placeholder="Password" /><br />
    <button type="submit">Login</button>
  </form>
</main>

<style>
</style>
