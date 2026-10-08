<script setup lang="ts">
import userData from "@/data/user.json";
import type { User } from "@/types/user";

const user: User = userData;
</script>

<template>
  <div class="user-card">
    <img class="user-card__photo" :src="user.picture" alt="Фото користувача" />
    <h2 class="user-card__name">
      {{ user.name.title }}. {{ user.name.first }} {{ user.name.last }}
    </h2>
    <p class="user-card__meta">
      {{ user.gender }}
      <span v-if="user.dob.age > 18">| {{ user.dob.age }} years</span>
    </p>
    <p class="user-card__line">
      {{ user.location.city }}, {{ user.location.state }}, {{ user.location.country }}
    </p>
    <p class="user-card__line">{{ user.email }}</p>
    <p class="user-card__line">{{ user.phone }}</p>
    <p class="user-card__line">{{ user.cell }}</p>
    <ul class="user-card__hobbies">
      <li v-for="hobby in user.hobbies" :key="hobby" class="user-card__hobby">
        {{ hobby }}
      </li>
    </ul>
  </div>
</template>

<style scoped>
.user-card {
  width: 320px;
  padding: 24px;
  margin: 24px auto;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 4px 16px rgba(20, 30, 70, 0.12);
  color: #1c2541;
  font-family: Arial, sans-serif;
}

.user-card__photo {
  width: 100%;
  border-radius: 12px;
}

.user-card__name {
  margin: 16px 0 8px;
  font-size: 24px;
}

.user-card__meta {
  margin: 0 0 12px;
  color: #5c6784;
  text-transform: capitalize;
}

.user-card__line {
  margin: 6px 0;
}

.user-card__hobbies {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  padding: 0;
  margin: 16px 0 0;
  list-style: none;
}

.user-card__hobby {
  padding: 4px 12px;
  background: #e8efff;
  color: #2a4ba0;
  border-radius: 999px;
  font-size: 14px;
}
</style>
