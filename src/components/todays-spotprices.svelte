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
            <li class="bg-white dark:bg-gray-800 border border-gray-200 dark:border-gray-700 rounded-lg shadow hover:shadow-lg transition-shadow duration-200 p-4 flex flex-col items-center">
                <div class="flex items-center gap-2 mb-1">
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 text-blue-500 dark:text-blue-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                    <h2 class="font-semibold text-base">
                        {formatHour(price.time_start)} – {formatHour(price.time_end)}
                    </h2>
                </div>
                <p class="text-2xl font-bold text-blue-600 dark:text-blue-400 mb-1">
                    {formatPrice(price)}
                </p>
            </li>
        {/each}
    </ul>
{/if}

