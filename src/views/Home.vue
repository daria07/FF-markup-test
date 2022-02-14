<template>
    <section class="section-main">
      <div class="container">
        <h1>Ваше налоговое резидентство1</h1>
        <div class="subtitle">Раскройте источник средств</div>
        <div class="signup-steps"> 
          <div class="signup-step step-finished"></div>
          <div class="signup-step step-finished"></div>
          <div class="signup-step"></div>
          <div class="signup-step"></div>
        </div>
        <form class="signup" id="form" v-on:submit.prevent="validate">
          <div class="signup-two"> 
            <select v-model="tax_resident" :class="{error: this.errors.welfare}" class="listup input-st"> 
                <option value="" disabled>Налоговое резидентство</option>
                <option value="1">Налоговое резидентство 1</option>
                <option value="2">Налоговое резидентство 2</option>
            </select>
            <div :class="{error: this.errors.welfare}" class="label-required"  v-if="this.errors.tax_resident">
              Поле обязательно для заполнения
            </div>

            <input class="input-st input" :disabled="us_tax_resident === 'yes' || dontknow" 
              @input="sliceInn"
              type="number" v-model="inn" placeholder="Индивидуальный номер налогоплательщика">
            <div class="label-required" v-if="this.errors.inn">Поле обязательно для заполнения</div>

            <label class="label-dontknow"> 
              <input v-model="dontknow" class="dontknow" type="checkbox">Я не помню свой номер налогоплательщика
            </label>

            <div class="signup-title">Являетесь ли Вы налоговым резидентом США?</div>
            <div class="answer">
              <input id="answer_yes" v-model="us_tax_resident" type="radio" value="yes">
              <label class="answer-item" for="answer_yes">Да</label>
              <input id="answer_no" v-model="us_tax_resident" type="radio" value="no">
              <label class="answer-item" for="answer_no">Нет</label>
              <div class="answer-comment" v-if="us_tax_resident === 'yes'">
                К сожалению, мы не можем открыть счет налоговому резиденту США.
              </div>
            </div>

            <div class="signup-comment">
              Попадаете ли Вы под категорию налогоплательщиков в Соединенных Штатах Америки по каким-либо другим причинам? 
              (например, обладатель двойного резидентства, владелец загородного дома/помещения, подача совместной декларации 
              о доходах с супругом и т.д.)
            </div>
            <div class="signup-title">Вы или Ваши родственники связаны с публичными политическими персонами?</div>
            <div class="answer">
              <input v-model="associated_public_political" class="hidden" id="answer_yes_polit" type="radio" name="associated_public_political" value="yes">
              <label class="answer-item" for="answer_yes_polit">Да</label>
              <input v-model="associated_public_political" class="hidden" id="answer_no_polit" type="radio" name="associated_public_political" value="no" checked="checked">
              <label class="answer-item" for="answer_no_polit">Нет</label>
            </div>
            <select v-model="welfare" :class="{error: this.errors.welfare}" class="listup input-st" id="welfare"> 
              <option disabled="disabled" value="">Размер благосостояния</option>
              <option value="1">Размер благосостояния 2</option>
            </select>
            <div v-if="this.errors.welfare" class="label-required">Поле обязательно для заполнения</div>

            <button class="btn-nextstep" type="submit">Продолжить</button>
          </div>
        </form>
      </div>
    </section>
</template>

<script>
export default {
  data() {
    return {
      tax_resident: '',
      inn: '',
      welfare: '',
      dontknow: false,
      us_tax_resident: 'no',
      associated_public_political: 'no',
      errors: {
        inn: false,
        tax_resident: false,
        welfare: false
      }
    }
  },
  methods: {
    validate()
    {
      this.errors.inn = this.us_tax_resident === 'no' && !this.dontknow && ('' + this.inn).length !== 12;
      this.errors.tax_resident = this.tax_resident === '';
      this.errors.welfare = this.welfare === '';
    },
    sliceInn()
    {
      if (('' + this.inn).length > 12) {
        this.inn = ('' + this.inn).slice(0, 12)
      }
    }
  }
}
</script>

