<script lang="ts" setup>
import type { PropType } from "vue";
import type { IForm } from "@/types";
import { computed, ref } from "vue";

const props = defineProps({
  form: {
    type: Object as PropType<IForm>,
    required: true
  }
})

let timer: number | undefined;
const showAnimate = ref(false);

const mailTo = computed<string>(() => {

  const template: string = `mailto:${props.form.to}?cc=${props.form.cc}&bcc${props.form.bcc}&subject=${props.form.subject}&body=${props.form.body}`;
  return template;

});

function copyCode() {
  if (timer) {
    window.clearTimeout(timer);
    showAnimate.value = false;
    timer = undefined;
  }

  showAnimate.value = true;
  navigator.clipboard.writeText(mailTo.value);
  timer = window.setTimeout(() => showAnimate.value = false, 500);
}
</script>

<template>
  <div
      class="fixed bottom-6 inset-x-1/2	-translate-x-1/2 -translate-y-1/2 w-[calc(100%-3rem)] max-w-3xl flex items-center justify-between gap-3 px-4 py-2.5 rounded-full	bg-black/75">

    <p class="w-full text-white whitespace-nowrap overflow-hidden text-ellipsis text-sm font-medium">
      {{ mailTo }}
    </p>

    <button
        @click="copyCode"
        class="whitespace-nowrap bg-blue-500 rounded-full text-white text-sm lg:text-base px-2 py-1 w-32">

      <span v-if="showAnimate">Copied!</span>
      <span v-else>Copy Code</span>
    </button>
  </div>
</template>
