<script>
    import { onMount } from "svelte";
    let canvasEl;
    let raf;

    onMount(() => {
        const canvas = canvasEl;
        const ctx = canvas.getContext("2d");
        let offset = 0;

        const draw = () => {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.beginPath();
            const cy = canvas.height / 2;
            for (let x = 0; x < canvas.width; x++) {
                const t = (x + offset) / 30;
                const phase = t % (2 * Math.PI);
                let y = cy;
                if (phase > 5.5 && phase < 5.7) y = cy - 60;
                else if (phase > 5.7 && phase < 5.9) y = cy + 20;
                else if (phase > 5.9 && phase < 6.1) y = cy - 40;
                else y = cy + Math.sin(t * 0.5) * 8;
                if (x === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            }
            const grad = ctx.createLinearGradient(0, 0, canvas.width, 0);
            grad.addColorStop(0, "rgba(201,168,76,0)");
            grad.addColorStop(0.3, "rgba(201,168,76,0.8)");
            grad.addColorStop(1, "rgba(201,168,76,0.8)");
            ctx.strokeStyle = grad;
            ctx.lineWidth = 2;
            ctx.stroke();
            offset += 1.5;
            raf = requestAnimationFrame(draw);
        };
        draw();
        return () => cancelAnimationFrame(raf);
    });
</script>

<canvas bind:this={canvasEl} width={260} height={120} class="opacity-90" />
