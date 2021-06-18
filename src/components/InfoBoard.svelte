<script>
    export let feature;

    function prettyType(feature){
        console.log(feature)
        if(feature.properties.PRK_SHEFF === 'TRUE') return 'Sheffield cycle stand';
        if(feature.properties.PRK_MSTAND === 'TRUE') return 'M cycle stand';
        if(feature.properties.PRK_PSTAND === 'TRUE') return 'P cycle stand';
        if(feature.properties.PRK_HOOP === 'TRUE') return 'Cyclehoop';
        if(feature.properties.PRK_POST === 'TRUE') return 'Post cycle stand';
        if(feature.properties.PRK_BUTERF === 'TRUE') return 'Butterfly cycle stand';
        if(feature.properties.PRK_WHEEL === 'TRUE') return 'Wheel rack';
        if(feature.properties.PRK_HANGAR === 'TRUE') return 'Bike hanger';
        if(feature.properties.PRK_TIER === 'TRUE') return 'Multi tiered cycle parking';
        return 'Other/Unknown';
    }

    //  Some features do not have images
    function hasImage(asset) {
        console.log(asset)
        return !asset.includes('no_asset_photo');
    }
</script>

<!--- Example feature
{
			"type" : "Feature",
			"geometry" : {
				"type" : "Point",
				"coordinates" : [ -0.2427797672, 51.5103212773 ]
			},
			"properties" : {
				"FEATURE_ID" : "RWG014703",
				"SVDATE" : "2017-09-07",
				"PRK_CARR" : "FALSE",
				"PRK_COVER" : "FALSE",
				"PRK_SECURE" : "FALSE",
				"PRK_LOCKER" : "FALSE",
				"PRK_SHEFF" : "FALSE",
				"PRK_MSTAND" : "FALSE",
				"PRK_PSTAND" : "FALSE",
				"PRK_HOOP" : "FALSE",
				"PRK_POST" : "FALSE",
				"PRK_BUTERF" : "FALSE",
				"PRK_WHEEL" : "FALSE",
				"PRK_HANGAR" : "TRUE",
				"PRK_TIER" : "FALSE",
				"PRK_OTHER" : "FALSE",
				"PRK_PROVIS" : 1,
				"PRK_CPT" : 6,
				"BOROUGH" : "Hammersmith & Fulham",
				"PHOTO1_URL" : "https://cycleassetimages.data.tfl.gov.uk/RWG014703_1.jpg",
				"PHOTO2_URL" : "https://cycleassetimages.data.tfl.gov.uk/RWG014703_2.jpg"
			}
		},
-->
<div class="info-board">
    <h1>{(prettyType(feature) + " " + feature.properties.FEATURE_ID)}</h1>
    <div class="image-container">
        {#if hasImage(feature.properties.PHOTO1_URL)}
            <img src={feature.properties.PHOTO1_URL}>
        {/if}
        {#if hasImage(feature.properties.PHOTO2_URL)}
            <img src={feature.properties.PHOTO2_URL}>
        {/if}
    </div>
    <table>
        <tr>
            <td>
                <p><strong>Capacity</strong></p>
                <small>Number of bikes that can be parked without difficulty</small>
            </td>
            <td>{feature.properties.PRK_CPT}</td>
        </tr>
        <tr>
            <td>
                <p><strong>Covered</strong></p>
                <small>Covered or sheltered (including partial shelter)</small>
            </td>
            <td>{feature.properties.PRK_COVER === 'FALSE'? 'No' : 'Yes' }</td>
        </tr>
        <tr>
            <td>
                <p><strong>Provision</strong></p>
                <small>Number of stands or discrete units</small></td>
            <td>{feature.properties.PRK_PROVIS}</td>
        </tr>
        <tr>
            <td>
                <p><strong>Carriageway</strong></p>
                <small>Next to a road</small></td>
            <td>{feature.properties.PRK_CARR === 'FALSE'? 'No' : 'Yes' }</td>
        </tr>
        <tr>
            <td>
                <p><strong>Secure</strong></p>
                <small>Locked compound with shared or combination lock provided by operator</small></td>
            <td>{feature.properties.PRK_SECURE === 'FALSE'? 'No' : 'Yes' }</td>
        </tr>
        <tr>
            <td>
                <p><strong>Locker</strong></p>
                <small>Locker using own or integral lock</small></td>
            <td>{feature.properties.PRK_LOCKER === 'FALSE'? 'No' : 'Yes' }</td>
        </tr>
    </table>
</div>

<style>
    .info-board {

    }

    .image-container {
        max-width: 50%;
        display: inline-flex;
    }

    .image-container img {
        max-width: 100%;
    }
</style>


