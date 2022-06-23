<template>
  <button type="submit" class="text-white text-xl border rounded p-2">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "SubmitButton",
  props: {
    text: {
      type: String,
      required: true,
    },
  },
};
</script>
