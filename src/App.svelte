<script lang="ts">
    import Stations from "./Stations.svelte";
    import SearchStations from "./SearchStations.svelte";

    async function getStations() {
        const cn = Intl.DateTimeFormat()
            .resolvedOptions()
            .timeZone.split("/")[1];
        const stations = await (
            await fetch(
                `https://de1.api.radio-browser.info/json/stations/bycountry/${cn}`
            )
        ).json();
        return stations;
    }

    // Only one active station per app
    let activeStation: HTMLAudioElement;
</script>

<main>
    <h1>Radio</h1>
    {#await getStations() then stations}
        <Stations title="Local Stations" {stations} bind:activeStation />
    {/await}
    <br />
    <SearchStations bind:activeStation />
</main>

<style>
    main {
        text-align: center;
        padding: 1em;
        margin: 0 auto;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }
</style>
