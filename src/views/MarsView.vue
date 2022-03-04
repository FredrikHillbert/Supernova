<template>
  <div class="about">
    <h1>Latest Weather From Mars </h1>
      <MarsPage></MarsPage>
  </div>
</template>


<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import MarsPage from '@/components/MarsPage.vue'; // @ is an alias to /src

@Component({
  components: {
    MarsPage,
  },
})
export default class MarsView extends Vue {}
</script>