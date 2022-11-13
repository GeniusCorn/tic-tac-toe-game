<script setup lang="ts"></script>

<template>
  <div flex gap-4 justify-between text-xl>
    <a
      icon-btn
      href="https://geniuscorn-tic-tac-toe.netlify.app/"
      target="_blank"
      rel="noopener noreferrer"
    >
      <div i-tabler-network></div>
    </a>

    <a icon-btn href="mailto:hi@nicecorn.com">
      <div i-tabler-mail />
    </a>

    <a
      icon-btn
      rel="noreferrer"
      target="_blank"
      href="https://github.com/GeniusCorn/tic-tac-toe-game"
    >
      <div i-tabler-brand-github />
    </a>
  </div>

  <div text-xs text-slate-500>
    <span>
      Powered by
      <a text-slate-500 hover:opacity-50 href="https://github.com/GeniusCorn"
        >GeniusCorn
      </a></span
    >
  </div>
</template>

<style scoped></style>
