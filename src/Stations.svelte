<script lang="ts">
    import Station from "./Station.svelte";

    export let title: string;
    export let activeStation: HTMLAudioElement;
    export let stations: any;

    const pageNumItems = 20;
    let pager = 0;
    $: displayStations = stations.slice(pager, pager + pageNumItems);

    function nextPage() {
        pager += pageNumItems;
    }
    function backPage() {
        pager -= pageNumItems;
    }
</script>

<h2>{title}</h2>
<div>
    {#each displayStations as station}
        <Station {station} bind:activeStation />
    {/each}
</div>
{#if pager + pageNumItems < stations.length}
    <button on:click={nextPage}>next</button>
{/if}
{#if pager > 0}
    <button on:click={backPage}>back</button>
{/if}

<style>
    div {
        display: flex;
        flex-wrap: wrap;
    }
</style>
