<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
.message-container {
  min-width: 250px;
  width: 20%; 
  margin-left: -125px; 
  background-color: #fafafa; 
  color: #444; 
  text-align: center; 
  border-radius: 2px; 
  padding: 16px; 
  position: fixed; 
  z-index: 1;
  left: 50%; 
  bottom: 30px;
  border-radius: 8px;
  border-left: 6px solid #ffcc00;
}
</style>