<template>
  <AccountSetting @show-deactivate-modal="$emit('show-deactivate-modal')" />
</template>

<script setup>
import AccountSetting from "~/components/AccountSetting.vue";

defineEmits(["show-deactivate-modal"]);
</script>
