<script lang="ts">
    import Stations from "./Stations.svelte";

    export let activeStation: HTMLAudioElement;

    let method: string;
    let input: string;
    let stations: any;

    async function search() {
        let urlMethod: string;
        switch (method) {
            case "Country":
                urlMethod = "bycountry";
                break;
            case "Language":
                urlMethod = "bylanguage";
                break;
            case "Name":
                urlMethod = "byname";
                break;
        }
        stations = await (
            await fetch(
                `https://de1.api.radio-browser.info/json/stations/${urlMethod}/${input}`
            )
        ).json();
    }
</script>

<select bind:value={method}>
    <option>Country</option>
    <option>Language</option>
    <option>Name</option>
</select>
<input bind:value={input} />
<button on:click={search}>Search</button>
{#if stations}
    <Stations title="Search" {stations} bind:activeStation />
{/if}
