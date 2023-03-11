<script setup lang="ts">
import { computed, ref } from "vue";
import type { IForm } from "@/types";
import GithubBadge from "@/components/GithubBadge.vue";
import CopyCode from "@/components/CopyCode.vue";
import Form from "@/components/Form.vue";


const form = ref<IForm>({
  to: "",
  cc: "",
  bcc: "",
  subject: "",
  body: ""
});
const showCopyCode = computed<boolean>(() => {
  return Object.values(form.value).some(input => input.length > 5)
})
const mailTo = computed<string>(() => {
  return `mailto:${form.value.to}?cc=${form.value.cc}&bcc=${form.value.bcc}&subject=${form.value.subject}&body=${form.value.body}`;
});

const htmlCode = computed<string>(() => {
  return `<a href="${mailTo.value}">Mail to</a>`;
})
</script>

<template>
  <div>
    <h1 class="px-6 py-5 text-center text-2xl	lg:text-3xl	font-medium">Mailto Link Generator</h1>
    <div class="w-full max-w-5xl mx-auto mt-10 px-6">
      <Form @input="form=$event"/>
    </div>

  </div>

  <div class="fixed bottom-6 inset-x-1/2	-translate-x-1/2 w-[calc(100%-3rem)] max-w-3xl grid gap-5">
    <CopyCode v-if="showCopyCode"
              title="Mailto link"
              :code="mailTo"/>
    <CopyCode v-if="showCopyCode"
              title="HTML code"
              :code="htmlCode"/>
  </div>
  <GithubBadge/>
</template>
