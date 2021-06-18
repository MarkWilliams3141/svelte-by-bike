<script>
    import * as cycle_parking from '../data/cycle_parking.json';
    import Map from "../components/Map.svelte";
    import InfoBoard from "../components/InfoBoard.svelte";
    import {onMount} from "svelte";
    $: center = { lat: 51.509041, lng: -0.0683852 };
    $: features = [];
    $: activeFeature = {}
    $: hasSelectedFeature = false;
    let showMap = false;

    onMount(async () => {
        // if geolocation available
        if (window.navigator.geolocation) {
            window.navigator.geolocation
                .getCurrentPosition((pos) => {
                    center = { lat:pos.coords.latitude, lng: pos.coords.longitude };
                    features = cycle_parking.features;
                    showMap = true;
                }, console.log);
        }
    });

    function handleSelectedFeature(event) {
        activeFeature = event.detail;
        hasSelectedFeature = true;
    }


</script>
<div class="page-wrapper">
    <section class="column map-column">
        {#if showMap}
            <Map center={center} features={features} on:selectedFeature={handleSelectedFeature}/>
        {/if}
    </section>
    <section class="column info-column">
        {#if hasSelectedFeature}
            <InfoBoard feature={activeFeature} />
        {:else}
            <h1>Select a bicycle rack</h1>
        {/if}
    </section>


</div>

<style>
    .page-wrapper {
        display: flex;
        height: 100vh;
        align-self: start;
    }

    .column {
        display: flex;
        flex-direction: column;
        flex-basis: 100%;
        flex: 1;
    }

    .info-column {
        background-color: #F7C59F;
        padding:15px;
        max-width: 50%;
    }

    .map-column {

    }
</style>

