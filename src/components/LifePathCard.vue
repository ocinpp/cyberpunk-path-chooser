<template>
  <div
    class="group relative cursor-pointer min-h-[500px] md:min-h-[550px] focus:outline-none"
    @click="$emit('select', path.title)"
    @keydown.enter="$emit('select', path.title)"
    @keydown.space.prevent="$emit('select', path.title)"
    :tabindex="0"
    :aria-selected="isSelected"
    :aria-label="`Select ${path.title} lifepath`"
    role="option"
  >
    <div
      class="absolute inset-0 border-2 border-red-500/30 transform transition-all duration-300 group-focus-visible:scale-[1.05]"
      :class="[
        isSelected
          ? 'border-sky-400 border-3 scale-[1.02] group-hover:scale-[1.05]'
          : 'group-hover:border-red-500/70 group-hover:scale-[1.05] group-focus-visible:border-red-500/70',
      ]"
    ></div>
    <div
      class="relative bg-gray-900 p-4 transform transition-all duration-300 hover:scale-[1.01] md:hover:scale-[1.04] group-focus-visible:scale-[1.01] md:group-focus-visible:scale-[1.04] h-full"
    >
      <div class="flip-card h-full" :class="{ 'is-flipped': path.isFlipped }">
        <div class="flip-card-inner">
          <div class="flip-card-front text-left flex flex-col">
            <h2 class="text-xl md:text-2xl font-mono mb-4">{{ path.title }}</h2>
            <img
              :src="path.image"
              :alt="`${path.title} lifepath illustration`"
              class="w-full h-[320px] md:h-[400px] object-cover mb-4"
            />
            <p class="text-sm text-gray-400 font-mono flex-1">
              {{ path.description }}
            </p>
          </div>
          <div class="flip-card-back text-left">
            <h2 class="text-xl md:text-2xl font-mono mb-4">
              {{ path.title }} - Background
            </h2>
            <p class="text-sm text-gray-400 font-mono">{{ path.background }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  path: {
    type: Object,
    required: true,
  },
  isSelected: {
    type: Boolean,
    default: false,
  },
});

defineEmits(["select"]);
</script>

<style scoped>
.flip-card {
  perspective: 1000px;
  position: relative;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.is-flipped .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}

/* Firefox issue of having a line at the right */
.is-flipped .flip-card-front {
  transform: scale(0.99);
}

.flip-card-back {
  transform: rotateY(180deg);
  background-color: rgb(17, 24, 39);
  padding: 1rem;
}
</style>
