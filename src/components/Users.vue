<script setup lang="ts">
import userData from "@/data/user.json";
import type { User } from "@/types/user";

const user: User = userData;
</script>

<template>
  <div class="user-card">
    <img :src="user.picture" alt="Фото користувача" />
    <h2>{{ user.name.title }}. {{ user.name.first }} {{ user.name.last }}</h2>
    <p>{{ user.gender }}</p>
    <p>{{ user.dob.age }} years</p>
    <p>{{ user.location.city }}, {{ user.location.state }}, {{ user.location.country }}</p>
    <p>{{ user.email }}</p>
    <p>{{ user.phone }}</p>
    <p>{{ user.cell }}</p>
  </div>
</template>
