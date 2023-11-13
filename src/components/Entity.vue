<style scoped>
.entity-container {
    height: 400px;
}
</style>
<template>
    <div class="entity-container" ref="entityContainer"/>
</template>
<script lang="ts" setup>
import { AssetKey, AssetLoader, Entities, Models, Renderer, Skins, sleep, toRadians } from "minerender";
import { OrbitControls } from "minerender/src/three/OrbitControls";
import { onMounted, ref, watch } from "vue";

const props = defineProps<{
    entity: string,
    rotate: boolean,
    grid?: boolean
}>();

const entityContainer = ref<HTMLDivElement>();

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

    entityContainer.value?.children[0]?.remove();
    renderer.appendTo(entityContainer.value!);

    const controls = new OrbitControls(renderer.camera, renderer.renderer.domElement);
    controls.enableZoom = false;
    renderer.registerEventDispatcher(controls);
    controls.update();

    renderer.start();

    // TODO: this is meh
    setTimeout(() => {
        renderer.dirty = true;
    }, 100);

    const entity = await Entities.getEntity(AssetKey.parse("entities", props.entity));
    const entityObject = await renderer.scene.addEntity(entity);

    // setInterval(() => {
    //     if (props.rotate) {
    //         let r = modelObject.getRotation();
    //         console.log(r)
    //         r.y += 0.1;
    //         modelObject.setRotation(r);
    //     }
    // }, 500);
};

onMounted(() => {
    recreate();
    watch(() => props.grid, () => {
        console.log("hi")
        recreate();
    })
});

</script>
