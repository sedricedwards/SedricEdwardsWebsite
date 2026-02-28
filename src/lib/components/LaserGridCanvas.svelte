<script>
    import { onMount } from "svelte";
    let canvasEl;
    let raf;

    onMount(() => {
        const canvas = canvasEl;
        const ctx = canvas.getContext("2d");
        let x = 0;
        const COLS = 13,
            ROWS = 8;
        const cw = canvas.width / COLS,
            rh = canvas.height / ROWS;

        const draw = () => {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            for (let c = 0; c < COLS; c++) {
                for (let r = 0; r < ROWS; r++) {
                    const px = c * cw + cw / 2,
                        py = r * rh + rh / 2;
                    const dist = Math.abs(px - x);
                    const alpha = Math.max(0.05, 0.3 - dist / 80);
                    ctx.beginPath();
                    ctx.arc(px, py, 2, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(201,168,76,${alpha})`;
                    ctx.fill();
                }
            }
            const grad = ctx.createLinearGradient(x - 30, 0, x + 30, 0);
            grad.addColorStop(0, "rgba(201,168,76,0)");
            grad.addColorStop(0.5, "rgba(201,168,76,0.6)");
            grad.addColorStop(1, "rgba(201,168,76,0)");
            ctx.fillStyle = grad;
            ctx.fillRect(x - 30, 0, 60, canvas.height);
            x = (x + 1.2) % canvas.width;
            raf = requestAnimationFrame(draw);
        };
        draw();
        return () => cancelAnimationFrame(raf);
    });
</script>

<canvas
    bind:this={canvasEl}
    width={260}
    height={160}
    class="opacity-90 rounded-xl"
/>
