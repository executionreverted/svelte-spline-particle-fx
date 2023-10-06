<script>
    import { onMount } from "svelte";
    import { Application } from "@splinetool/runtime";
    let loading = true;
    let model;
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

        // I couldn't get it work as expected, without setTimeout.
        // I think its about spline, doing something in background and async variable updates cause spawn objects on old points.
        setTimeout(async () => {
            await app?.emitEvent("mouseDown", "BG");
        }, 50);
    };

    onMount(() => {
        const canvas = document.getElementById("canvas3d");
        if (!canvas) return;
        app = new Application(canvas);
        if (!app) return;
        app.load(url).then((splineScene) => {
            console.log("hello");
            model = splineScene;
            loading = false;
            console.log(loading);
        });

        document.addEventListener("click", onClick);
        return () => {
            document.removeEventListener("click", onClick);
        };
    });
</script>

<canvas id="canvas3d" />
<p>{loading ? "Loading Spline Scene..." : " "}</p>

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

    p {
        min-height: 14px;
        color: darkslateblue;
        text-align: center;
    }
</style>
