<script lang="ts" setup>
import { ref, watch } from "vue";
import type { IForm } from "@/types";

const form = ref<IForm>({
  to: "",
  cc: "",
  bcc: "",
  subject: "",
  body: ""
});
const showCcInput = ref(false);
const showBccInput = ref(false);
const watchOptions: { immediate: boolean } = {
  immediate: true
}
const emit = defineEmits([ "input" ]);

watch(() => form.value, () => {
  emit("input", form.value)
}, watchOptions)
</script>

<template>
  <div class="grid gap-4 rounded-lg bg-white shadow-[0_0px_10px_0px_rgba(0,0,0,0.2)]">

    <div class="px-5 py-4 border-b border-solid border-gray-200">
      <label>New Message</label>
    </div>

    <div class="px-5 grid gap-2">
      <div class="flex items-center justify-between gap-2">
        <div class="flex items-center gap-2 w-full">
          <label for="to" class="text-xs lg:text-sm font-medium text-gray-500">To</label>
          <input type="text"
                 v-model="form.to"
                 id="to"
                 class="w-full px-2 py-1 outline-0 text-xs lg:text-sm"/>
        </div>

        <div class="flex gap-2">
          <button type="button"
                  @click="showCcInput=!showCcInput"
                  class="text-xs lg:text-sm font-medium text-gray-500 hover:underline transition-all">Cc
          </button>
          <button type="button"
                  @click="showBccInput=!showBccInput"
                  class="text-xs lg:text-sm font-medium text-gray-500  hover:underline transition-all">Bcc
          </button>
        </div>

      </div>

      <div v-if="showCcInput" class="flex items-center gap-2">
        <label for="cc" class="text-xs lg:text-sm font-medium text-gray-500">Cc</label>
        <input type="text"
               v-model="form.cc"
               id="cc"
               class="w-full px-2 py-1 outline-0 text-xs lg:text-sm"/>
      </div>

      <div v-if="showBccInput" class="flex items-center gap-2">
        <label for="bcc" class="text-xs lg:text-sm font-medium text-gray-500">Bcc</label>
        <input type="text"
               v-model="form.bcc"
               id="bcc"
               class="w-full px-2 py-1 outline-0 text-xs lg:text-sm"/>
      </div>

      <div class="flex items-center gap-2">
        <label for="subject" class="text-xs lg:text-sm font-medium text-gray-500">Subject</label>
        <input type="text"
               v-model="form.subject"
               id="subject"
               class="w-full px-2 py-1 outline-0 text-xs lg:text-sm"/>
      </div>
    </div>

    <div class="grid gap-4 px-5 py-4  border-t border-solid border-gray-200">
      <label for="body" class="text-xs lg:text-sm font-medium text-gray-500">Body</label>
      <textarea id="body"
                v-model="form.body"
                type="text"
                class="resize-none w-full h-48 pr-2 py-1 outline-0 text-xs lg:text-sm"></textarea>
    </div>
  </div>
</template>
