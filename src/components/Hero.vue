<style>
h1, h2, h3 {
  font-weight: 400;
}

h1 {
  font-size: 4.2rem;
}

h2 {
  font-size: 2.28rem;
}

h3 {
  font-size: 1.64rem;
}
</style>
<template>
  <v-container class="text-center">
    <v-row justify="center">
      <v-col>
        <div>
          <picture draggable="false">
            <source type="image/svg+xml" srcset="@/assets/minerender.svg">
            <source type="image/webp" srcset="@/assets/minerender-x256.webp">
            <img src="@/assets/minerender-x256.png" draggable="false" width="256" height="256" alt="MineRender Logo">
          </picture>
        </div>
        <h1 class="text-indigo">MineRender</h1>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col>
        <h2>Quick, Easy, Interactive 3D/2D Renders of Minecraft</h2>
        <h3>Skins, Blocks, Items, GUIs and more</h3>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col>
        <v-btn href="#getting-started" color="blue">Get Started</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>
<script setup lang="ts">
</script>
