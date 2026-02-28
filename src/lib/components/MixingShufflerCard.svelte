<script>
    import { onMount } from "svelte";
    import { Headphones } from "lucide-svelte";

    const ALL_LABELS = [
        "Deep Mix Analysis",
        "Stem Separation",
        "Frequency Mastery",
    ];
    const CHAMPAGNE = "#C9A84C";
    const IVORY = "#FAF8F5";

    let topIdx = 0;

    function getLabel(offset) {
        return ALL_LABELS[(topIdx + offset) % ALL_LABELS.length];
    }

    onMount(() => {
        const interval = setInterval(() => {
            topIdx = (topIdx + 1) % ALL_LABELS.length;
        }, 2800);
        return () => clearInterval(interval);
    });
</script>

<div
    class="card-lift h-full bg-[#2A2A35]/30 border border-[#2A2A35]/50 rounded-[2rem] p-8 flex flex-col"
>
    <div class="flex items-center gap-3 mb-6">
        <Headphones size={20} class="text-champagne" />
        <span
            class="text-ivory/50 text-xs font-mono-custom uppercase tracking-widest"
            >Mix Engine</span
        >
    </div>
    <h3 class="text-ivory text-xl font-bold font-sans mb-2 leading-tight">
        Personalized Mixing
    </h3>
    <p class="text-ivory/50 text-sm leading-relaxed mb-8">
        With a human touch that no algorithm can replicate.
    </p>

    <div class="relative flex-1 flex flex-col gap-3 mt-auto">
        {#each [0, 1, 2] as offset}
            {@const label = getLabel(offset)}
            <div
                class="flex items-center gap-3 px-5 py-3.5 rounded-2xl border transition-all duration-700"
                style:background={offset === 0
                    ? "rgba(201,168,76,0.12)"
                    : "rgba(42,42,53,0.5)"}
                style:border-color={offset === 0
                    ? "rgba(201,168,76,0.4)"
                    : "rgba(255,255,255,0.06)"}
                style:transform={`scale(${1 - offset * 0.025})`}
                style:opacity={String(1 - offset * 0.2)}
            >
                <!-- Explicit closing tag required in Svelte 5 for non-void elements -->
                <span
                    class="w-2 h-2 rounded-full"
                    style:background={offset === 0 ? CHAMPAGNE : "#ffffff30"}
                ></span>
                <span
                    class="font-mono-custom text-sm"
                    style:color={offset === 0 ? CHAMPAGNE : IVORY + "99"}
                >
                    {label}
                </span>
            </div>
        {/each}
    </div>
</div>
