<template>
  <div class="main">
    <FlatBtn @click="openModule = true">Открыть форму</FlatBtn>
    <teleport to="body">
      <MainForm
          v-if="openModule"
          @close="openModule = false"
      />
    </teleport>
  </div>
</template>
<script setup>
import { ref } from "vue";
import MainForm from "@/components/MainForm";
import FlatBtn from "@/components/buttons/FlatBtn";

const openModule = ref(false)
</script>
<style>
.main {
  padding: 20px 80px;
  box-shadow: 6px -6px 10px 2px rgba(34, 60, 80, 0.2);
  background-color: rgb(246, 242, 242);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}
</style>
