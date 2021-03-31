<template>
<div class="d-flex justify-content-center">
   <div class="input-group" style="width: 200px; height: 50px;">
    <textarea
      class="form-control"
      aria-label="With textarea"
      style="resize: none;"
      v-model="current"
    >
    </textarea>
  </div>
</div>
</template>

<script>
export default {
  props: ["current"],
};
</script>