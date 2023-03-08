<script setup>
import { ref } from 'vue'
import { getMails } from './composable/getMails.js'
import SingleMail from './components/SingleMail.vue'
import BinaryPreview from './components/BinaryPreview.vue'
import MailSearch from './components/MailSearch.vue'
import IconSearch from './components/icons/IconSearch.vue'
const mails = ref(getMails())
// console.log(mails)
//4.create handler function
const selectedMails = ref([])
const addSelectedMail = (msg, e) => {
  console.log(e.mailId)
  console.log(e.eTarget)
  console.log(e.status)
  console.log(msg)
  selectedMails.value.push(e.mailId)
}
const selectedBinaryFile = ref('')
const chooseBinaryFile = (event) => {
  console.log(event.target)
  console.log(event.target.files)
  console.log(event.target.files[0])
  selectedBinaryFile.value = event.target.files[0]
}
</script>
<template>
  <div class="w-full p-3">
    <div>
      <MailSearch>
        <template #default>
          <IconSearch />
          <h1>Your Search:</h1>
          <input type="text" class="border border-gray-200" />
        </template>
        <template #header>
          <p class="text-2xl tracking-widest">SIT, KMUTT</p>
        </template>
      </MailSearch>
    </div>
    <div>
      <h1 class="flex justify-center text-2xl font-semibold">
        ~ Mailing List ~
      </h1>
    </div>
    <!-- 5. display selected mails -->
    <div>Selected Mails {{ selectedMails }}</div>
    <div class="w-full flex">
      <div class="flex w-2/12 justify-center tracking-widest font-semibold">
        Title
      </div>
      <div
        class="flex w-8/12 justify-self-center tracking-widest font-semibold"
      >
        Body
      </div>
      <div class="flex w-2/12 justify-center tracking-widest font-semibold">
        Keywords
      </div>
    </div>
    <div class="w-full flex" v-for="mail in mails" :key="mail.id">
      <!-- 3. put your custom event to component tag -->
      <SingleMail :mail="mail" @chooseMail="addSelectedMail('Done', $event)" />
    </div>
    <!-- <div class="grid grid-cols-8 gap-2">
      <div class="justify-self-center tracking-widest font-semibold">Title</div>
      <div class="col-span-6 justify-self-center tracking-widest font-semibold">
        Body
      </div>
      <div class="justify-self-center tracking-widest font-semibold">
        Keywords
      </div>
    </div>
    <div class="grid grid-cols-8 gap-2" v-for="mail in mails" :key="mail.id">
      <SingleMail
        :mail="mail"
        :layout="{ type: 'grid', colSpanNo: 2, colSpanValue: 6 }"
      />
    </div> -->
    <div>
      Choose your file:<input
        type="file"
        accept="image/*, .pdf"
        @change="chooseBinaryFile"
      />
      <BinaryPreview :selectedBinaryObject="selectedBinaryFile" />
    </div>
  </div>
</template>
<style scoped></style>
