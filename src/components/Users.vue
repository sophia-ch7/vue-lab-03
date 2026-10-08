<script setup lang="ts">
import UserCard from "@/components/UserCard.vue";
import usersData from "@/data/user.json";
import type { User } from "@/types/user";

const users: User[] = usersData;
</script>

<template>
  <section class="users">
    <div v-if="users.length" class="users__list">
      <UserCard v-for="user in users" :key="user.id" :user="user" />
    </div>
    <p v-else class="users__empty">Список юзерів пустий</p>
  </section>
</template>

<style scoped>
.users {
  max-width: 1200px;
  padding: 24px;
  margin: 0 auto;
}

.users__list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 24px;
}

.users__empty {
  text-align: center;
  font-size: 20px;
}
</style>
