<script>
	import { onMount } from "svelte";
	let darkMode = $state();
	$effect(() => {
		darkMode = localStorage.theme === "dark" ? true : false;
	});

	function toggle() {
		darkMode = !darkMode;
		// Tailwind dark mode
		// On page load or when changing themes, best to add inline in `head` to avoid FOUC
		if (!darkMode) {
			// Whenever the user explicitly chooses light mode
			localStorage.theme = "light";
		}
		if (darkMode) {
			// Whenever the user explicitly chooses dark mode
			localStorage.theme = "dark";
		}

		if (localStorage.theme === "dark" || !("theme" in localStorage)) {
			document.documentElement.classList.add("dark");
		} else {
			document.documentElement.classList.remove("dark");
		}

		// Whenever the user explicitly chooses to respect the OS preference
		// localStorage.removeItem("theme");
	}
</script>

<button onclick={() => toggle()} class="text-2xl i-carbon-sun dark:text-white dark:i-carbon-moon inline-flex align-text-top">{darkMode ? "Switch to light mode" : "Switch to dark mode"}</button>

<style>
</style>
