<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    import { ArrowRight } from "lucide-svelte";

    gsap.registerPlugin(ScrollTrigger);

    const PROJECTS = [
        {
            title: "Neon Parallels",
            genre: "Electronic / Ambient",
            type: "Full EP — Mix & Master",
            year: "2024",
            tags: ["5 Tracks", "Stem Mix", "Mastered"],
            color: "#C9A84C",
        },
        {
            title: "Hollow Echo",
            genre: "R&B / Neo-Soul",
            type: "Album — Mixing",
            year: "2024",
            tags: ["12 Tracks", "Full Mix", "Dolby Atmos"],
            color: "#7B8FA1",
        },
        {
            title: "kira.wav",
            genre: "Indie Pop",
            type: "Artist Website",
            year: "2023",
            tags: ["SvelteKit", "Booking", "EPK"],
            color: "#9B8EA8",
        },
        {
            title: "Tidal Shift",
            genre: "Hip-Hop / Trap",
            type: "Single — Mix & Master",
            year: "2025",
            tags: ["Stem Mix", "Mastered", "Streaming Ready"],
            color: "#C9A84C",
        },
    ];

    let heroEl, gridEl;

    onMount(() => {
        const ctx = gsap.context(() => {
            gsap.fromTo(
                heroEl,
                { y: 40, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 1,
                    ease: "power3.out",
                    delay: 0.2,
                },
            );
            gsap.fromTo(
                Array.from(gridEl?.children || []),
                { y: 60, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 0.8,
                    ease: "power3.out",
                    stagger: 0.12,
                    scrollTrigger: { trigger: gridEl, start: "top 85%" },
                },
            );
        });
        return () => ctx.revert();
    });
</script>

<svelte:head>
    <title>Work — Sedric Edwards</title>
    <meta
        name="description"
        content="Selected work by Sedric Edwards — mixing, mastering, and artist website projects."
    />
</svelte:head>

<!-- Hero -->
<section class="pt-40 pb-20 bg-[#0D0D12]">
    <div bind:this={heroEl} class="section-container">
        <p
            class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-4"
        >
            Selected Work
        </p>
        <h1
            class="text-5xl md:text-7xl font-black font-sans text-ivory leading-tight tracking-tight mb-6"
        >
            Proof in the <span class="font-drama italic text-champagne"
                >sound.</span
            >
        </h1>
        <p class="text-ivory/50 text-xl max-w-xl leading-relaxed">
            A curated selection of mixes, masters, and digital experiences
            crafted for artists across genres.
        </p>
    </div>
</section>

<!-- Project Grid -->
<section class="py-24">
    <div class="section-container">
        <div bind:this={gridEl} class="grid grid-cols-1 md:grid-cols-2 gap-6">
            {#each PROJECTS as project}
                <div
                    class="card-lift group relative rounded-[2rem] border border-[#2A2A35]/50 overflow-hidden cursor-pointer"
                    style="background:rgba(42,42,53,0.2)"
                >
                    <!-- Colored accent bar -->
                    <div
                        class="absolute top-0 left-0 right-0 h-1 opacity-60"
                        style="background:{project.color}"
                    />

                    <div class="p-8">
                        <div class="flex items-start justify-between mb-6">
                            <p
                                class="font-mono-custom text-ivory/30 text-xs uppercase tracking-widest"
                            >
                                {project.year}
                            </p>
                            <span
                                class="font-mono-custom text-xs text-champagne/70 uppercase tracking-widest"
                                >{project.genre}</span
                            >
                        </div>

                        <h2
                            class="text-3xl font-black font-sans text-ivory mb-1"
                        >
                            {project.title}
                        </h2>
                        <p class="text-ivory/50 text-sm mb-6">{project.type}</p>

                        <div class="flex flex-wrap gap-2">
                            {#each project.tags as tag}
                                <span
                                    class="px-3 py-1 rounded-full border border-[#2A2A35]/60 text-ivory/40 text-xs font-mono-custom"
                                >
                                    {tag}
                                </span>
                            {/each}
                        </div>
                    </div>
                </div>
            {/each}
        </div>
    </div>
</section>

<!-- CTA -->
<section class="py-24 border-t border-[#2A2A35]/30 bg-[#0D0D12]">
    <div class="section-container text-center max-w-2xl">
        <p
            class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-6"
        >
            Ready to Create?
        </p>
        <h2
            class="text-4xl md:text-5xl font-black font-sans text-ivory leading-tight mb-6"
        >
            Your project could be <span class="font-drama italic text-champagne"
                >next.</span
            >
        </h2>
        <a href="/contact" class="btn-magnetic btn-primary">
            <span class="btn-slide" />
            <span class="relative z-10 flex items-center gap-2"
                >Start a Conversation <ArrowRight size={16} /></span
            >
        </a>
    </div>
</section>
