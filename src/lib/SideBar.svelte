<script lang="ts">
  let searchQuery = "";
  let error = "";
  export let sessionizeKey = "";
  export let selectedSession = undefined;

  const resetKey = () => {
    localStorage.removeItem("sessionizeKey");
    sessionizeKey = "";
  };

  const search = async () => {
    error = "";
    selectedSession = undefined;
    const fetchResult = await fetch(
      `https://sessionize.com/api/v2/${sessionizeKey}/view/Sessions`
    );

    const results = await fetchResult.json();
    for (const session of results[0].sessions) {
      if (session.title.toLowerCase().includes(searchQuery.toLowerCase())) {
        selectedSession = session;
        break;
      }
    }

    if (!selectedSession) {
      error = "No match";
    }
  };
</script>

<div class="gridRows sidebar">
  <div class="gridRows">
    <div>Search for a session to provide feedback on</div>
    <label for="searchBox">Title:</label>
    <input id="searchBox" type="text" bind:value={searchQuery} />
    <button type="button" class="primary" on:click={search}>Search</button>
    {#if error}
      <div class="error">{error}</div>
    {/if}
  </div>
  <button type="button" class="primary alignBottom" on:click={resetKey}>
    Reset Sessionize Key
  </button>
</div>

<style>
  .sidebar {
    height: 100%;
    grid-template-rows: min-content 1fr;
  }
</style>
