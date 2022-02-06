<template>
    <div :class="`input__default__cont ${prefix}`">
        <span class="input__default__prefix" v-show="dataField.prefix">{{ dataField.prefix }}</span>
        <input 
            class="input__default" 
            :placeholder="dataField.placeholder"
            :name="dataField.name"
            :value="dataField.value"
            :type="dataField.type"
            :required="dataField.required"
            v-on:input="$emit('value', $event.target.value)"
        >
    </div>
</template>


<script>
    export default {
        name: 'InputDefault',
        model: {
            event: 'value'
        },
        props: ['dataField'],
        computed: {
            prefix: function(){
                let prefixClass = '';
                if(this.dataField.prefix){
                    prefixClass = "prefix";
                }
                return prefixClass;
            },
        },
    }
</script>

<style lang="less">
.input__default__cont{
  position: relative;
  width: 100%;
  display: inline-flex;

  &.prefix{
    .input__default{
      padding-left: 45px;
    }
  }
}

.input__default{
  width: 100%;
  padding: 12px 18px;
  background-color: white;
  color: #333333;
  font-size: 18px;
  line-height: 20px;
  border: none;
  outline: none;
  box-shadow: none;
  appearance: none;
  box-sizing: border-box;
}

.input__default__prefix{
  font-size: 18px;
  line-height: 20px;
  color: #98a3af;
  position: absolute;
  padding: 12px 18px;
}

.input__default::-webkit-input-placeholder { color: #798590; }
.input__default:-ms-input-placeholder { color: #798590; }
.input__default::-ms-input-placeholder { color: #798590; }
.input__default::placeholder { color: #798590; } 

.input__default::-webkit-outer-spin-button,
.input__default::-webkit-inner-spin-button {
    -webkit-appearance: none;
}
</style>