<script lang="ts">
  export let sessionizeKey = "";
  let tempSessionizeKey = "";
  let error = "";

  const setKey = async () => {
    if (!tempSessionizeKey) {
      return;
    }

    try {
      const fetchResult = await fetch(
        `https://sessionize.com/api/v2/${tempSessionizeKey}/view/Sessions`
      );
      if (fetchResult.status != 200) {
        tempSessionizeKey = "";
        error = `Invalid key (${fetchResult.status})`;
        return;
      }
    } catch (ex) {
      tempSessionizeKey = "";
      error = `Invalid key (${ex})`;
      return;
    }

    localStorage.setItem("sessionizeKey", tempSessionizeKey);
    sessionizeKey = tempSessionizeKey;
  };
</script>

<div class="gridRows">
  <label for="sessionizeKey">
    To get started, please provide your Sessionize API key:
  </label>
  {#if error}
    <div class="error">{error}</div>
  {/if}
  <input
    id="sessionizeKey"
    type="password"
    required
    bind:value={tempSessionizeKey}
  />
  <button class="primary" on:click={setKey}>Set</button>
</div>
