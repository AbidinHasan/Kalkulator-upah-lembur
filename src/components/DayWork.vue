<style scoped>
.wrapper {
  --font-color-dark: #fdfdfd;
  --font-color-light: #343030;
  --bg-color: #1f2028;
  --main-color: #fbfbfb;
  position: relative;
  width: 219px;
  height: 36px;
  background-color: var(--bg-color);
  border: 2px solid var(--main-color);
  border-radius: 34px;
  display: flex;
  flex-direction: row;
  box-shadow: 4px 4px var(--main-color);
}

.option {
  width: 100px;
  height: 28px;
  position: relative;
  top: 4px;
  left: 10px;
}

.input {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  appearance: none;
  cursor: pointer;
}

.btn {
  width: 100%;
  height: 100%;
  background-color: var(--bg-color);
  border-radius: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.span {
  color: var(--font-color-dark);
}

.input:checked + .btn {
  background-color: var(--main-color);
}

.input:checked + .btn .span {
  color: var(--font-color-light);
}
</style>

<template>
  <div class="wrapper">
    <div class="option">
      <input
        class="input"
        type="radio"
        v-model="Day"
        name="btn"
        value="option1"
        checked
      />
      <div class="btn">
        <span class="span">5 Day Work</span>
      </div>
    </div>
    <div class="option">
      <input
        class="input"
        type="radio"
        v-model="Day"
        name="btn"
        value="option2"
      />
      <div class="btn">
        <span class="span">6 Day Work</span>
      </div>
    </div>
  </div>
</template>

<script setup>
const Day = defineModel();
</script>
