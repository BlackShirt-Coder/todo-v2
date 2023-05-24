<template>
  <input type="text" class="input-text"  v-focus @input="$emit('update:searchValue',$event.target.value)" placeholder="Search...">
  <i class="bi bi-x-lg pe-3" style="cursor: pointer;" @click="$emit('clearBtn')"></i>
</template>

<script>
const focus = {
  mounted: (el) => el.focus()
};
export default {
  name: "SearchTodo",
  emits:['clearBtn','searchValue'],
  props:['searchValue'],
  directives: {
    focus
  }

}
</script>

<style scoped>
.input-text {
  display: inline-block;
  width: 100%;
  border: none;
  outline: none;
  padding: 15px;
}
</style>