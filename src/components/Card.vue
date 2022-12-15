<template>
  <div id="card">
    <div id="card-header">
      <slot name="header"></slot>
      <slot name="edit"></slot>
    </div>
    <div id="card-content">
      <slot></slot>
    </div>
    <div id="card-footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardComponent",
};
</script>

<style scoped>
#card {
  box-shadow: 0px 4px 8px 0px rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  padding: 5px;
  margin: 10px;
  min-width: 40%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
#card:hover {
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
}
</style>