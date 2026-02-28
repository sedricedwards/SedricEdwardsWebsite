<script>
    import MixingShufflerCard from "$lib/components/MixingShufflerCard.svelte";
    import WebDesignTypewriterCard from "$lib/components/WebDesignTypewriterCard.svelte";
    import PlanningSchedulerCard from "$lib/components/PlanningSchedulerCard.svelte";
    import Pricing from "$lib/components/Pricing.svelte";
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";

    gsap.registerPlugin(ScrollTrigger);

    let heroEl;

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
        });
        return () => ctx.revert();
    });
</script>

<svelte:head>
    <title>Services — Sedric Edwards</title>
    <meta
        name="description"
        content="Professional mixing, mastering, and artist website design services by Sedric Edwards."
    />
</svelte:head>

<!-- Page Hero -->
<section class="pt-40 pb-20 bg-[#0D0D12]">
    <div bind:this={heroEl} class="section-container">
        <p
            class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-4"
        >
            What I Offer
        </p>
        <h1
            class="text-5xl md:text-7xl font-black font-sans text-ivory leading-tight tracking-tight mb-6"
        >
            Services built for<br />
            <span class="font-drama italic text-champagne"
                >artists, by an artist.</span
            >
        </h1>
        <p class="text-ivory/50 text-xl max-w-xl leading-relaxed">
            Every service is designed with one goal: giving your art the sonic
            and digital presence it deserves.
        </p>
    </div>
</section>

<!-- Interactive Service Cards -->
<section class="py-24 bg-[#0D0D12]">
    <div class="section-container">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <MixingShufflerCard />
            <WebDesignTypewriterCard />
            <PlanningSchedulerCard />
        </div>
    </div>
</section>

<!-- Service Detail: Mixing & Mastering -->
<section class="py-24 border-t border-[#2A2A35]/30">
    <div class="section-container">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-16 items-center">
            <div>
                <p
                    class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-4"
                >
                    Service 01
                </p>
                <h2
                    class="text-4xl md:text-5xl font-black font-sans text-ivory leading-tight mb-6"
                >
                    Mixing &amp; <span class="font-drama italic text-champagne"
                        >Mastering</span
                    >
                </h2>
                <p class="text-ivory/60 text-lg leading-relaxed mb-6">
                    Whether you have a single or a full album, every track gets
                    the same level of attention. Deep mix analysis, surgical EQ,
                    dynamic control, and a master that translates across every
                    platform.
                </p>
                <ul class="space-y-3 mb-8">
                    {#each ["Stem mixing & multitrack editing", "Frequency & dynamics processing", "Loudness standards for Spotify, Apple Music & more", "Reference track matching", "Unlimited revisions (Performance & Enterprise)"] as item}
                        <li
                            class="flex items-start gap-3 text-ivory/70 text-sm"
                        >
                            <span class="text-champagne mt-1">—</span>{item}
                        </li>
                    {/each}
                </ul>
                <a href="/contact" class="btn-magnetic btn-primary">
                    <span class="btn-slide" />
                    <span class="relative z-10">Book a Mix Session</span>
                </a>
            </div>
            <div
                class="rounded-[2rem] bg-[#2A2A35]/30 border border-[#2A2A35]/50 p-10 flex flex-col gap-4"
            >
                {#each ["Stem Delivery", "Mix Review", "Master Pass", "Platform Export"] as step, i}
                    <div class="flex items-center gap-4">
                        <span
                            class="w-8 h-8 rounded-full border border-champagne/40 flex items-center justify-center font-mono-custom text-champagne text-xs"
                            >0{i + 1}</span
                        >
                        <span class="text-ivory/70 text-sm">{step}</span>
                    </div>
                    {#if i < 3}<div class="w-px h-4 bg-[#2A2A35] ml-4" />{/if}
                {/each}
            </div>
        </div>
    </div>
</section>

<!-- Service Detail: Artist Web Design -->
<section class="py-24 border-t border-[#2A2A35]/30 bg-[#0D0D12]">
    <div class="section-container">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-16 items-center">
            <div
                class="order-2 md:order-1 rounded-[2rem] bg-[#2A2A35]/30 border border-[#2A2A35]/50 p-10"
            >
                <div
                    class="font-mono-custom text-xs text-ivory/30 mb-4 uppercase tracking-widest"
                >
                    Live Preview
                </div>
                <div class="space-y-2">
                    {#each ["Hero Section", "Bio & Story", "Music Player", "Booking Form", "Social Links"] as el}
                        <div
                            class="flex items-center gap-3 px-4 py-2.5 rounded-xl bg-[#0D0D12]/60 border border-[#2A2A35]/40"
                        >
                            <span
                                class="w-1.5 h-1.5 rounded-full bg-champagne/60"
                            />
                            <span class="text-ivory/60 text-sm">{el}</span>
                        </div>
                    {/each}
                </div>
            </div>
            <div class="order-1 md:order-2">
                <p
                    class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-4"
                >
                    Service 02
                </p>
                <h2
                    class="text-4xl md:text-5xl font-black font-sans text-ivory leading-tight mb-6"
                >
                    Artist Web <span class="font-drama italic text-champagne"
                        >Design</span
                    >
                </h2>
                <p class="text-ivory/60 text-lg leading-relaxed mb-8">
                    Your website is your digital stage. We build premium artist
                    sites that capture your sound visually — fast, mobile-first,
                    and built to convert visitors into fans and clients.
                </p>
                <a href="/contact" class="btn-magnetic btn-outline">
                    <span class="btn-slide" />
                    <span class="relative z-10">Start Your Site</span>
                </a>
            </div>
        </div>
    </div>
</section>

<Pricing />
