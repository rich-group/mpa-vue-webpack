<template>
  <div class="flex">
    <p>
      <span>姓名: \{{ defaultUser.name }}</span>
      <span>年龄: \{{ defaultUser.age }}</span>
      <span>性别: \{{ defaultUser.sex }}</span>,
      <span>地址: \{{ defaultUser.address }}</span>
    </p>
    <div v-for="u in users">
      <p>
        <span>姓名: \{{ u.name }}</span>,
        <span>年龄: \{{ u.age }}</span>,
        <span>性别: \{{ u.sex }}</span>,
        <span>地址: \{{ u.address }}</span>
      </p>
    </div>
  </div>
</template>
{{#if ts}}
<script setup lang="ts">
import {ref } from 'vue';
import type { UserModel, User } from '@/apis/model/UserModel';
withDefaults(defineProps<{
  defaultUser: Object
}>(), {
  defaultUser: {}
})
const users = ref<User[]>([]);
$API.BFF.detail<UserModel>().then(res => {
  if (res.retCode === 20000) {
    users.value = res.data;
  }
});
</script>
{{else}}
<script setup>
import { ref } from 'vue';
defineProps({
  defaultUser: {
    type: Object,
    default: () => ({})
  }
})
const users = ref([]);
$API.BFF.detail().then(res => {
  if (res.retCode === 20000) {
    users.value = res.data;
  }
});
</script>
{{/if}}
