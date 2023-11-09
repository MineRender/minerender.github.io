<template>
    <Hero/>

    <v-divider class="my-4"/>

    <v-container>
        <v-row>
            <v-col v-for="n in randomSkins" :key="n" cols="4">
                <v-card>
                    <Skin :skin="n" :rotate="rotate"></Skin>
                    <v-card-subtitle>{{ n }}</v-card-subtitle>
                </v-card>
            </v-col>
        </v-row>
    </v-container>

    <v-divider class="my-4"/>

    <v-container>
        <v-row>
            <v-col v-for="n in randomBlocks" :key="n" cols="4">
                <v-card>
                    <Model :model="'block/' + n" :rotate="rotate"></Model>
                    <v-card-subtitle>{{ n }}</v-card-subtitle>
                </v-card>
            </v-col>
        </v-row>
    </v-container>

    <v-divider class="my-4"/>

    <v-container>
        <v-row>
            <v-col v-for="n in randomItems" :key="n" cols="4">
                <v-card>
                    <Model :model="'item/' + n" :rotate="rotate"></Model>
                    <v-card-subtitle>{{ n }}</v-card-subtitle>
                </v-card>
            </v-col>
        </v-row>
    </v-container>

    <v-container>
        <v-checkbox v-model="rotate" value="Rotate"></v-checkbox>
    </v-container>

</template>

<script lang="ts" setup>
import HelloWorld from '@/components/HelloWorld.vue'
import Skin from "@/components/Skin.vue";
import Hero from "@/components/Hero.vue";
import { ref } from "vue";
import Model from "@/components/Model.vue";

const randomSkins = ['inventivetalent', 'Plancke', '08bed5'];
const randomBlocks = ['stone', 'dirt', 'oak_stairs'];
const randomItems = ['diamond_axe', 'fishing_rod', 'ghast_spawn_egg'];

const rotate = ref<boolean>(true);

</script>
