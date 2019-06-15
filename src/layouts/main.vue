<template>
    <div class="container">
        <img src="../assets/logo.png">
        <ul>
          <li>
            <v-link href="/">Home</v-link>
            <v-link href="/about">About</v-link>
          </li>
        </ul>
    <slot></slot>
    </div>
</template>

<script>
    import vLink from '../components/vLink.vue';
    export default {
        data() {
            return {
            }
        },
        components: {
            vLink
        }
    }
</script>

<style scoped>
  .container {
    padding: 15px 30px;
    background: #f9f7f5;
  }
</style>
