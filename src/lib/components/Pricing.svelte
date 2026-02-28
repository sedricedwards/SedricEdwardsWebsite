<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    import { ArrowRight, CheckCircle } from "lucide-svelte";

    gsap.registerPlugin(ScrollTrigger);

    const TIERS = [
        {
            name: "Essential",
            price: "From $299",
            desc: "Perfect for independent artists getting started.",
            features: [
                "2-track mix & master",
                "Basic artist website",
                "1 revision round",
                "Email support",
            ],
            cta: "Get Started",
            featured: false,
        },
        {
            name: "Performance",
            price: "From $799",
            desc: "For serious artists ready to level up their presence.",
            features: [
                "Full EP mix & master",
                "Premium artist website",
                "Unlimited revisions",
                "Priority support",
                "Session planning call",
            ],
            cta: "Book a Session",
            featured: true,
        },
        {
            name: "Enterprise",
            price: "Custom",
            desc: "Labels, studios, and artists with complex needs.",
            features: [
                "Full album production",
                "Multi-page web platform",
                "Ongoing retainer",
                "Dedicated line",
                "Custom integrations",
            ],
            cta: "Collaborate",
            featured: false,
        },
    ];

    let sectionEl, titleEl, cardsEl;

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
                    scrollTrigger: { trigger: sectionEl, start: "top 80%" },
                },
            );
            gsap.fromTo(
                Array.from(cardsEl?.children || []),
                { y: 60, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 0.9,
                    ease: "power3.out",
                    stagger: 0.15,
                    scrollTrigger: { trigger: cardsEl, start: "top 80%" },
                },
            );
        }, sectionEl);
        return () => ctx.revert();
    });
</script>

<section bind:this={sectionEl} class="py-32 md:py-48 bg-[#0D0D12]">
    <div class="section-container">
        <div bind:this={titleEl} class="text-center mb-16 md:mb-20">
            <p
                class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-4"
            >
                Investment
            </p>
            <h2
                class="text-4xl md:text-6xl font-black font-sans text-ivory leading-tight tracking-tight"
            >
                Choose your<br />
                <span class="font-drama italic text-champagne"
                    >collaboration.</span
                >
            </h2>
        </div>

        <div
            bind:this={cardsEl}
            class="grid grid-cols-1 md:grid-cols-3 gap-6 items-stretch"
        >
            {#each TIERS as tier}
                <div
                    class="relative rounded-[2rem] p-8 flex flex-col border transition-all duration-300 card-lift
						{tier.featured
                        ? 'border-champagne/50 ring-1 ring-champagne/20'
                        : 'border-[#2A2A35]/40'}"
                    style="background:{tier.featured
                        ? '#1a1810'
                        : 'rgba(42,42,53,0.3)'}"
                >
                    {#if tier.featured}
                        <div
                            class="absolute -top-4 left-1/2 -translate-x-1/2 bg-champagne text-[#0D0D12] text-xs font-bold font-mono-custom uppercase tracking-widest px-5 py-1.5 rounded-full"
                        >
                            Most Popular
                        </div>
                    {/if}

                    <div class="mb-6">
                        <h3 class="text-ivory font-bold text-lg mb-1">
                            {tier.name}
                        </h3>
                        <p class="text-ivory/50 text-sm leading-relaxed">
                            {tier.desc}
                        </p>
                    </div>
                    <div class="mb-8">
                        <span
                            class="text-3xl font-black font-sans {tier.featured
                                ? 'text-champagne'
                                : 'text-ivory'}">{tier.price}</span
                        >
                    </div>
                    <ul class="space-y-3 mb-10 flex-1">
                        {#each tier.features as f}
                            <li
                                class="flex items-center gap-3 text-sm text-ivory/70"
                            >
                                <CheckCircle
                                    size={15}
                                    class="text-champagne flex-shrink-0"
                                />{f}
                            </li>
                        {/each}
                    </ul>
                    <a
                        href="/contact"
                        class="btn-magnetic w-full {tier.featured
                            ? 'btn-primary'
                            : 'btn-outline'}"
                    >
                        <span class="btn-slide" />
                        <span
                            class="relative z-10 flex items-center justify-center gap-2"
                        >
                            {tier.cta}
                            <ArrowRight size={15} />
                        </span>
                    </a>
                </div>
            {/each}
        </div>
    </div>
</section>
