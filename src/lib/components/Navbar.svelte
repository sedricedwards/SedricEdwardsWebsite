<script>
    import { page } from "$app/stores";
    import { onMount } from "svelte";

    let scrolled = $state(false);
    let menuOpen = $state(false);

    const NAV_LINKS = [
        { label: "Work", href: "/work" },
        { label: "Services", href: "/services" },
        { label: "Contact", href: "/contact" },
    ];

    onMount(() => {
        const handleScroll = () => {
            scrolled = window.scrollY > 80;
        };
        window.addEventListener("scroll", handleScroll, { passive: true });
        handleScroll(); // Check initial state
        return () => window.removeEventListener("scroll", handleScroll);
    });
</script>

<nav
    class="fixed top-6 left-1/2 -translate-x-1/2 z-50 transition-all duration-500 {menuOpen
        ? 'rounded-3xl bg-[#0D0D12]/90 backdrop-blur-2xl border border-[#2A2A35]/80 shadow-2xl px-6 pb-6 pt-3'
        : scrolled
          ? 'rounded-full bg-[#0D0D12]/70 backdrop-blur-xl border border-[#2A2A35]/60 shadow-2xl px-6 py-3'
          : 'rounded-full bg-transparent px-8 py-4'}"
    style="width: {scrolled || menuOpen
        ? 'min(720px, 95vw)'
        : 'min(900px, 95vw)'}"
>
    <div class="flex items-center justify-between">
        <!-- Logo -->
        <a
            href="/"
            class="font-drama text-xl italic tracking-wide text-champagne hover:opacity-80 transition-opacity"
        >
            Sedric Edwards
        </a>

        <!-- Desktop Links -->
        <div class="hidden md:flex items-center gap-8">
            {#each NAV_LINKS as link}
                <a
                    href={link.href}
                    class="nav-link text-ivory/70 text-sm font-medium uppercase tracking-widest capitalize"
                    class:text-champagne={$page.url.pathname === link.href}
                >
                    {link.label}
                </a>
            {/each}
        </div>

        <!-- Hamburger -->
        <button
            class="md:hidden flex flex-col gap-1.5 p-2"
            onclick={() => (menuOpen = !menuOpen)}
            aria-label="Toggle menu"
        >
            <span
                class="block w-6 h-px bg-ivory transition-all duration-300 {menuOpen
                    ? 'rotate-45 translate-y-2 text-champagne'
                    : ''}"
            ></span>
            <span
                class="block w-6 h-px bg-ivory transition-all duration-300 {menuOpen
                    ? 'opacity-0'
                    : ''}"
            ></span>
            <span
                class="block w-6 h-px bg-ivory transition-all duration-300 {menuOpen
                    ? '-rotate-45 -translate-y-2 text-champagne'
                    : ''}"
            ></span>
        </button>
    </div>

    <!-- Mobile Menu -->
    {#if menuOpen}
        <div
            class="md:hidden mt-6 pb-2 flex flex-col gap-4 border-t border-[#2A2A35]/50 pt-6 animate-fade-in"
        >
            {#each NAV_LINKS as link}
                <a
                    href={link.href}
                    onclick={() => (menuOpen = false)}
                    class="text-ivory/80 hover:text-champagne transition-colors text-sm font-medium uppercase tracking-widest px-2"
                    class:text-champagne={$page.url.pathname === link.href}
                >
                    {link.label}
                </a>
            {/each}
        </div>
    {/if}
</nav>

<style>
    :global(.animate-fade-in) {
        animation: fadeIn 0.3s ease-out forwards;
    }

    @keyframes fadeIn {
        from {
            opacity: 0;
            transform: translateY(-5px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }
</style>
