<template>
  <div class="home">
    <SubmissionForm />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import SubmissionForm from "@/components/SubmissionForm.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    SubmissionForm,
  },
});
</script>