<style lang="scss">

  .section-main {
    padding-top: 40px;
    padding-bottom: 140px; 
  }
  
  h1 {
    text-align: center;
    font-style: normal;
    font-weight: 500;
    font-size: 40px;
    line-height: 48px;
    margin-bottom: 20px;
    margin-top: 0;
  }
  
  .subtitle {
    text-align: center;
    font-size: 16px;
    line-height: 24px;
    margin-bottom: 20px; 
  }
  
  .signup-steps {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    margin-bottom: 20px; 
  }
  
  .signup-step {
    background: #E5E5E5;
    border-radius: 3px;
    width: 32px;
    height: 6px;
    margin-right: 24px; 

    &:last-child {
      margin-right: 0; 
    }
  }
  
  .step-finished {
    background: #72BF44; 
  }
  
  .signup {
    max-width: 600px;
    margin: 0 auto; 
  }
  
  .input-st {
    background: #FFFFFF;
    border: 1px solid #CCCCCC;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    border-radius: 3px;
    padding: 16px 14px;
    margin-top: 20px;
    line-height: 22px; 
    font-size: 16px;

    &.error {
      border: 1px solid #CC0E00;
    }
  }
    
  .label-required {
    font-size: 14px;
    line-height: 20px;
    color: #CC0E00;
    margin-top: 4px; 
  }
  
  .listup {
    position: relative;
    cursor: pointer;
    width: 100%;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    background-image: url(../assets/img/arrow-down.svg);
    background-repeat: no-repeat;
    background-position: 98% center;
    outline: none; 
  }
  
  .input {
    width: 100%; 
    &::-webkit-input-placeholder {
      color: #000000; 
    }
    &::-moz-placeholder {
      color: #000000; 
    }
    &::-ms-input-placeholder {
      color: #000000; 
    }
    &::-ms-input-placeholder {
      color: #000000; 
    }
    &::placeholder {
      color: #000000; 
    }
    &:disabled {
      cursor: no-drop;
      background: #F0F0F0;
      color: #999999; 

      &:disabled::-webkit-input-placeholder {
        color: #999999; 
      }
      &:disabled::-moz-placeholder {
        color: #999999; 
      }
      &:disabled:-ms-input-placeholder {
        color: #999999; 
      }
      &:disabled::-ms-input-placeholder {
        color: #999999; 
      }
      &:disabled::placeholder {
        color: #999999; 
      }
    }
  }

  .label-dontknow {
    font-size: 14px;
    line-height: 20px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    cursor: pointer;
    margin-top: 20px; 
  }
  
  .dontknow::before {
    content: '';
    background: #FFFFFF;
    border: 1px solid #CCCCCC;
    border-radius: 3px;
    margin-right: 15px;
    width: 24px;
    height: 24px;
    display: inline-block;
    cursor: pointer; 
  }
  
  .dontknow:checked::before {
    background-color: #72BF44;
    border: 1px solid #72BF44;
    background-image: url(../assets/img/check.svg);
    background-position: center;
    background-repeat: no-repeat; 
  }
  
  .signup-title {
    margin-top: 40px;
    margin-bottom: 10px;
    font-weight: 500;
    font-size: 20px;
    line-height: 24px; 
  }
  
  .btn-nextstep {
    background: #72BF44;
    border-radius: 3px;
    padding: 14px;
    width: 100%;
    font-size: 18px;
    line-height: 28px;
    color: #ffffff;
    margin-top: 40px; 
  }
  
  .answer {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;

    input[type=radio] {
      display: none;
    }
  }

  .answer-item {
    background: none;
    border-radius: 3px;
    padding: 13px 20px;
    margin-right: 10px;
    border: 1px solid #72BF44;
    cursor: pointer; 
  }
  
  input[type=radio]:checked + .answer-item {
    background: #72BF44;
    color: #ffffff; 
  }
  
  .answer-comment {
    font-size: 14px;
    line-height: 20px;
    color: #CC0E00; 
  }
  
  .signup-comment {
    background: #F2F2F2;
    padding: 20px;
    font-size: 14px;
    line-height: 20px; 
    margin-top: 10px;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
  input[type=number] {
    -moz-appearance:textfield;
  }

  @media(max-width: 640px) {
    
    h1 {
      font-size: 30px;
      line-height: 36px;
    }

    .signup-title {
      font-size: 18px;
      line-height: 22px;
    }

    .answer-comment {
      width: 100%;
      margin-top: 10px;
    }

    .answer {
      flex-wrap: wrap;
    }

  }

</style>
