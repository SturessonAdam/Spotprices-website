<script>

    let dark = false;

    function toggleDark() {
        dark = !dark;
        if (dark) {
            document.documentElement.classList.add('dark');
            localStorage.setItem('theme', 'dark');
        } else {   
            document.documentElement.classList.remove('dark');
            localStorage.setItem('theme', 'light');
        }
    }

</script>

<header class="flex justify-between items-center mb-6">
    <h1 class="text-2xl font-bold">Spotprices</h1>
    <button
        class="px-4 py-2 rounded bg-gray-200 dark:bg-gray-700 text-gray-900 dark:text-gray-100"
        on:click={toggleDark}
        aria-label="Toggle dark mode"
    >
        {dark ? '🌙 Dark mode' : '☀️ Light mode'}
    </button>
</header>