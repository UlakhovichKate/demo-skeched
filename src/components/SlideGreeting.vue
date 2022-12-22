<script>
export default {
  data() {
    return {
      greeting: ['', 'Happy Birthday', 'Happy New Year', 'Merry Christmas'],
      selected: ''
    }
  }
}
</script>

<template>
  <div class="c-form">
    <div class="c-form__input-group">
      <label for="greeting-text" class="c-form__label">Title</label>
      <select  id="greeting-text" name="greeting_phrase" class="c-form__select c-image-text__select" v-model="selected">
        <option v-for="(option, index) in greeting" :key="index">{{option}}</option>
      </select>
    </div>

    <div class="c-form__input-group">
      <label for="greeting-title" class="c-form__label">Custom Title</label>
      <div class="c-form__inputs">
        <textarea id="greeting-title" class="c-form__input" name="input-title" rows="4" maxlength="60" placeholder="Write your title (max 60 characters, max 2 lines)" autocomplete="off" v-model="selected"></textarea>
      </div>
    </div>
  </div>
</template>

<style>

.c-form__input-group {
  display: grid;
  grid-template-columns: 80px 1fr;
  align-items: center;
  margin-bottom: 12px;
  transition: background-color 0.2s ease-out;
}

.c-form__label {
  font-size: 12px;
  color: #ccc;
  padding: 15px 0;
}

.c-form__select {
   width: 100%;
   padding: 15px;
   border: 1px solid #FFBD9B;
   cursor: pointer;
 }

.c-form__input {
  padding: 10px;
  border: 1px solid #FFBD9B;
  color: black;
  width: 100%;
  transition: background-color 0.2s ease-out;
  resize: none;
}

.c-form__input::placeholder {
   transition: color 0.2s ease-out;
   color: #ccc;
 }

</style>
