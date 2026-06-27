<script>
	import '../app.css';
	import Navbar from '$lib/components/Navbar.svelte';
	import Footer from '$lib/components/Footer.svelte';
	import { ArrowUp } from 'lucide-svelte';

	let { children } = $props();
	let showTop = $state(false);
</script>

<svelte:window onscroll={() => (showTop = scrollY > 600)} />

<Navbar />
<main class="page-fade">
	{@render children()}
</main>
<Footer />

<!-- ponytail: smooth scroll comes from `scroll-behavior: smooth` in app.css, so scrollTo is enough -->
<button
	aria-label="Scroll to top"
	onclick={() => scrollTo({ top: 0 })}
	class="fixed bottom-6 right-6 z-50 grid place-items-center w-11 h-11 rounded-full bg-champagne text-obsidian shadow-2xl transition-all duration-300 hover:-translate-y-0.5 {showTop
		? 'opacity-100'
		: 'opacity-0 pointer-events-none'}"
>
	<ArrowUp size={18} />
</button>
