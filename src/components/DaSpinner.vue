<template>
  <div class="spinner">
    <div class="bounce1"/>
    <div class="bounce2"/>
    <div class="bounce3"/>
  </div>
</template>

<script>
export default {
  name: 'DaSpinner',
};
</script>
<style>
@keyframes sk-bouncedelay {
  0%, 80%, 100% {
    transform: scale(0);
  }
  40% {
    transform: scale(1.0);
  }
}
</style>
<style scoped>
.spinner {
  display: flex;
  width: 80px;
  height: 18px;
  flex-direction: row;
  justify-content: space-between;
  text-align: center;

  & > div {
    width: 18px;
    height: 18px;
    background-color: var(--color-comment);

    border-radius: 100%;
    display: inline-block;
    -webkit-animation: sk-bouncedelay 1.4s infinite ease-in-out both;
    animation: sk-bouncedelay 1.4s infinite ease-in-out both;
  }

  & .bounce1 {
    animation-delay: -0.32s;
  }

  & .bounce2 {
    animation-delay: -0.16s;
  }
}
</style>
