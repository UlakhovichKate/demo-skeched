<script>
export default {
  emits: ['add-message'],
  data() {
    return {
      message: ''
    }
  }
}
</script>

<template>
  <div class="message">
    <div class="message__note">Message (+£0.50) </div>
    <textarea class="message__text" rows="4" maxlength="500" v-model="message" @input="$parent.$emit('add-message', $event.target.value)"></textarea>
    <div class="message__note">(max 500 characters)</div>
    <div class="message__content"><pre>{{ message }}</pre></div>
  </div>
</template>

<style>
.message {
  text-align: left;
}

.message__text {
  width: 100%;
  padding: 10px;
  border: 1px solid #FFBD9B;
  color: black;
  transition: background-color 0.2s ease-out;
  resize: none;
}

.message__note {
  font-size: 12px;
}

.message__content {
  margin: 20px auto;
  text-align: center;
}

</style>
