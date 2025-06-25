<script>
    import { onMount } from 'svelte';
    
    let spotPrices = [];
    let error = null;
    let selectedCurrency = 'SEK';
    
    onMount(async () => {
        try {
            const response = await fetch('https://currentprice-backend.onrender.com/prices');
            const data = await response.json();
            console.log('API response:', data);
            spotPrices = data;
        } catch (err) {
            error = 'Failed to load spot prices';
            console.error(err);
        }
    });

  //Function to format the date in 'YYYY-MM-DD' format
  const formatHour = (isoString) => {
    const date = new Date(isoString);
    return date.toLocaleTimeString('sv-SE', { hour: '2-digit', minute: '2-digit' });
  };

  function formatPrice(price) {
	if (selectedCurrency === 'SEK') {
		return `${(price.SEK_per_kWh * 100).toFixed(2)} öre/kWh`;
	} else {
		return `${(price.EUR_per_kWh * 100).toFixed(2)} eurocent/kWh`;
	}
}; 

</script>

<div class="mb-4 flex gap-4 items-center justify-center">
	<label class="flex items-center gap-1">
		<input type="radio" name="currency" bind:group={selectedCurrency} value="SEK" />
		<span>SEK (öre)</span>
	</label>
	<label class="flex items-center gap-1">
		<input type="radio" name="currency" bind:group={selectedCurrency} value="EUR" />
		<span>EUR (eurocent)</span>
	</label>
</div>

{#if error}
	<p class="text-red-500">{error}</p>
{:else}
	<ul class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
		{#each spotPrices as price}
			<li class="bg-white p-4 rounded shadow">
				<h2 class="font-semibold text-lg">
					{formatHour(price.time_start)} – {formatHour(price.time_end)}
				</h2>
				<p class="text-gray-800 text-xl">
					{formatPrice(price)}
				</p>
			</li>
		{/each}
	</ul>
{/if}

