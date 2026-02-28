<script>
    import Hero from "$lib/components/Hero.svelte";
    import MixingShufflerCard from "$lib/components/MixingShufflerCard.svelte";
    import WebDesignTypewriterCard from "$lib/components/WebDesignTypewriterCard.svelte";
    import PlanningSchedulerCard from "$lib/components/PlanningSchedulerCard.svelte";
    import Philosophy from "$lib/components/Philosophy.svelte";
    import Protocol from "$lib/components/Protocol.svelte";
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    import { ArrowRight } from "lucide-svelte";

    gsap.registerPlugin(ScrollTrigger);

    let titleEl, cardsEl;

    onMount(() => {
        const ctx = gsap.context(() => {
            gsap.fromTo(
                titleEl,
                { y: 40, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 0.9,
                    ease: "power3.out",
                    scrollTrigger: { trigger: titleEl, start: "top 85%" },
                },
            );
            gsap.fromTo(
                Array.from(cardsEl?.children || []),
                { y: 50, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 0.8,
                    ease: "power3.out",
                    stagger: 0.15,
                    scrollTrigger: { trigger: cardsEl, start: "top 80%" },
                },
            );
        });
        return () => ctx.revert();
    });
</script>

<svelte:head>
    <title>Sedric Edwards — Music Technologist</title>
    <meta
        name="description"
        content="Sedric Edwards — Music technologist, mixer, and mastering engineer. Crafting bespoke sonic experiences where human intuition meets technical mastery."
    />
</svelte:head>

<Hero />

<!-- Services Overview -->
<section id="work" class="py-28 md:py-40">
    <div class="section-container">
        <div bind:this={titleEl} class="mb-16 md:mb-20">
            <p
                class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-4"
            >
                What I Offer
            </p>
            <h2
                class="text-4xl md:text-6xl font-black font-sans text-ivory leading-tight tracking-tight"
            >
                Services built for<br />
                <span class="font-drama italic text-champagne"
                    >artists, by an artist.</span
                >
            </h2>
        </div>
        <div bind:this={cardsEl} class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <MixingShufflerCard />
            <WebDesignTypewriterCard />
            <PlanningSchedulerCard />
        </div>
        <div class="mt-12 text-center">
            <a href="/services" class="btn-magnetic btn-outline">
                <span class="btn-slide" />
                <span class="relative z-10 flex items-center gap-2"
                    >View All Services <ArrowRight size={16} /></span
                >
            </a>
        </div>
    </div>
</section>

<Philosophy />
<Protocol />
