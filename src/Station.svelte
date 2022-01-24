<script lang="ts">
    export let station: { favicon: string; url: string; name: string };
    export let activeStation: HTMLAudioElement;

    function playStation(station: string) {
        if (activeStation) {
            activeStation.src = "";
        }
        activeStation = new Audio(station);
        activeStation.play();
    }

    function stationName(name: string): string {
        if (name.length > 12) {
            return `${name.slice(0, 12)}..`;
        } else {
            return name;
        }
    }
</script>

<div>
    <button
        style="background-image: url({station.favicon})"
        on:click={() => playStation(station.url)}
    >
        {#if !station.favicon}
            {station.name}
        {/if}
        {#if activeStation && activeStation.src === station.url}
            <!-- Station is playing -->
            <img
                src="https://raw.githubusercontent.com/sigmaSd/Rodio/master/assets/play.png"
                alt="playing"
            />
        {/if}
    </button>
    <p>{stationName(station.name)}</p>
</div>

<style>
    div {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    :root {
        --size: 150px;
    }

    button {
        width: var(--size);
        height: var(--size);
        background-size: var(--size);
    }
    img {
        width: calc(var(--size) / 2);
    }
</style>
