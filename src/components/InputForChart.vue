<script setup lang="ts">
import { ref, computed } from 'vue';



const textValue = ref('');
const emit = defineEmits(['data-submit']);

function inpuHandler(e: Event) {
  const { value } = e.target as HTMLTextAreaElement;
  textValue.value = value;
};

const computedTest = computed(() => csvToJson(textValue.value))


function csvToJson(csv: string) {
  csv = csv.replaceAll('"', '').replaceAll("'", '').trim()

  const [headers, ...rows] = csv.split('\n');
  const headersArr = headers.split(',');

  return rows.map((item) => {
    const items = item.split(',');

    return headersArr.reduce((acc, key, index) => {
      return {
        ...acc,
        [key]: items[index],
      };
    }, {});
  });
}
function submitHandler() {
  emit('data-submit', computedTest.value);
  textValue.value = '';
}



</script>

<template>

  <div>
    <textarea 
      @input="inpuHandler" 
      v-model="textValue"
      placeholder="expected format:
      header,header,header,
      111111,222222,333333,
      444444,555555,666666"
    ></textarea>
  </div>
  <button :disabled="!textValue" @click="submitHandler">Submit</button>

</template>

<style scoped>
textarea {
  resize: none;
  height: 100px;
  width: 500px;
}

button {
  background-color: antiquewhite;
}
</style>
