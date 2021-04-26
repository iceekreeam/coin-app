<template>
    <section>
        <base-card>
        <coin-form></coin-form>
        </base-card>
    </section>
</template>
<script>
import CoinForm from "../components/forms/CoinForm.vue";
export default {
    components:{CoinForm}
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.controls {
  display: flex;
  justify-content: space-between;
}
</style>