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
</script>

