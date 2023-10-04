<template>
<form @submit.prevent class="form">

     <my-card :isFocused="isFocused" @cardfocusUpdated="focusUpdated"
     :cardNumber="cardNumber" 
     :cardholderText="cardholderText" 
     :expiryMonth="expiryMonth"
     :expiryYear="expiryYear"
     :cvvNumber="cvvNumber"
     >
    </my-card>
    
        <div class="form__row">
          <div class="form__block">
            <my-title>Card Number</my-title>
            <my-input 
            :inputText="cardNumber" 
            inputName="cardNumber" 
            @updated="cardNumberUpdated"
            @click="focusUpdated('number')"
            :inputFocused="isFocused === 'number'"
            ></my-input> 

          </div>
        </div>
        <div class="form__row">
          <div class="form__block">
            <my-title>Cardholder</my-title>
            <my-input 
            :inputText="cardholderText" 
            inputName="cardholder" 
            @updated="cardholderTextUpdated"
            @click="focusUpdated('cardholder')"
            :inputFocused="isFocused === 'cardholder'"
            ></my-input>
          </div>
        </div>
        <div class="form__row">
          <div class="form__block">
            <my-title>Expiry Date</my-title>
            <div class="form__block-wrapper">
              <div @click="focusUpdated('month')">
                <my-select 
                :selectFocused="isFocused === 'month'" 
                selectType="month" 
                :selectValue="expiryMonth"
                @updated="monthUpdated"
                ></my-select>
              </div> 
              <div @click="focusUpdated('year')">
                <my-select 
                :selectFocused="isFocused === 'year'" 
                selectType="year" 
                :selectValue="expiryYear"
                @updated="yearUpdated"
                ></my-select>  
              </div> 
            </div>
          </div>
          <div class="form__block">
            <my-title>CVV</my-title>
            <my-input 
            :inputText="cvvNumber" 
            inputName="cvvNumber" 
            @updated="cvvNumberUpdated"
            @click="focusUpdated('cvv')"
            :inputFocused="isFocused === 'cvv'"
            ></my-input>         
          </div>
        </div>        
        <div class="form__row">
            <my-button>Submit</my-button>
        </div>
        <my-button buttonType="github"
        @click="openInNewTab('https://github.com/DieReiterin?tab=repositories')"
        >See on Github</my-button>
    </form>
</template>
<script>
import MyCard from '@/components/MyCard.vue'
export default {
  components: {
    MyCard,
  },
  data() {
        return {
            cardNumber: '',
            cardholderText: '',
            expiryMonth: '',
            expiryYear: '',
            cvvNumber: '',
            isFocused: '',
          }
    },
    methods: { 
      openInNewTab(url) {
      window.open(url, '_blank', 'noreferrer');
      },  
      cardNumberUpdated(newValue) {
        this.cardNumber = newValue
      },
      cardholderTextUpdated(newValue) {
        this.cardholderText = newValue
      },
      cvvNumberUpdated(newValue) {
        this.cvvNumber = newValue
      },
      monthUpdated(newValue) {
        this.expiryMonth = newValue
      },
      yearUpdated(newValue) {
        this.expiryYear = newValue
      },
      focusUpdated(newVal) {
        this.isFocused = newVal;
      },
    },
}
</script>
<style scoped>
.form {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 560px;
  height: 570px;
  margin: 200px auto 50px;
  padding: 30px;
  padding-top: 170px;
  background-color: #fff;
  border-radius: 15px;
  box-shadow: 0px 0px 50px rgb(190, 190, 190);
}
.form__row {
  display: flex;
  justify-content: space-between;
  width: 500px;
  height: 70px;
}
.form__row:not(:last-child) {
  margin-bottom: 25px;  
}
.form__row:last-child {
  margin-top: 25px;
}

.form__block {
  display: flex;
  flex-direction: column;
  width: 100%;
  margin: 3px;
}
.form__block:nth-child(2n) { 
  margin-left: 30px;
  max-width: 130px;
}

.form__block-wrapper {
  width: 100%;
  height: 50px;
  display: flex;
}


</style>