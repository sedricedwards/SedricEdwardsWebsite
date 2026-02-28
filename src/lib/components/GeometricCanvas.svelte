<script>
    import { onMount, onDestroy } from "svelte";
    let canvasEl;
    let raf;

    onMount(() => {
        const canvas = canvasEl;
        const ctx = canvas.getContext("2d");
        let angle = 0;

        const draw = () => {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            const cx = canvas.width / 2,
                cy = canvas.height / 2;
            for (let r = 30; r <= 120; r += 30) {
                ctx.beginPath();
                ctx.arc(cx, cy, r, 0, Math.PI * 2);
                ctx.strokeStyle = `rgba(201,168,76,${0.12 + (r / 120) * 0.2})`;
                ctx.lineWidth = 1;
                ctx.stroke();
            }
            for (let i = 0; i < 8; i++) {
                const a = angle + (i * Math.PI * 2) / 8;
                ctx.beginPath();
                ctx.moveTo(cx, cy);
                ctx.lineTo(cx + Math.cos(a) * 120, cy + Math.sin(a) * 120);
                ctx.strokeStyle = "rgba(201,168,76,0.15)";
                ctx.lineWidth = 1;
                ctx.stroke();
            }
            angle += 0.004;
            raf = requestAnimationFrame(draw);
        };
        draw();
        return () => cancelAnimationFrame(raf);
    });
</script>

<canvas bind:this={canvasEl} width={260} height={260} class="opacity-80" />
