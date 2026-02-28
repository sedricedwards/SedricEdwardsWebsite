<script>
    import { onMount } from "svelte";
    import { Calendar } from "lucide-svelte";

    const DAYS = ["S", "M", "T", "W", "T", "F", "S"];
    let activeDay = /** @type {number | null} */ (null);
    let saved = false;
    let cursorDay = /** @type {number | 'save' | null} */ (null);
    let step = 0;

    const CHAMPAGNE = "#C9A84C";
    const IVORY = "#FAF8F5";

    onMount(() => {
        const steps = [
            () => {
                cursorDay = 1;
            },
            () => {
                activeDay = 1;
                cursorDay = 1;
            },
            () => {
                cursorDay = 3;
            },
            () => {
                activeDay = 3;
                cursorDay = 3;
            },
            () => {
                cursorDay = "save";
            },
            () => {
                saved = true;
            },
            () => {
                saved = false;
                activeDay = null;
                cursorDay = null;
            },
        ];
        const interval = setInterval(() => {
            steps[step % steps.length]();
            step++;
        }, 900);
        return () => clearInterval(interval);
    });
</script>

<div
    class="card-lift h-full bg-[#2A2A35]/30 border border-[#2A2A35]/50 rounded-[2rem] p-8 flex flex-col"
>
    <div class="flex items-center gap-3 mb-6">
        <Calendar size={20} class="text-champagne" />
        <span
            class="text-ivory/50 text-xs font-mono-custom uppercase tracking-widest"
            >Scheduler</span
        >
    </div>
    <h3 class="text-ivory text-xl font-bold font-sans mb-2 leading-tight">
        Meticulous Planning
    </h3>
    <p class="text-ivory/50 text-sm leading-relaxed mb-6">
        In tune with what you need — every detail, carefully considered.
    </p>

    <div class="mt-auto">
        <div class="grid grid-cols-7 gap-2 mb-5">
            {#each DAYS as day, i}
                <div class="flex flex-col items-center gap-2">
                    <span class="text-ivory/40 text-xs font-mono-custom"
                        >{day}</span
                    >
                    <div
                        class="w-8 h-8 rounded-lg flex items-center justify-center text-xs font-mono-custom transition-all duration-300"
                        style:background={activeDay === i
                            ? "rgba(201,168,76,0.2)"
                            : "rgba(255,255,255,0.04)"}
                        style:border={"1px solid " +
                            (activeDay === i
                                ? CHAMPAGNE + "66"
                                : "rgba(255,255,255,0.06)")}
                        style:color={activeDay === i ? CHAMPAGNE : IVORY + "40"}
                        style:transform={cursorDay === i
                            ? "scale(0.95)"
                            : "scale(1)"}
                        style:box-shadow={activeDay === i
                            ? "0 0 12px rgba(201,168,76,0.2)"
                            : "none"}
                    >
                        {i + 1}
                    </div>
                </div>
            {/each}
        </div>
        <button
            class="w-full py-2.5 rounded-xl border transition-all duration-300 font-mono-custom text-xs tracking-widest uppercase"
            style:background={saved
                ? "rgba(201,168,76,0.15)"
                : "rgba(255,255,255,0.04)"}
            style:border-color={saved
                ? CHAMPAGNE + "60"
                : "rgba(255,255,255,0.08)"}
            style:color={saved ? CHAMPAGNE : IVORY + "50"}
            style:transform={cursorDay === "save" ? "scale(0.97)" : "scale(1)"}
        >
            {saved ? "✓ Session Saved" : "Save Session"}
        </button>
    </div>
</div>
