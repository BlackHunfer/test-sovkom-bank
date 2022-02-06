<template>
    <div class="switch__wtext">
        <input class="switch__input" id="switch" type="checkbox"
            v-on:change="$emit('value', $event.target.checked)"
            :checked="dataField.value"
        >
        <label for="switch" class="switch__wtext__label switch__wtext__label1">{{ dataField.variant1.label }}</label>
        <label for="switch" class="switch">
            <span class="slider"></span>
        </label>
        <label for="switch" class="switch__wtext__label switch__wtext__label2">{{ dataField.variant2.label }}</label>
    </div>
</template>


<script>
    export default {
        name: 'SwitchWith2Labels',
        model: {
            event: 'value'
        },
        props: ['dataField'],
    }
</script>

<style lang="less">
.switch__wtext{
  display: flex;
  align-items: center;
}

.switch__wtext__label.disabled{
  color: #adb9c4;
  border: none;
  cursor: default;
}

.switch__wtext__label{
  color: #506981;
  font-size: 16px;
  cursor: pointer;
  border-bottom: 1px dotted #506981;
  transition: 0.3s all;
}

.switch__wtext__label:not(.disabled):hover{
  color: #3c4f61;
  border-color: transparent;
}

.switch {
  position: relative;
  display: inline-block;
  width: 40px;
  height: 22px;
  margin-left: 11px;
  margin-right: 11px;
  flex: none;
}

.switch__input{
  opacity: 0;
  width: 0;
  height: 0;
  visibility: hidden;
  position: absolute;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #5e9969;
  border-radius: 34px;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 18px;
  width: 18px;
  left: 2px;
  bottom: 2px;
  background-color: white;
  border-radius: 50%;
  box-shadow: 0px 2px 3px 0px #00000042;
  -webkit-transition: .4s;
  transition: .4s;
}

.switch__input:checked ~ .switch .slider {
  background-color: #5e9969;
}

.switch__input:checked ~ .switch .slider:before {
  -webkit-transform: translateX(18px);
  -ms-transform: translateX(18px);
  transform: translateX(18px);
}

.switch__input:not(:checked) ~ .switch__wtext__label1{
  color: #adb9c4;
  border-color: transparent;
  cursor: default;
  pointer-events: none;
}

.switch__input:checked ~ .switch__wtext__label2{
  color: #adb9c4;
  border-color: transparent;
  cursor: default;
  pointer-events: none;
}

@media (max-width: 382px){
    .switch__wtext__label{
        font-size: 13px;
    }
    .switch {
        margin-left: 7px;
        margin-right: 7px;
    }
}
</style>