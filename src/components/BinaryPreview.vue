<script setup>
import { computed, ref } from 'vue'
const props = defineProps({ selectedBinaryObject: [String, Object] })
console.log(props.selectedBinaryObject)
const currentBinaryObject = computed(() => {
  return props.selectedBinaryObject.name
})
const previewSrc = ref('')
const previewImage = () => {
  const reader = new FileReader()
  reader.addEventListener(
    'load',
    () => {
      // convert image file to base64 tring
      previewSrc.value = reader.result
    },
    false
  )
  if (props.selectedBinaryObject) {
    reader.readAsDataURL(props.selectedBinaryObject)
  }
}
const previewDoc = () => {
  previewSrc.value = URL.createObjectURL(props.selectedBinaryObject)
}
const isDoc = ref(false)
const canPreview = computed(() => {
  if (typeof props.selectedBinaryObject === 'object') {
    if (props.selectedBinaryObject.name.endsWith('pdf')) {
      previewDoc()
      isDoc.value = true
    } else {
      previewImage()
      isDoc.value = false
    }
    return true
  } else return false
})
</script>
<template>
  <div>Current Binary Object: {{ currentBinaryObject }}</div>
  <img :src="previewSrc" class="w-56 h-56" v-if="canPreview && !isDoc" />
  <a
    :href="previewSrc"
    target="_blank"
    v-if="canPreview && isDoc"
    class="text-purple-500"
    >{{ currentBinaryObject }}</a
  >
</template>
<style scoped></style>
