<template>
    <div class="btn__border">{{ title }}</div>
</template>


<script>
    export default {
        name: 'BtnBorder',
        props: ['title'],
    }
</script>

<style lang="less">
.btn__border{
  width: 100%;
  text-align: center;
  font-size: 18px;
  color: #506981;
  padding: 10px 30px;
  border: 1px solid #506981;
  border-radius: 3px;
  cursor: pointer;
  outline: none;
  transition: 0.3s all;
  box-sizing: border-box;

  &:hover{
    color: #303f4d;
    border-color: #303f4d;
  }
}
</style>