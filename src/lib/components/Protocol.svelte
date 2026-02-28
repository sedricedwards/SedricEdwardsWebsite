<script>
    import GeometricCanvas from "./GeometricCanvas.svelte";
    import LaserGridCanvas from "./LaserGridCanvas.svelte";
    import EKGCanvas from "./EKGCanvas.svelte";

    const STEPS = [
        {
            num: "01",
            title: "First Contact",
            desc: "We talk. You share your vision, your sound, your goals. No forms — just a real conversation about what you want to build.",
            Canvas: GeometricCanvas,
            bg: "#16161f",
        },
        {
            num: "02",
            title: "Strategic Design",
            desc: "Every element is mapped with intention — from mix architecture to website wireframes. Nothing is deployed without a plan.",
            Canvas: LaserGridCanvas,
            bg: "#121219",
        },
        {
            num: "03",
            title: "Delivery & Iteration",
            desc: "You receive a premium deliverable. We refine together until it feels exactly right. Your satisfaction is the only metric.",
            Canvas: EKGCanvas,
            bg: "#0f0f16",
        },
    ];
</script>

<section id="protocol" class="bg-[#0D0D12]">
    <div class="section-container py-16">
        <p
            class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-4"
        >
            The Process
        </p>
        <h2
            class="text-4xl md:text-6xl font-black font-sans text-ivory leading-tight tracking-tight mb-20"
        >
            How we work<br />
            <span class="font-drama italic text-ivory/40">together.</span>
        </h2>
    </div>

    {#each STEPS as step, i}
        <div class="protocol-card" style="z-index:{10 + i}">
            <div
                class="relative mx-auto w-full max-w-5xl rounded-[3rem] overflow-hidden border border-[#2A2A35]/40 shadow-2xl"
                style="background:{step.bg}"
            >
                <div
                    class="flex flex-col md:flex-row items-center gap-12 p-10 md:p-16"
                >
                    <div
                        class="flex-shrink-0 flex items-center justify-center w-[260px] h-[200px]"
                    >
                        <svelte:component this={step.Canvas} />
                    </div>
                    <div class="flex-1">
                        <span
                            class="font-mono-custom text-champagne text-xs tracking-[0.3em]"
                            >STEP {step.num}</span
                        >
                        <h3
                            class="text-3xl md:text-5xl font-black font-sans text-ivory mt-3 mb-5 leading-tight"
                        >
                            {step.title}
                        </h3>
                        <p
                            class="text-ivory/60 text-lg leading-relaxed max-w-md"
                        >
                            {step.desc}
                        </p>
                    </div>
                </div>
            </div>
        </div>
    {/each}

    <div class="h-24" />
</section>
