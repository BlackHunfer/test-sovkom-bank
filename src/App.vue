<template>
  <div id="app">
    <div class="search">
        <form v-on:submit.prevent="onSubmit">
          <div class="search__body">
            <div class="search__cont">
                <div class="search__cont__left" v-show="searchMode.value == false">
                    <div class="search__cont__item"
                      v-for="(field, index) in fields.slice(0, 3)"
                      :key="index"
                    >
                      <select-default v-model="field.value" :dataField="field"></select-default>
                    </div>
                </div>
                <div class="search__cont__left" v-show="searchMode.value == true">
                  <div class="search__cont__item">
                    <input-default v-model="fields[3].value" :dataField="fields[3]"></input-default>
                  </div>
                </div>
                <div class="search__cont__right">
                    <button type="submit">
                      <btn-default title="Найти" @submit="$emit('submit')"></btn-default>
                    </button>
                </div>
            </div>
            <div class="search__cont search__cont__hidden" 
              v-show="searchMode.value == false && priceSetting.active == true 
              || searchMode.value == false && footageSetting.active == true"
            >
              <div class="search__cont__hidden__left" v-show="priceSetting.active == true">
                <div class="search__cont__item">
                  <input-default v-model="fields[4].value" :dataField="fields[4]"></input-default>
                </div>
                <div class="search__cont__item">
                  <input-default v-model="fields[5].value" :dataField="fields[5]"></input-default>
                </div>
                <div class="search__cont__item">
                  <select-default v-model="fields[6].value" :dataField="fields[6]"></select-default>
                </div>
              </div>
              <div class="search__cont__hidden__left" v-show="priceSetting.active == false">
                <btn-border @click.native="addSetting(priceSetting)" title="Добавить цену"></btn-border>
              </div>
              <div class="search__cont__hidden__right" v-show="footageSetting.active == true">
                  <div class="search__cont__item">
                    <input-default v-model="fields[7].value" :dataField="fields[7]"></input-default>
                  </div>
                  <div class="search__cont__item">
                    <input-default v-model="fields[8].value" :dataField="fields[8]"></input-default>
                  </div>
                  <span class="input__default__group-text">м<sup>2</sup></span>
              </div>
              <div class="search__cont__hidden__right" v-show="footageSetting.active == false">
                <btn-border @click.native="addSetting(footageSetting)" title="Добавить метраж"></btn-border>
              </div>
            </div>
            <button type="submit" class="desktop-hidden">
              <btn-default title="Найти" @submit="$emit('submit')"></btn-default>
            </button>
          </div>
          <div class="search__footer">
                <div class="search__footer__left">
                  <switch-with-2-labels v-model="searchMode.value" :dataField="searchMode"></switch-with-2-labels>
                </div>
                <div class="search__footer__right" v-show="searchMode.value == false">
                  <plus-icon-with-label-btn v-model="priceSetting.active" :btn="priceSetting"></plus-icon-with-label-btn>
                  <plus-icon-with-label-btn v-model="footageSetting.active" :btn="footageSetting"></plus-icon-with-label-btn>
                </div>
          </div>
        </form>
    </div>
  </div>
</template>

<script>
import SelectDefault from './components/forms/SelectDefault'
import InputDefault from './components/forms/InputDefault'
import SwitchWith2Labels from './components/forms/SwitchWith2Labels'
import PlusIconWithLabelBtn from './components/btns/PlusIconWithLabelBtn'
import BtnDefault from './components/btns/BtnDefault'
import BtnBorder from './components/btns/BtnBorder'

export default {
  name: 'App',
  components: {
    SelectDefault,
    InputDefault,
    SwitchWith2Labels,
    PlusIconWithLabelBtn,
    BtnDefault,
    BtnBorder,
  },
  data() {
    return {
      searchMode: {
        value: false,
        variant1: {
          label: "Основной поиск",
          value: false
        },
        variant2: {
          label: "Искать по названию",
          value: true
        }
      },
      priceSetting: {
        label: "Цена",
        active: false
      },
      footageSetting: {
        label: "Метраж",
        active: false
      },
      fields: [
        {
          name: "city",
          value: "1",
          items: [
            {
              label: "Москва",
              value: "1",
            },
            {
              label: "Санкт-Петербург",
              value: "2",
            }
          ]
        },
        {
          name: "action",
          value: "1",
          items: [
            {
              label: "Купить",
              value: "1",
            },
            {
              label: "Арендовать",
              value: "2",
            }
          ]
        },
        {
          name: "object",
          value: "office",
          items: [
            {
              label: "Офис",
              value: "office",
            },
            {
              label: "Квартиру",
              value: "apartment"
            },
            {
              label: "Комната",
              value: "room"
            }
          ]
        },
        {
          name: "titleobject",
          value: "",
          placeholder: "Введите название объекта (бизнес-центра, торгового центра, новостройки, логопарка)",
        },
        {
          name: "pricefrom",
          value: "",
          type: "number",
          prefix: "От",
        },
        {
          name: "priceto",
          value: "",
          type: "number",
          prefix: "До",
        },
        {
          name: "priceсurrency",
          value: "1",
          items: [
            {
              label: "₽/месяц",
              value: "1",
            },
            {
              label: "$/месяц",
              value: "2",
            }
          ]
        },
        {
          name: "footagefrom",
          value: "",
          type: "number",
          prefix: "От",
        },
        {
          name: "footageto",
          value: "",
          type: "number",
          prefix: "До",
        },
      ]
    }
  },
  methods: {
    addSetting(setting){
      setting.active = true;
    },
    onSubmit(){
      let params = [];

      if(this.searchMode.value === true){

        let param = {};
        param.name = this.fields[3].name;
        param.value = this.fields[3].value;
        params.push(param);
            
      }else{

        this.fields.map((item, index) => {
          if(item.value != null && item.value != ''){

            if(this.priceSetting.active == false){
              if(item.name.indexOf("price") !== -1){
                return;
              }
            }
            if(this.footageSetting.active == false){
              if(item.name.indexOf("footage") !== -1){
                return;
              }
            }

            let param = {};
            param.name = item.name;
            param.value = item.value;

            params.push(param);
          }
        });

      }

      alert("Параметры формы собраны. Можно увидеть в консоли разработчика");
      console.log(params);
    }
  },
}
</script>

