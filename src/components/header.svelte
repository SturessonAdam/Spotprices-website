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

<nav class="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex justify-between h-16 items-center">   
      <div class="flex items-center gap-4">
        <slot />
      </div>
      <div class="flex items-center gap-4">
        <a href="/" class="text-gray-700 dark:text-gray-200 hover:underline">Hem</a>
        <button
          class="px-4 py-2 rounded bg-gray-200 dark:bg-gray-700 text-gray-900 dark:text-gray-100 transition"
          on:click={toggleDark}
          aria-label="Toggle dark mode"
        >
          {dark ? '🌙 Dark mode' : '☀️ Light mode'}
        </button>
      </div>
    </div>
  </div>
</nav>