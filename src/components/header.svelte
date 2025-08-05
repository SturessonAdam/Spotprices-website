<script>
    let dark = false;

    const toggleDark = () => {
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

<nav class="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 mb-4">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex justify-between h-16 items-center">   
      <div class="flex items-center gap-4">
        <slot />
      </div>
      <div class="flex items-center gap-4">
        <a href="/" class="text-gray-700 dark:text-gray-200 hover:underline">Hem</a>
        <button
          class="relative w-12 h-6 bg-gray-300 dark:bg-gray-600 rounded-full transition-colors duration-300 focus:outline-none"
          on:click={toggleDark}
          aria-label="Toggle dark mode"
        >
          <span
            class="absolute left-1 top-1 w-4 h-4 rounded-full shadow transition-transform duration-300"
            style="transform: translateX({dark ? '24px' : '0'})"
          ></span>
          <span class="absolute left-1 top-1 w-4 h-4 flex items-center justify-center pointer-events-none transition-opacity duration-300"
                style="opacity: {dark ? 1 : 0}; transform: translateX(24px)">
            🌙
          </span>
          <span class="absolute left-1 top-1 w-4 h-4 flex items-center justify-center pointer-events-none transition-opacity duration-300"
                style="opacity: {dark ? 0 : 1};">
            ☀️
          </span>
        </button>
      </div>
    </div>
  </div>
</nav>