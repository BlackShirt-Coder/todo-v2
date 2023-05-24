<template>
  <i :class="{downBtn:allcompleted}" @click="$emit('completeAll')" class="bi bi-chevron-down ps-4 "></i>

  <input  type="text" @keyup.enter="$emit('addTodo')"  @input="$emit('update:bindValue',$event.target.value)" class="input-text"
         placeholder="What needs to be done?" autocomplete="off">
  <div class="me-5 search-icon">
    <i @click="$emit('searchToggle')" class="bi bi-search"></i>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  props:['allcompleted'],
 emits:['completeAll','addTodo','searchToggle','bindValue']
}
</script>

<style scoped>
.bi-chevron-down {
  color: #c2c2c2;
  font-weight: bolder;
  font-size: 25px;
}

.downBtn {
  color: #333333 !important;
  font-weight: bolder;
  font-size: 25px;

}

.input-text {
  display: inline-block;
  width: 100%;
  border: none;
  outline: none;
  padding: 15px;
}

</style>