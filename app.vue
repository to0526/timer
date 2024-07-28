<script setup lang="ts">
const minute = ref(0);
const second = ref(0);
const count = ref(0);
const status = ref('');
let intervalId = '';
const onStartClick = (): void => {
  startTimer();
  status.value = 'running';
}
const onStopClick = (): void => {
  clearInterval(intervalId);
  status.value = 'stop';
}
const onResetClick = (): void => {
  minute.value = 0;
  second.value = 0;
  count.value = 0;
  status.value = '';
}
const startTimer = (): void => {
  intervalId = setInterval(
    (): void => {
      count.value += 1;
      if (count.value % 60 == 0) {
        second.value = 0;
        minute.value += 1;
      } else {
        second.value += 1;
      }
    },
    1000
  );
}
</script>

<template>
  <div>
    {{minute.toString().padStart(2, '0')}}:{{second.toString().padStart(2, '0')}}
    <br />
    <button v-on:click='onStartClick' v-if="status == ''">スタート</button>
    <button disabled v-else-if="status == 'running'">再開</button>
    <button v-on:click='onStartClick' v-else-if="status == 'stop'">再開</button>
    <br />
    <button disabled v-if="status == ''">ストップ</button>
    <button v-on:click='onStopClick' v-else-if="status == 'running'">ストップ</button>
    <button disabled v-if="status == 'stop'">ストップ</button>
    <br />
    <button disabled v-if="status == ''">リセット</button>
    <button disabled v-else-if="status == 'running'">リセット</button>
    <button v-on:click='onResetClick' v-if="status == 'stop'">リセット</button>
  </div>
</template>
