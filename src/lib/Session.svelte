<script lang="ts">
    export let selectedSession = undefined;
</script>

{#if selectedSession}
    <h2>{selectedSession.title}</h2>
    <p>{selectedSession.description}</p>
{/if}