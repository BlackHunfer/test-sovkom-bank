<template>
    <div class="btn__default">{{ title }}</div>
</template>


<script>
    export default {
        name: 'BtnDefault',
        props: ['title'],
    }
</script>

<style lang="less">
.btn__default{
  padding: 11px 30px;
  width: 100%;
  line-height: 22px;
  background-color: #5e9969;
  color: white;
  font-size: 20px;
  outline: none;
  border: none;
  box-shadow: none !important;
  transition: 0.3s all;
  text-align: center;
  cursor: pointer;
  box-sizing: border-box;

  &:hover{
    background-color: #46724e;
  }
}

</style>