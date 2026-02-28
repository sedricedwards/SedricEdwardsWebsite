<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ArrowRight, ChevronDown } from "lucide-svelte";

    let containerEl, lineOneEl, lineTwoEl, subEl, ctaEl, scrollEl;

    onMount(() => {
        const ctx = gsap.context(() => {
            const tl = gsap.timeline({ delay: 0.3 });
            tl.fromTo(
                lineOneEl,
                { y: 50, opacity: 0 },
                { y: 0, opacity: 1, duration: 1.1, ease: "power3.out" },
            )
                .fromTo(
                    lineTwoEl,
                    { y: 60, opacity: 0 },
                    { y: 0, opacity: 1, duration: 1.2, ease: "power3.out" },
                    "-=0.7",
                )
                .fromTo(
                    subEl,
                    { y: 30, opacity: 0 },
                    { y: 0, opacity: 1, duration: 0.9, ease: "power3.out" },
                    "-=0.6",
                )
                .fromTo(
                    ctaEl,
                    { y: 20, opacity: 0 },
                    { y: 0, opacity: 1, duration: 0.8, ease: "power3.out" },
                    "-=0.5",
                )
                .fromTo(
                    scrollEl,
                    { opacity: 0 },
                    { opacity: 1, duration: 0.6 },
                    "-=0.2",
                );
        }, containerEl);
        return () => ctx.revert();
    });
</script>

<section
    id="hero"
    bind:this={containerEl}
    class="relative min-h-[100dvh] flex items-end overflow-hidden"
>
    <!-- Background -->
    <div class="absolute inset-0">
        <img
            src="/hero_background.png"
            alt="Abstract visualization of music mixing and mastering with glowing soundwaves"
            class="w-full h-full object-cover object-center"
        />
        <div
            class="absolute inset-0 bg-gradient-to-t from-[#0D0D12] via-[#0D0D12]/70 to-[#0D0D12]/20"
        />
        <div
            class="absolute inset-0 bg-gradient-to-r from-[#0D0D12]/60 to-transparent"
        />
    </div>

    <!-- Content -->
    <div class="relative z-10 section-container w-full pb-24 md:pb-32">
        <div class="max-w-3xl">
            <p
                class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-6 opacity-90"
            >
                Music Technologist · Sound · Future
            </p>

            <h1 class="sr-only">Sedric Edwards — Music Technologist. Sound meets Precision.</h1>

            <div bind:this={lineOneEl}>
                <span
                    class="block text-4xl md:text-6xl lg:text-7xl font-sans font-black text-ivory leading-tight tracking-tight"
                >
                    Sound meets
                </span>
            </div>
            <div bind:this={lineTwoEl}>
                <span
                    class="block font-drama italic text-6xl md:text-8xl lg:text-[9rem] leading-none text-champagne"
                >
                    Precision.
                </span>
            </div>

            <p
                bind:this={subEl}
                class="mt-6 text-ivory/60 text-lg md:text-xl font-light max-w-lg leading-relaxed"
            >
                Sedric Edwards — musician with the future in view. Crafting
                bespoke sonic experiences where human intuition meets technical
                mastery.
            </p>

            <div bind:this={ctaEl} class="mt-10 flex flex-wrap gap-4">
                <a href="/contact" class="btn-magnetic btn-primary">
                    <span class="btn-slide" />
                    <span class="relative z-10 flex items-center gap-2">
                        Book a Session <ArrowRight size={16} />
                    </span>
                </a>
                <a href="/work" class="btn-magnetic btn-outline">
                    <span class="btn-slide" />
                    <span class="relative z-10">Explore My Work</span>
                </a>
            </div>
        </div>
    </div>

    <!-- Scroll Indicator -->
    <div
        bind:this={scrollEl}
        class="absolute bottom-8 left-1/2 -translate-x-1/2 z-10 flex flex-col items-center gap-2 opacity-50"
    >
        <span
            class="font-mono-custom text-ivory text-xs tracking-widest uppercase"
            >Scroll</span
        >
        <ChevronDown size={16} class="text-champagne animate-bounce" />
    </div>
</section>
