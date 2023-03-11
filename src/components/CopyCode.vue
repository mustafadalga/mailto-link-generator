<script lang="ts" setup>
import { ref } from "vue";

const props = defineProps({
  title: {
    type: String,
    required: true
  },
  code: {
    type: String,
    required: true
  }
})

let timer: number | undefined;
const showAnimate = ref(false);


function copyCode() {
  if (timer) {
    window.clearTimeout(timer);
    showAnimate.value = false;
    timer = undefined;
  }

  showAnimate.value = true;
  navigator.clipboard.writeText(props.code);
  timer = window.setTimeout(() => showAnimate.value = false, 500);
}
</script>

<template>
    <div class="grid min-w-0">
      <label class="pl-5 text-sm text-gray-600">{{ title }}</label>
      <div
          class="flex items-center justify-between gap-3 px-4 py-2.5 rounded-full	bg-black/75 min-w-0">


        <p class="w-full text-white whitespace-nowrap overflow-hidden text-ellipsis text-xs lg:text-sm font-medium">
          {{ code }}
        </p>

        <button
            @click="copyCode"
            class="whitespace-nowrap bg-blue-500 rounded-full text-white text-xs lg:text-sm px-2 py-1 w-32">

          <span v-if="showAnimate">Copied!</span>
          <span v-else>Copy Code</span>
        </button>
      </div>
    </div>
</template>
