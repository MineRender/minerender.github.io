<style>
.skin-container {
    height: 400px;
}
</style>
<template>
    <div class="skin-container" ref="skinContainer"/>
</template>
<script lang="ts" setup>
import { AssetKey, AssetLoader, Models, Renderer, Skins, sleep } from "minerender";
import { Maybe } from "minerender/src/util/util";
import { Model } from "minerender/src/model/Model";
import { OrbitControls } from "minerender/src/three/OrbitControls";
import { onBeforeMount, onMounted, ref, watch } from "vue";

const props = defineProps<{
    skin: string,
    rotate: boolean,
    grid?: boolean
}>();

const skinContainer = ref<HTMLDivElement>();

let renderer: Renderer;
const recreate = async ()=>{
    await sleep(100 * Math.random());

    renderer = new Renderer({
        camera: {
            near: 1,
            far: 1000
        },
        render: {
            autoResize: true,
            stats: true,
            fpsLimit: 60,
            antialias: false
        },
        composer: {
            enabled: false
        },
        debug: {
            grid: props.grid,
            axes: props.grid
        }
    });

    skinContainer.value?.children[0]?.remove();
    renderer.appendTo(skinContainer.value!);

    const controls = new OrbitControls(renderer.camera, renderer.renderer.domElement);
    controls.enableZoom = false;
    renderer.registerEventDispatcher(controls);
    controls.update();

    controls.target.set(0, 10, 0);
    renderer.camera.lookAt(0, 10, 0);

    renderer.start();

    // TODO: this is meh
    setTimeout(() => {
        renderer.dirty = true;
    }, 100);

    const skin = await Skins.fromUuidOrUsername(props.skin);
    console.log(skin);
    const skinObject = await renderer.scene.addSkin(skin);

    setInterval(() => {
        if (props.rotate) {
            let r = skinObject.getRotation();
            r.y += 0.06;
            skinObject.setRotation(r);
        }
    }, 100);
}

onMounted(async () => {
    console.log("onMounted");
    recreate();
    watch(()=>props.grid,()=>{
        recreate();
    })
})

</script>
