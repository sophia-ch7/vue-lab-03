<script setup lang="ts">
import { ref } from "vue";
import type { User } from "@/types/user";

defineProps<{
  user: User;
}>();

const isDetailsVisible = ref(false);
</script>

<template>
  <div
    class="user-card"
    :class="{
      'user-card--minor': user.dob.age < 18,
      'user-card--young': user.dob.age >= 18 && user.dob.age <= 30,
      'user-card--adult': user.dob.age >= 31 && user.dob.age <= 50,
      'user-card--senior': user.dob.age > 50,
    }"
  >
    <img
      class="user-card__photo"
      :src="user.picture"
      :alt="`${user.name.first} ${user.name.last}`"
    />
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
    <button class="user-card__toggle" @click="isDetailsVisible = !isDetailsVisible">
      About me
    </button>
    <p v-show="isDetailsVisible" class="user-card__details">
      {{ user.details }}
    </p>
  </div>
</template>

<style scoped>
.user-card {
  padding: 24px;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 4px 16px rgba(20, 30, 70, 0.12);
  color: #1c2541;
  font-family: Arial, sans-serif;
}

.user-card--minor {
  background: #fff3d6;
}

.user-card--young {
  background: #e3f6e8;
}

.user-card--adult {
  background: #e3edff;
}

.user-card--senior {
  background: #f1e5ff;
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

.user-card__toggle {
  width: 100%;
  margin-top: 16px;
  padding: 10px;
  border: none;
  border-radius: 8px;
  background: #1c2541;
  color: #ffffff;
  font-size: 16px;
  cursor: pointer;
}

.user-card__details {
  margin: 12px 0 0;
  color: #5c6784;
}
</style>
