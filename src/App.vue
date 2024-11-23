<template>
  <div class="min-h-screen bg-black text-red-500 flex flex-col">
    <!-- Header -->
    <header class="p-6 text-center">
      <h1
        class="text-2xl text-cyan-400 md:text-4xl font-mono tracking-wider mb-2"
      >
        V'S LIFEPATH
      </h1>
      <p class="text-red-400 text-sm md:text-base">
        SELECT V'S LIFEPATH. SOME EVENTS AND DIALOGUE OPTIONS IN THE GAME WILL
        BE DIFFERENT DEPENDING ON YOUR CHOICE.
      </p>
    </header>

    <!-- Main Content -->
    <main class="flex-1 flex flex-col items-center justify-center p-4 md:p-8">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-7xl w-full">
        <div
          v-for="path in lifePaths"
          :key="path.title"
          class="group relative cursor-pointer"
          @click="selectPath(path.title)"
        >
          <div
            :class="[
              'absolute inset-0 border-2 border-red-500/30 transform skew-x-2 transition-all duration-300',
              selectedPath === path.title
                ? 'border-cyan-400 border-4'
                : 'group-hover:border-red-500/70',
            ]"
          ></div>
          <div
            class="relative bg-gray-900 p-4 transform transition-all duration-300 hover:scale-105 h-full"
          >
            <div
              class="flip-card-inner"
              :class="{ 'is-flipped': path.isFlipped }"
            >
              <div class="flip-card-front">
                <h2 class="text-xl md:text-2xl font-mono mb-4">
                  {{ path.title }}
                </h2>
                <img
                  :src="path.image"
                  :alt="path.title"
                  class="w-full h-[300px] object-cover mb-4"
                />
                <p class="text-sm text-gray-400 font-mono">
                  {{ path.description }}
                </p>
              </div>
              <div class="flip-card-back">
                <h2 class="text-xl md:text-2xl font-mono mb-4">
                  {{ path.title }} - Background
                </h2>
                <p class="text-sm text-gray-400 font-mono">
                  {{ path.background }}
                </p>
              </div>
            </div>
            <button
              @click.stop="flipCard(path)"
              class="mt-4 px-3 py-1 bg-cyan-500/10 text-cyan-400 hover:bg-cyan-500/20 transition-colors duration-300"
            >
              {{ path.isFlipped ? "Show Front" : "Show Back" }}
            </button>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <footer
      class="p-6 flex justify-between items-center border-t border-red-500/20"
    >
      <div class="font-mono text-xs text-red-500/70">
        Night City Resident Database
      </div>
      <div class="flex gap-4">
        <button
          class="px-4 py-2 bg-cyan-500/10 text-cyan-400 hover:bg-cyan-500/20 transition-colors duration-300"
        >
          BACK
        </button>
        <button
          class="px-4 py-2 bg-red-500/10 text-red-400 hover:bg-red-500/20 transition-colors duration-300"
        >
          SELECT
        </button>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from "vue";

const lifePaths = ref([
  {
    title: "Nomad",
    image: "/placeholder-1.png?height=400&width=300",
    description:
      "Roam the Badlands, living by your own rules in a tight-knit nomad clan.",
    background:
      "As a Nomad, you've grown up in the Badlands, part of a nomadic clan that values family, loyalty, and freedom above all else. Your life has been one of constant movement, scavenging, and survival.",
    isFlipped: false,
  },
  {
    title: "Streetkid",
    image: "/placeholder-2.png?height=400&width=300",
    description:
      "Grow up on the streets, knowing every back alley and fixer in Night City.",
    background:
      "Born and raised in Night City's urban jungle, you've seen it all. From gang wars to corporate schemes, you've learned to survive by your wits and street smarts.",
    isFlipped: false,
  },
  {
    title: "Corpo",
    image: "/placeholder-3.png?height=400&width=300",
    description:
      "Climb the corporate ladder in the ruthless world of mega-corporations.",
    background:
      "You've spent your life climbing the ranks of a powerful corporation, navigating office politics and corporate espionage. The world of high finance and power plays is your natural habitat.",
    isFlipped: false,
  },
]);

const selectedPath = ref(null);

const selectPath = (path) => {
  selectedPath.value = path;
};

const flipCard = (path) => {
  path.isFlipped = !path.isFlipped;
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap");

:root {
  font-family: "Share Tech Mono", monospace;
}

/* Add some cyberpunk-style scan lines */
.bg-black::before {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(
    0deg,
    rgba(0, 0, 0, 0.15) 0px,
    rgba(0, 0, 0, 0.15) 1px,
    transparent 1px,
    transparent 2px
  );
  pointer-events: none;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.is-flipped {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}

.flip-card-back {
  transform: rotateY(180deg);
}
</style>
