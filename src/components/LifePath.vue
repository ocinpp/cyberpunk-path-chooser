<template>
  <div class="min-h-screen bg-black text-red-500 flex flex-col font-tech-mono">
    <!-- Header -->
    <header class="p-6 text-center">
      <h1 class="text-2xl text-cyan-400 md:text-4xl tracking-wider mb-2">
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
          class="relative flex flex-col gap-4"
        >
          <LifePathCard
            :path="path"
            :is-selected="selectedPath === path.title"
            @select="selectPath"
          />
          <button
            @click.stop="flipCard(path)"
            class="w-full px-3 py-1 bg-cyan-500/10 text-cyan-400 hover:bg-cyan-500/20 transition-colors duration-300"
          >
            {{ path.isFlipped ? "Show Front" : "Show Back" }}
          </button>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <footer
      class="p-6 flex justify-between items-center border-t border-red-500/20"
    >
      <div class="text-xs text-red-500/70">Night City Resident Database</div>
      <div class="flex gap-4">
        <button
          @click="resetSelection"
          class="px-4 py-2 bg-cyan-500/10 text-cyan-400 hover:bg-cyan-500/20 transition-colors duration-300"
        >
          BACK
        </button>
        <button
          :disabled="!selectedPath"
          @click="confirmSelection"
          :class="[
            'px-4 py-2 transition-colors duration-300',
            selectedPath
              ? 'bg-red-500/10 text-red-400 hover:bg-red-500/20'
              : 'bg-gray-500/10 text-gray-400 cursor-not-allowed',
          ]"
        >
          SELECT
        </button>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from "vue";
import LifePathCard from "./LifePathCard.vue";

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

const resetSelection = () => {
  selectedPath.value = null;
  lifePaths.value.forEach((path) => (path.isFlipped = false));
};

const confirmSelection = () => {
  if (selectedPath.value) {
    console.log(`Selected path: ${selectedPath.value}`);
    // Add your confirmation logic here
  }
};

const flipCard = (path) => {
  path.isFlipped = !path.isFlipped;
};
</script>

<style>
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
  z-index: 1;
}

/* Font face declaration */
@font-face {
  font-family: "Share Tech Mono";
  font-display: swap;
}

.font-tech-mono {
  font-family: "Share Tech Mono", monospace;
}
</style>
