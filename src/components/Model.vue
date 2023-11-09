<style>
.model-container {
    height: 400px;
}
</style>
<template>
    <div class="model-container" ref="modelContainer"/>
</template>
<script lang="ts" setup>
import { AssetKey, AssetLoader, Models, Renderer, Skins, toRadians } from "minerender";
import { Maybe } from "minerender/src/util/util";
import { Model } from "minerender/src/model/Model";
import { OrbitControls } from "minerender/src/three/OrbitControls";
import { onBeforeMount, onMounted, ref } from "vue";

const props = defineProps<{
    model: string,
    rotate: boolean
}>();

const modelContainer = ref<HTMLDivElement>();

let renderer: Renderer;
onBeforeMount(() => {
    console.log("onBeforeMount")
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
            grid: true,
            axes: true
        }
    });
})

onMounted(async () => {
    console.log("onMounted");
    renderer.appendTo(modelContainer.value!);

    const controls = new OrbitControls(renderer.camera, renderer.renderer.domElement);
    controls.enableZoom = false;
    renderer.registerEventDispatcher(controls);
    controls.update();

    renderer.start();

    // TODO: this is meh
    setTimeout(() => {
        renderer.dirty = true;
    }, 100);

    const model = await Models.getMerged(AssetKey.parse("models", props.model));
    const modelObject = await renderer.scene.addModel(model, {
        wireframe: true,
        mergeMeshes: true,
        instanceMeshes: true
    });
    console.log(modelObject.options);

    // setInterval(() => {
    //     if (props.rotate) {
    //         let r = modelObject.getRotation();
    //         console.log(r)
    //         r.y += 0.1;
    //         modelObject.setRotation(r);
    //     }
    // }, 500);
})

</script>
