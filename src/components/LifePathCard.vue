<template>
  <div
    class="group relative cursor-pointer min-h-[500px] md:min-h-[550px]"
    @click="$emit('select', path.title)"
  >
    <div
      :class="[
        'absolute inset-0 border-2 border-red-500/30 transform skew-x-2 transition-all duration-300',
        isSelected
          ? 'border-sky-400 border-4 skew-x-3'
          : 'group-hover:border-red-500/70',
      ]"
    ></div>
    <div
      class="relative bg-gray-900 p-4 transform transition-all duration-300 hover:scale-[1.02] md:hover:scale-105 h-full"
    >
      <div class="flip-card h-full" :class="{ 'is-flipped': path.isFlipped }">
        <div class="flip-card-inner">
          <div class="flip-card-front text-left flex flex-col">
            <h2 class="text-xl md:text-2xl font-mono mb-4">{{ path.title }}</h2>
            <img
              :src="path.image"
              :alt="path.title"
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

.flip-card-back {
  transform: rotateY(180deg);
  background-color: rgb(17, 24, 39);
  padding: 1rem;
}
</style>