<style lang="less">
#app {
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}




.search{
  // width: 939px;
}

.search__body{
  padding: 30px 20px;
  background: linear-gradient(to right, #82b3e5, #a8d5e9);
}

.search__cont{
  display: flex;

  &:not(:first-child){
    margin-top: 25px;
  }
}

.search__footer{
  display: flex;
  justify-content: space-between;
  padding: 15px 20px;
  background-color: #e6f2fe;
}

.search__footer__right{
  display: flex;

  .btn__plus:not(:last-child){
    margin-right: 20px; 
  }
}

.search__cont__left{
  display: flex;
  width: 100%;

  .search__cont__item:first-child{
    border-top-left-radius: 3px;
    border-bottom-left-radius: 3px;
  }
}

.search__cont__right{
  flex: none;
  width: 130px;
  margin-left: auto;

  .btn__default{
    border-top-right-radius: 3px;
    border-bottom-right-radius: 3px;
  }
}

.search__cont__item{
  flex: 1;
  overflow: hidden;

  &:not(:last-child) select,
  &:not(:last-child) input{
    border-right: 1px solid #a3c6e8;
  }
}

.search__cont__hidden__left{
  display: flex;
  width: 62%;
  margin-right: 2%;

  .search__cont__item:first-child{
    border-top-left-radius: 3px;
    border-bottom-left-radius: 3px;
  }
  .search__cont__item:last-child{
    border-top-right-radius: 3px;
    border-bottom-right-radius: 3px;
  }
}
.search__cont__hidden__right{
  display: flex;
  width: 36%;

  .search__cont__item:first-child{
    border-top-left-radius: 3px;
    border-bottom-left-radius: 3px;
  }
  .search__cont__item:last-child{
    border-top-right-radius: 3px;
    border-bottom-right-radius: 3px;
  }

  .search__cont__item:nth-child(2){
    input{
      border-right: none;
    }
  }
}

.search__cont__hidden{
  select, input{
    background-color: #e6f2fe;
  }
}

.input__default__group-text{
  background-color: #c2e3f2;
  font-size: 18px;
  line-height: 35px;
  padding: 0 18px;
  border-top-right-radius: 3px;
  border-bottom-right-radius: 3px;
}

button[type='submit']{
  border: none;
  padding: 0;
  box-shadow: none;
  background-color: transparent;
  width: 100%;
  box-sizing: border-box;
}

.desktop-hidden{
  display: none;
}

@media (max-width: 767px){
  .search__body {
    padding: 20px 15px;
  }
  .search__footer{
    padding: 15px 15px;
  }
  .search__cont__left{
    flex-direction: column;
  }
  .search__cont__right{
    display: none;
  }

  .search__cont__left{
    .search__cont__item:not(:first-child){
      margin-top: 20px;
    }
  }

  .search__cont__hidden,
  .search__footer{
    flex-direction: column;
  }

  .search__cont__hidden__left {
    width: 100%;
    margin-right: 0;
  }

  .search__cont__hidden__right {
    margin-top: 20px;
    width: 100%;
  }

  .search__footer__right{
    margin-top: 20px;
  }
  .search__cont__left{
    .search__cont__item{
      border-radius: 3px;
      overflow: hidden;
    }
    select, input{
      border-right: 0 !important;
    }
  }

  .desktop-hidden{
    display: block;
    margin-top: 20px;
    border-radius: 3px;
    overflow: hidden;
  }
}

@media (max-width: 440px){
  .search__cont__hidden__left{
    flex-direction: column;

    .search__cont__item{
      border-radius: 3px;
    }

    .search__cont__item:not(:first-child){
      margin-top: 20px;
    }
  }
}

</style>
