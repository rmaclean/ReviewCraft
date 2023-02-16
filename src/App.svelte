<script lang="ts">
  import NeedKey from "./lib/NeedKey.svelte";
  import SideBar from "./lib/SideBar.svelte";
  import Session from "./lib/Session.svelte";

  let sessionizeKey = localStorage.getItem("sessionizeKey");
  let selectedSession = undefined;
</script>

<main>
  <div class="sideBar">
    {#if !sessionizeKey}
      <NeedKey bind:sessionizeKey={sessionizeKey}  />
    {:else}
      <SideBar bind:sessionizeKey={sessionizeKey} bind:selectedSession={selectedSession} />
    {/if}
  </div>
  <div class="titleBar"><h1>ReviewCraft</h1></div>
  <div class="content">
    <Session selectedSession={selectedSession} />
  </div>
</main>

<style>
  main {
    display: grid;
    font-family: "Cairo Play", sans-serif;
    color: whitesmoke;

    grid-template-columns: 200px 1fr;
    grid-template-rows: 50px 1fr;
    grid-template-areas:
      "sideBar titleBar"
      "sideBar .";

    height: 100vh;
    width: 100vw;
  }

  .sideBar {
    grid-area: sideBar;
    background: rgb(4, 4, 57);
    border-right-color: white;
    border-right-width: 2px;
    border-right-style: solid;
    padding: 10px;
  }

  .titleBar {
    grid-area: titleBar;
    padding-left: 20px;
    padding-top: 10px;
  }

  .content {
    padding: 20px;
  }
</style>
