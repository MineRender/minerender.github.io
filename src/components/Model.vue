<style scoped>
.model-container {
    height: 400px;
}
</style>
<template>
    <div class="model-container" ref="modelContainer"/>
</template>
<script lang="ts" setup>
import {AssetKey, AssetLoader, Models, Renderer, Skins, sleep, toRadians, toDegrees} from "minerender";
import {OrbitControls} from "minerender/src/three/OrbitControls";
import {onMounted, ref, watch} from "vue";

const props = defineProps<{
    model: string,
    rotate: boolean,
    grid?: boolean
}>();

const modelContainer = ref<HTMLDivElement>();

let renderer: Renderer;
const recreate = async () => {
    await sleep(100 * Math.random());

    console.log("onMounted");
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

    modelContainer.value?.children[0]?.remove();
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
    if (model) {
        const modelObject = await renderer.scene.addModel(model, {
            wireframe: props.grid,
            mergeMeshes: true,
            instanceMeshes: true
        });
        console.log(modelObject.options);

        setInterval(() => {
            if (props.rotate) {
                let r = modelObject.getRotation();
                r.y = (r.y + 0.1) % (Math.PI / 2);
                modelObject.setRotation(r);
            }
        }, 100);
    }

};

onMounted(() => {
    recreate();
    watch(() => props.grid, () => {
        console.log("hi")
        recreate();
    })
});

</script>
