<script>

  async function getUsers() {
    let userData = await fetch("https://api.github.com/users");
    const users = await userData.json();
    return users;
  }
</script>

<section>
  {#await getUsers()}
    <!-- promise is pending -->
    <h2>Loading ...</h2>
  {:then users}
    {#each users as user}
      <article class="user">
        <img src={user.avatar_url} alt={user.login} />
        <div class="user-info">
          <h3>User: {user.login}</h3>
          <a href={user.html_url} class="btn-primary" target="_blank"
            >github url</a
          >
        </div>
      </article>
    {/each}
  {:catch error}
    <h2>Something went wrong {error.message}</h2>
  {/await}
</section>
