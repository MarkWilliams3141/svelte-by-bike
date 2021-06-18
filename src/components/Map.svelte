<script>
    import { onMount } from "svelte";
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    function selectedFeature(feature) {
        dispatch('selectedFeature', feature);
    }

    let container;
    let map;
    let service;
    let infowindow;
    let zoom = 15;
    export let center;
    export let features;
    let locations = [];

    onMount(async () => {
        const options = {
            zoom,
            center,
            styles: [
                // paste "Styled Maps: Night Mode" styles here
            ],
        };
        // setup the general Map with the provided options
        map = new google.maps.Map(container, options);

        features.forEach((feature) => {
             locations.push({ lat: feature.geometry.coordinates[1], lng: feature.geometry.coordinates[0]})
        })

        const markers = features.map((feature, i) => {
            const newMarker = new google.maps.Marker({
                position: { lat: feature.geometry.coordinates[1], lng: feature.geometry.coordinates[0]},
                label: "🚲",
            });

            //Attach click event to the marker.
            google.maps.event.addListener(newMarker, "click", function (e) {
                selectedFeature(feature)
            });


            return newMarker;
        });
        new MarkerClusterer(map, markers, {
            imagePath:
                "https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m",
        });


    });
</script>

<div class="map" bind:this={container}></div>

<style>
  .map {
    height: 100%;
    width:100%
  }

</style>
