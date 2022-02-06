<template>
    <div class="select__default">
        <select
            v-on:input="$emit('value', $event.target.value)"
            :name="dataField.name"
            :required="dataField.required"
        >
            <option
            
                v-for="item in dataField.items"
                :key="item.value"
                :value="item.value"
                :selected="dataField.value == item.value ? true : false"
            >
                {{ item.label }}
            </option>
        </select>
    </div>
</template>


<script>
    export default {
        name: 'SelectDefault',
        model: {
            event: 'value'
        },
        props: ['dataField'],
    }
</script>

<style lang="less">
.select__default{
  position: relative;
  width: 100%;

  select{
    width: 100%;
    padding: 12px 40px 12px 18px;
    background-color: white;
    color: #333333;
    font-size: 18px;
    border: none;
    outline: none;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
  }

  &:after{
    content: "▼";
    color: #63758c;
    font-size: 12px;
    position: absolute;
    right: 18px;
    top: 50%;
    margin-top: -5.94px;
    z-index: 1;
    text-align: center;
    pointer-events: none;
    box-sizing: border-box;
  }
}
</style>