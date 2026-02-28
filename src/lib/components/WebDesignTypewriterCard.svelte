<script>
    import { onMount } from "svelte";
    import { Globe } from "lucide-svelte";

    const MESSAGES = [
        "Designing your artist landing page...",
        "Injecting brand identity...",
        "Wiring booking integrations...",
        "Optimizing for conversion...",
        "Launching your digital presence...",
    ];

    let msgIdx = 0;
    let displayed = "";
    let charIdx = 0;
    /** @type {number | undefined} */
    let timeout;

    function tick() {
        const msg = MESSAGES[msgIdx];
        if (charIdx < msg.length) {
            displayed = msg.slice(0, charIdx + 1);
            charIdx++;
            timeout = setTimeout(tick, 45);
        } else {
            timeout = setTimeout(() => {
                msgIdx = (msgIdx + 1) % MESSAGES.length;
                charIdx = 0;
                displayed = "";
                tick();
            }, 2200);
        }
    }

    onMount(() => {
        tick();
        return () => {
            if (timeout !== undefined) clearTimeout(timeout);
        };
    });
</script>

<div
    class="card-lift h-full bg-[#2A2A35]/30 border border-[#2A2A35]/50 rounded-[2rem] p-8 flex flex-col"
>
    <div class="flex items-center gap-3 mb-6">
        <Globe size={20} class="text-champagne" />
        <span
            class="text-ivory/50 text-xs font-mono-custom uppercase tracking-widest"
            >Live Feed</span
        >
        <!-- Explicit closing tag required in Svelte 5 for non-void elements -->
        <span class="w-1.5 h-1.5 rounded-full bg-champagne pulse-dot ml-1"
        ></span>
    </div>
    <h3 class="text-ivory text-xl font-bold font-sans mb-2 leading-tight">
        Artist Web Design
    </h3>
    <p class="text-ivory/50 text-sm leading-relaxed mb-8">
        Custom sites built specifically with your artistic vision in mind.
    </p>

    <div
        class="mt-auto bg-[#0D0D12]/80 rounded-2xl border border-[#2A2A35]/40 p-5 flex-1 flex flex-col justify-center min-h-[120px]"
    >
        <div class="flex items-center gap-2 mb-4">
            <!-- Traffic light dots — explicit closing tags for Svelte 5 compliance -->
            <span class="w-2.5 h-2.5 rounded-full bg-red-500/50"></span>
            <span class="w-2.5 h-2.5 rounded-full bg-yellow-500/50"></span>
            <span class="w-2.5 h-2.5 rounded-full bg-green-500/50"></span>
        </div>
        <p class="font-mono-custom text-champagne text-sm leading-relaxed">
            <span class="text-ivory/40">$&nbsp;</span>{displayed}<span
                class="cursor-blink text-champagne ml-0.5">▌</span
            >
        </p>
    </div>
</div>
