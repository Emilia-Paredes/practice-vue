<template>
  <div class="inputTag">
    <div class="tags">
      <div class="tag" v-for="(tag, index) in tags" :key="index">
        {{ tag }}
        <i class="fa fa-times" @click="deleteTag(index)"></i>
      </div>
    </div>
    <input type="text" v-model="currentValue" @keydown="handlerKeyDown">
  </div>
</template>

<script lang="ts" setup>
import { Ref, ref } from 'vue';
let currentValue: Ref<string> = ref('')
let tags: Ref<Array<string>> = ref([])

const handlerKeyDown = (e: KeyboardEvent) => {
  if (e.key === 'Enter' && currentValue.value !== '') {
    tags.value.push(currentValue.value)
    currentValue.value = ''
  }
}
const deleteTag = (index: number) => {
  tags.value.splice(index, 1);
}

</script>

<style scoped>
.tags {
  display: flex;
  gap: 0.3rem;

  .tag {
    padding: 0.3rem;
    width: fit-content;
    border-radius: 0.3rem;
    background-color: bisque;

    i {
      padding-left: 0.5rem;
    }
  }
}

input {
  margin: 1rem 0;
}
</style>