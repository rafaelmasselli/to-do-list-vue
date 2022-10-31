<template>
  <div class="tasks-progress">
    <span class="progress-value">{{ progress }}%</span>
    <div class="progress-bar" :style="{ width: progress + '%' }"></div>
  </div>
</template>

<script>
export default {
  props: {
    progress: { type: Number, default: 0 },
  },
};
</script>

<style>
.tasks-progress {
  margin-top: 10px;
  position: relative;
  width: 40%;
  border: 1px solid #fff;
  color: #000;
  border-radius: 8px;
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.progress-bar {
  position: absolute;
  border-radius: 8px;
  height: 100%;
  background-color: rgb(161, 245, 165);
  align-self: flex-start;
}

.progress-value {
  z-index: 1;
  font-size: 1.5rem;
}
</style>
