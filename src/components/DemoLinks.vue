<template>
    <v-row justify="center">
        <v-col cols="2" class="text-right">
            <v-btn
                color="primary"
                prepend-icon="mdi-play-box-outline"
                :href="'https://minerender.github.io/' + name"
                target="_blank"
            >
                Demo
            </v-btn>
        </v-col>
        <v-col cols="2" class="text-left">
            <v-btn
                color="secondary"
                prepend-icon="mdi-code-braces"
                :href="'https://codesandbox.io/p/github/MineRender/' + name + '?file=%2Findex.ts'"
                target="_blank"
            >Edit</v-btn>
        </v-col>
    </v-row>
</template>
<script lang="ts" setup>
const props = defineProps<{
    name: string
}>()
</script>
