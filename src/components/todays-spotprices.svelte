<script>
    import { onMount } from 'svelte';
    
    let spotPrices = [];
    let error = null;
    
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
</script>

{#if error}
  <p class="text-red-600">{error}</p>
{:else if spotPrices.length === 0}
  <p>Loading spotprices...</p>
{:else}
  <ul class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
    {#each spotPrices as price}
      <li class="bg-white p-4 rounded shadow">
        <h2 class="font-semibold text-lg">
          {formatHour(price.time_start)} – {formatHour(price.time_end)}
        </h2>
        <p class="text-gray-800 text-xl">{(price.SEK_per_kWh * 100).toFixed(2)} öre/kWh</p>
        <p class="text-gray-500 text-sm">{(price.EUR_per_kWh * 100).toFixed(2)} eurocent/kWh</p>
      </li>
    {/each}
  </ul>
{/if}

