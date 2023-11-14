<style scoped>
</style>
<template>
    <div>
        <div ref="renderContainer" id="render-container"></div>
        <div ref="settingsPanel" id="settings-panel">
            <v-expansion-panels>
                <v-expansion-panel>
                    <v-expansion-panel-title>
                        <template v-slot:default="{ expanded }">
                            <v-row no-gutters>
                                <v-col cols="4" class="d-flex justify-start">
                                    Objects
                                </v-col>
                                <v-col
                                    cols="8"
                                    class="text-grey"
                                >
                                    <v-fade-transition leave-absolute>
                                    <span
                                        v-if="expanded"
                                        key="0"
                                    >
                                      Enter a name for the trip
                                    </span>
                                        <span
                                            v-else
                                            key="1"
                                        >
                                      {{ trip.name }}
                                    </span>
                                    </v-fade-transition>
                                </v-col>
                            </v-row>
                        </template>
                    </v-expansion-panel-title>
                    <v-expansion-panel-text>
                        <v-text-field
                            v-model="trip.name"
                            hide-details
                            placeholder="Caribbean Cruise"
                        ></v-text-field>
                    </v-expansion-panel-text>
                </v-expansion-panel>
            </v-expansion-panels>
        </div>
    </div>
</template>
<script lang="ts" setup>

import { ref } from "vue";

const renderContainer = ref<HTMLDivElement>();

</script>
