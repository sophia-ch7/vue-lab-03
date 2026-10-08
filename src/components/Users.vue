<script setup lang="ts">
import { computed, ref } from "vue";
import UserCard from "@/components/UserCard.vue";
import usersData from "@/data/user.json";
import type { User } from "@/types/user";

type GenderFilter = "all" | "male" | "female";

const users: User[] = usersData;
const genderFilter = ref<GenderFilter>("all");

const filteredUsers = computed<User[]>(() => {
  if (genderFilter.value === "all") {
    return users;
  }
  return users.filter((user) => user.gender === genderFilter.value);
});
</script>

<template>
  <section class="users">
    <div class="users__toolbar">
      <button
        class="users__button"
        :class="{ 'users__button--active': genderFilter === 'all' }"
        @click="genderFilter = 'all'"
      >
        Всі
      </button>
      <button
        class="users__button"
        :class="{ 'users__button--active': genderFilter === 'male' }"
        @click="genderFilter = 'male'"
      >
        Чоловіки
      </button>
      <button
        class="users__button"
        :class="{ 'users__button--active': genderFilter === 'female' }"
        @click="genderFilter = 'female'"
      >
        Жінки
      </button>
    </div>

    <div v-if="filteredUsers.length" class="users__list">
      <UserCard v-for="user in filteredUsers" :key="user.id" :user="user" />
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

.users__toolbar {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 24px;
}

.users__button {
  padding: 8px 16px;
  border: 1px solid #1c2541;
  border-radius: 8px;
  background: #ffffff;
  color: #1c2541;
  font-size: 16px;
  cursor: pointer;
}

.users__button--active {
  background: #1c2541;
  color: #ffffff;
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
