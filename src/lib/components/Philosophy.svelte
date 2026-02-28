<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";

    gsap.registerPlugin(ScrollTrigger);

    let sectionEl, line1El, line2El;

    onMount(() => {
        const ctx = gsap.context(() => {
            gsap.fromTo(
                line1El,
                { y: 60, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 1.1,
                    ease: "power3.out",
                    scrollTrigger: { trigger: sectionEl, start: "top 75%" },
                },
            );
            gsap.fromTo(
                line2El,
                { y: 80, opacity: 0 },
                {
                    y: 0,
                    opacity: 1,
                    duration: 1.3,
                    ease: "power3.out",
                    delay: 0.2,
                    scrollTrigger: { trigger: sectionEl, start: "top 75%" },
                },
            );
        }, sectionEl);
        return () => ctx.revert();
    });
</script>

<section
    id="philosophy"
    bind:this={sectionEl}
    class="relative py-32 md:py-48 overflow-hidden"
>
    <div class="absolute inset-0">
        <img
            src="https://images.unsplash.com/photo-1470225620780-dba8ba36b745?w=1920&q=70"
            alt="Ambient dark soundscape"
            class="w-full h-full object-cover opacity-10"
        />
        <div class="absolute inset-0 bg-[#2A2A35]/90" />
    </div>

    <div class="relative z-10 section-container">
        <p
            bind:this={line1El}
            class="text-ivory/40 text-lg md:text-2xl font-light max-w-2xl mb-8 leading-relaxed"
        >
            Most in the industry focus on&nbsp;
            <em class="text-ivory/60 not-italic"
                >volume — churning out tracks, templates, cookie-cutter results.</em
            >
        </p>
        <div bind:this={line2El}>
            <p
                class="text-ivory text-3xl md:text-5xl lg:text-6xl font-black font-sans leading-tight max-w-3xl"
            >
                We focus on&nbsp;<span class="font-drama italic text-champagne"
                    >intention.</span
                >
            </p>
            <p
                class="mt-6 text-2xl md:text-4xl font-drama italic text-ivory/80 leading-tight max-w-3xl"
            >
                Every session, every pixel, every decision — made with
                <span class="text-champagne"> you</span> in mind.
            </p>
        </div>
    </div>
</section>
