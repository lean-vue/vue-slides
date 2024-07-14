<script>
export default {
  props: {
    count: {
      type: Number,
      default: 0,
    },
  },
  data: function () { return {counter: this.count } }
}
</script>

<template>
  <div class="ml-4">
    <button class="border rounded px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-800" @click="counter++">
      Count is: {{ counter }}
    </button>
  </div>
</template>
