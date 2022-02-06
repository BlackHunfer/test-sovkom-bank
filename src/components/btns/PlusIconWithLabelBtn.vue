<template>
    <div :class="`btn__plus ${active}`" @click="swapActive(btn.active)">
        <div class="btn__plus__icon">
            <div class="btn__plus__icon__line1"></div>
            <div class="btn__plus__icon__line2"></div>
        </div>
        {{ btn.label }}
    </div>
</template>


<script>
    export default {
        name: 'PlusIconWithLabelBtn',
        model: {
            event: 'active'
        },
        props: ['btn'],
        computed: {
            active: function(){
                let activeClass = '';
                if(this.btn.active === true){
                    activeClass = "active";
                }
                return activeClass;
            },
        },
        methods: {
          swapActive(value){
            let active = value;
            if(value === true){
              active = false;
            }else{
              active = true;
            }
            this.$emit('active', active)
          }
        },
    }
</script>

<style lang="less">
.btn__plus{
  display: flex;
  align-items: center;
  font-size: 16px;
  color: #506981;
  transition: 0.3s all;
  cursor: pointer;

  &:hover{
    color: #384a5a;
  }
}

.btn__plus__icon{
  width: 18px;
  height: 18px;
  border: 2px solid #506981;
  border-radius: 100%;
  position: relative;
  margin-right: 9px;
}

.btn__plus__icon__line1{
  width: 2px;
  height: 10px;
  position: absolute;
  left: 50%;
  top: 50%;
  margin-left: -1px;
  margin-top: -5px;
  background-color: #506981;
  transform-origin: center;
  transition: 0.3s all;
}

.btn__plus__icon__line2{
  width: 10px;
  height: 2px;
  position: absolute;
  left: 50%;
  top: 50%;
  margin-left: -5px;
  margin-top: -1px;
  background-color: #506981;
  transform-origin: center;
  transition: 0.3s all;
}

.btn__plus.active{
  color: #88949f;

  .btn__plus__icon__line1{
    transform: rotate(45deg);
  }
  .btn__plus__icon__line2{
    transform: rotate(45deg);
  }
}


</style>