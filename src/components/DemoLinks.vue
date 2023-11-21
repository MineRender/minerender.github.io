<template>
    <v-row justify="center" class="text-center">
        <v-col cols="1">
            <v-btn :href="'https://minerender.github.io/' + name" target="_blank">Demo</v-btn>
        </v-col>
        <v-col cols="1">
            <v-btn :href="'https://codesandbox.io/p/github/MineRender/' + name" target="_blank">CodeSandbox</v-btn>
        </v-col>
    </v-row>
</template>
<script lang="ts" setup>
const props = defineProps<{
    name: string
}>()
</script>
