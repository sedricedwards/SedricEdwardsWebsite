<footer class="rounded-t-[4rem] pt-16 pb-10" style="background:#06060a">
    <div class="section-container">
        <div class="grid grid-cols-1 md:grid-cols-4 gap-12 mb-14">
            <!-- Brand -->
            <div class="md:col-span-2">
                <h3 class="font-drama italic text-champagne text-2xl mb-3">
                    Sedric Edwards
                </h3>
                <p class="text-ivory/40 text-sm leading-relaxed max-w-xs">
                    Musician with the future in view. Blending human emotion
                    with technical precision to create sounds and digital
                    experiences that last.
                </p>
                <div class="flex items-center gap-2 mt-6">
                    <span class="w-2 h-2 rounded-full bg-green-400 pulse-dot" />
                    <span
                        class="font-mono-custom text-xs text-ivory/40 uppercase tracking-widest"
                        >Systems Operational</span
                    >
                </div>
            </div>

            <!-- Navigation -->
            <div>
                <p
                    class="font-mono-custom text-ivory/30 text-xs uppercase tracking-widest mb-5"
                >
                    Navigate
                </p>
                <ul class="space-y-3">
                    {#each [["Home", "/"], ["Work", "/work"], ["Services", "/services"], ["Contact", "/contact"]] as [label, href]}
                        <li>
                            <a
                                {href}
                                class="text-ivory/50 text-sm hover:text-champagne transition-colors"
                            >
                                {label}
                            </a>
                        </li>
                    {/each}
                </ul>
            </div>

            <!-- Services -->
            <div>
                <p
                    class="font-mono-custom text-ivory/30 text-xs uppercase tracking-widest mb-5"
                >
                    Services
                </p>
                <ul class="space-y-3 text-ivory/50 text-sm">
                    <li>Mix &amp; Master</li>
                    <li>Artist Websites</li>
                    <li>Session Planning</li>
                    <li>Consultation</li>
                </ul>
            </div>
        </div>

        <div
            class="border-t border-[#2A2A35]/30 pt-8 flex flex-col md:flex-row items-center justify-between gap-4"
        >
            <p class="text-ivory/20 font-mono-custom text-xs">
                © {new Date().getFullYear()} Sedric Edwards. All rights reserved.
            </p>
            <p
                class="text-ivory/20 font-mono-custom text-xs tracking-widest uppercase"
            >
                Musician · Technologist · Visionary
            </p>
        </div>
    </div>
</footer>
