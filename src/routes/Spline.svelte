<script>
    import { onMount } from "svelte";
    import { Application } from "@splinetool/runtime";
    let model;
    // @ts-ignore
    let app;
    let url = "https://prod.spline.design/6kU7G9ercAASvqGU/scene.splinecode";
    // import spline scene
    const onClick = async (e) => {
        const x = e.x;
        const y = e.y;
        const centerX = window.innerWidth / 2;
        const centerY = window.innerHeight / 2;

        const mousePosX = x - centerX;
        const mousePosY = centerY - y;
        await app?.setVariables({ SpawnX: mousePosX, SpawnY: mousePosY });
        console.log("set variables", mousePosX, mousePosY);
        setTimeout(async () => {
            await app?.emitEvent("mouseDown", "BG");
        }, 50);
    };

    onMount(() => {
        const canvas = document.getElementById("canvas3d");
        if (!canvas) return;
        // @ts-ignore
        app = new Application(canvas);
        if (!app) return;
        app.load(
            url,
            // @ts-ignore
            (splineScene) => {
                model = splineScene;
            }
        );

        console.log(app.emitEvent);
        document.addEventListener("click", onClick);

        return () => {
            document.removeEventListener("click", onClick);
        };
    });
</script>

<canvas id="canvas3d" />

<style>
    #canvas3d {
        width: 100vw;
        height: 100vh;
        position: fixed;
        top: 0;
        left: 0;
        background: transparent;
        pointer-events: none;
    }
</style>
