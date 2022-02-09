<template>
   <div class="-mb-50 border-b border-gray-200 dark:border-gray-700 mt-0">
   <div class="flex flex-wrap -mb-px">
  <button class="inline-block w-64 p-4 bg-">
    Fancy Quiz App
  </button>
  <button class="inline-block w-64 p-4 bg-">
    Counter: {{ numCorrect }}/{{ numTotal }}
  </button>
</div>
</div>
</template>
<script>
export default {
    props: ['numTotal', 'numCorrect']
}
</script>