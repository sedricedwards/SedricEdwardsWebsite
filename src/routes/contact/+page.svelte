<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ArrowRight, Zap } from "lucide-svelte";

    // IMPORTANT: Replace YOUR_FORMSPREE_ID with your real Formspree form ID
    // Sign up at https://formspree.io, create a form, and paste the ID here.
    const FORMSPREE_ENDPOINT = "https://formspree.io/f/mzdaqzwa";

    let form = { name: "", email: "", type: "mix", message: "" };
    let status = "idle"; // 'idle' | 'loading' | 'success' | 'error'
    let errorMsg = "";
    let formEl;

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

    /** @param {SubmitEvent} e */
    async function handleSubmit(e) {
        e.preventDefault();
        status = "loading";
        errorMsg = "";
        try {
            const data = new FormData(formEl);
            const res = await fetch(FORMSPREE_ENDPOINT, {
                method: "POST",
                body: data,
                headers: { Accept: "application/json" },
            });
            if (res.ok) {
                status = "success";
                form = { name: "", email: "", type: "mix", message: "" };
            } else {
                const json = await res.json().catch(() => ({}));
                errorMsg =
                    json?.errors?.[0]?.message ??
                    "Something went wrong. Please try again.";
                status = "error";
            }
        } catch {
            errorMsg =
                "Network error. Please check your connection and try again.";
            status = "error";
        }
    }
</script>

<svelte:head>
    <title>Contact — Sedric Edwards</title>
    <meta
        name="description"
        content="Book a mixing, mastering, or web design session with Sedric Edwards."
    />
</svelte:head>

<!-- Hero -->
<section class="relative pt-40 pb-16 overflow-hidden">
    <div class="absolute inset-0">
        <img
            src="https://images.unsplash.com/photo-1614854262318-831574f15f1f?w=1920&q=70"
            alt="Dark studio ambience"
            class="w-full h-full object-cover opacity-5"
        />
        <div
            class="absolute inset-0 bg-gradient-to-b from-[#0D0D12] via-[#2A2A35]/40 to-[#0D0D12]"
        ></div>
    </div>

    <div bind:this={heroEl} class="relative z-10 section-container max-w-3xl">
        <div class="text-center mb-14">
            <p
                class="font-mono-custom text-champagne text-xs tracking-[0.3em] uppercase mb-4"
            >
                Let's Create
            </p>
            <h1
                class="text-4xl md:text-6xl font-black font-sans text-ivory leading-tight tracking-tight"
            >
                Ready to begin?<br />
                <span class="font-drama italic text-champagne"
                    >I'm listening.</span
                >
            </h1>
        </div>

        {#if status === "success"}
            <!-- Success State -->
            <div
                class="text-center py-16 border border-champagne/30 rounded-[2rem] bg-champagne/5 backdrop-blur-sm"
            >
                <Zap size={40} class="text-champagne mx-auto mb-5" />
                <h3 class="text-2xl font-bold text-ivory mb-3">
                    Message received.
                </h3>
                <p class="text-ivory/60">
                    I'll be in touch within 24 hours. Let's build something
                    extraordinary.
                </p>
                <button
                    on:click={() => (status = "idle")}
                    class="mt-8 btn-magnetic btn-outline text-sm px-6 py-3"
                >
                    <span class="btn-slide"></span>
                    <span class="relative z-10">Send Another</span>
                </button>
            </div>
        {:else}
            <!-- Form -->
            <form bind:this={formEl} on:submit={handleSubmit} class="space-y-5">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
                    <div>
                        <label
                            for="name"
                            class="block text-ivory/50 text-xs font-mono-custom uppercase tracking-widest mb-2"
                            >Name</label
                        >
                        <input
                            id="name"
                            name="name"
                            type="text"
                            required
                            bind:value={form.name}
                            class="w-full bg-[#2A2A35]/30 border border-[#2A2A35]/60 rounded-2xl px-5 py-4 text-ivory placeholder-ivory/30 text-sm focus:outline-none focus:border-champagne/60 transition-colors"
                            placeholder="Your name"
                        />
                    </div>
                    <div>
                        <label
                            for="email"
                            class="block text-ivory/50 text-xs font-mono-custom uppercase tracking-widest mb-2"
                            >Email</label
                        >
                        <input
                            id="email"
                            name="email"
                            type="email"
                            required
                            bind:value={form.email}
                            class="w-full bg-[#2A2A35]/30 border border-[#2A2A35]/60 rounded-2xl px-5 py-4 text-ivory placeholder-ivory/30 text-sm focus:outline-none focus:border-champagne/60 transition-colors"
                            placeholder="your@email.com"
                        />
                    </div>
                </div>

                <div>
                    <label
                        for="type"
                        class="block text-ivory/50 text-xs font-mono-custom uppercase tracking-widest mb-2"
                        >I need help with</label
                    >
                    <select
                        id="type"
                        name="type"
                        bind:value={form.type}
                        class="w-full border border-[#2A2A35]/60 rounded-2xl px-5 py-4 text-ivory text-sm focus:outline-none focus:border-champagne/60 transition-colors appearance-none"
                        style="background:rgba(42,42,53,0.4)"
                    >
                        <option value="mix">Mixing &amp; Mastering</option>
                        <option value="web">Artist Website Design</option>
                        <option value="both">Both — Full Package</option>
                        <option value="other">Something else</option>
                    </select>
                </div>

                <div>
                    <label
                        for="message"
                        class="block text-ivory/50 text-xs font-mono-custom uppercase tracking-widest mb-2"
                        >Tell me about your project</label
                    >
                    <textarea
                        id="message"
                        name="message"
                        required
                        rows={5}
                        bind:value={form.message}
                        class="w-full bg-[#2A2A35]/30 border border-[#2A2A35]/60 rounded-2xl px-5 py-4 text-ivory placeholder-ivory/30 text-sm focus:outline-none focus:border-champagne/60 transition-colors resize-none"
                        placeholder="Describe your vision, sound, and goals..."
                    ></textarea>
                </div>

                {#if status === "error"}
                    <p class="text-red-400 text-sm font-mono-custom">
                        {errorMsg}
                    </p>
                {/if}

                <button
                    type="submit"
                    disabled={status === "loading"}
                    class="btn-magnetic btn-primary w-full py-5 text-sm disabled:opacity-60"
                >
                    <span class="btn-slide"></span>
                    <span
                        class="relative z-10 flex items-center justify-center gap-2"
                    >
                        {#if status === "loading"}
                            <span
                                class="w-4 h-4 rounded-full border-2 border-[#0D0D12]/30 border-t-[#0D0D12] animate-spin"
                            ></span>
                            Sending...
                        {:else}
                            Send Message <ArrowRight size={16} />
                        {/if}
                    </span>
                </button>
            </form>
        {/if}
    </div>
</section>

<!-- Info Row -->
<section class="py-20 bg-[#0D0D12] border-t border-[#2A2A35]/30">
    <div class="section-container grid grid-cols-1 md:grid-cols-3 gap-8">
        {#each [{ label: "Response Time", value: "Within 24 hours" }, { label: "Availability", value: "Mon – Sat, 10am – 8pm PST" }, { label: "Location", value: "Remote · Worldwide" }] as info}
            <div class="text-center">
                <p
                    class="font-mono-custom text-ivory/30 text-xs uppercase tracking-widest mb-2"
                >
                    {info.label}
                </p>
                <p class="text-ivory font-sans font-semibold text-lg">
                    {info.value}
                </p>
            </div>
        {/each}
    </div>
</section>
