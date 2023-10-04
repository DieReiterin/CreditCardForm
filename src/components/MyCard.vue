<template>
  <transition name="cvv" mode="out-in">

    <div v-show="isFocused === 'cvv'" class="card card__cvv"
    >      
        <div class="cvv__upper"></div>
        <div class="cvv__center">
          <div class="cvv__center-spacer"></div>
          <div class="cvv__center-text">{{ cvvHandler(cvvNumber) }}</div>
          
        </div>
        <div class="cvv__bottom">
          <img class="card__img-paysys" :src="require('@/assets/' + getPaymentSystem(cardNumber) + '.png')" alt="payment system">          
        </div>    
      </div>


  </transition>
  <transition name="card" mode="out-in">
    
    <div v-show="isFocused !== 'cvv'" class="card"
    >
          <div class="card__row card__row-upper">
            <img class="card__img-chip" src="@/assets/chip.png" alt="card chip">
        <transition name="paysys" mode="out-in">
          <img class="card__img-paysys" 
          :key="getPaymentSystem(cardNumber)" 
          :src="require('@/assets/' + getPaymentSystem(cardNumber) + '.png')" 
          alt="payment system">
        </transition>
          </div>
          <div class="card__row card__row-center"
          :class="{
            'focused__elem': isFocused === 'number'
          }"
            @click="clicked('number')"
            >
            <div class="card__number-item">{{ cardNumberHandler(cardNumber, 1) }}</div>
            <div class="card__number-item">{{ cardNumberHandler(cardNumber, 2) }}</div>
            <div class="card__number-item">{{ cardNumberHandler(cardNumber, 3) }}</div>
            <div class="card__number-item">{{ cardNumberHandler(cardNumber, 4) }}</div>          
          </div>
          <div class="card__row card__row-bottom">
            <div class="card__block card__block-cardholder"
            :class="{
              'focused__elem': isFocused === 'cardholder'
            }"
            @click="clicked('cardholder')"
            >
              <span class="card__block-title">
                Cardholder
              </span>
              <span class="card__block-text">
                {{ cardholderHandler(cardholderText) }}
              </span>
            </div>
            <div class="card__block card__block-expires"
            :class="{
              'focused__elem': isFocused === 'month' || isFocused === 'year'
            }"
            @click="clicked('month')"
            >
            
              <span class="card__block-title">
                Expires
              </span>
              <span class="card__block-text">
                {{ monthHandler(expiryMonth) }}/{{ yearHandler(expiryYear) }}
              </span>
            </div>
          </div>
        </div>
  </transition>
</template>
<script>
export default {
    props: {
      isFocused: {
          type: String,
          required: true,
        },
      cardNumber: {
          type: String,
          required: true,
      },
      cardholderText: {
          type: String,
          required: true,
      },
      expiryMonth: {
          type: String,
          required: true,
      },
      expiryYear: {
          type: String,
          required: true,
      },
      cvvNumber: {
          type: String,
          required: true,
      },
    },
    methods: {
      clicked(newVal){
        this.$emit('cardfocusUpdated', newVal)
      },
      bgRandom() {
        return Math.random() < 0.25 ? '1' : Math.random() < 0.5 ? '2' : Math.random() < 0.75 ? '3' : '4'
      },
      cardNumberHandler(inserted, position) {  
        const longArr = [];
        const num = inserted.split(' ').join('');
        for (let n = 0; n < 4; n++) {
          longArr.push(num[n] ?? '#')
        }
        for (let n = 4; n < 12; n++) {
          longArr.push(num[n] ? '*' : '#') 
        }
        for (let n = 12; n < 16; n++) {
          longArr.push(num[n] ?? '#')
        }
        let longString = longArr.join('');
        return position === 1 ? longString.slice(0, 4) :
         position === 2 ? longString.slice(4, 8) :
          position === 3 ? longString.slice(8, 12) :
           longString.slice(12, 16)
      },
      cardholderHandler(text) {
        return text === '' ? 'Full Name' : text                
      },
      monthHandler(month) {
        return month === '' ? 'MM' : month
      },
      yearHandler(year) {
        return year === '' ? 'YY' : year.slice(2,4)
      },
      cvvHandler(cvv) {
        return cvv === '' ? '' : cvv.length === 1 ? '*' : cvv.length === 2 ? '**' : cvv.length === 3 ? '***' : '****'
      },
      getPaymentSystem(num) {
        return num.length < 4 ? 'visa' : 
        num.slice(0, 5) < '2000' ? 'unionpay' : 
        num.slice(0, 5) < '4000' ? 'mastercard' : 
        num.slice(0, 5) < '6000' ? 'dinersclub' : 
        num.slice(0, 5) < '8000' ? 'amex' : 
        num.slice(0, 5) < '9500' ? 'jcb' : 'visa'
      },
    },
  }
</script>
<style scoped>
.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  position: absolute;
  left: 12%;
  top: -25%;
  z-index: 1;
  width: 430px;
  height: 270px;
  padding: 25px 15px;
  border-radius: 15px;
  text-shadow: 7px 6px 10px rgba(14, 42, 90, 0.8);
  box-shadow: 0px 0px 50px grey;
  background: rgb(240, 255, 77) no-repeat center center / cover;
  background-image: url(@/assets/bg-4.png);
}
.card__row {
  display: flex;
  max-height: 50px;
}
.card__row:not(:last-child) {
  margin-bottom: 40px;
}
.card__row-upper, .card__row-bottom {
  justify-content: space-between;
  width: 100%;
}
.card__img-chip {
  max-width: 60px;
  max-height: 50px;
}
.card__img-paysys {
  max-width: 850px;
  max-height: 45px;
}
.card__row-center {
  width: 95%;
  font-size: 25px;
  font-weight: 500;
  color: #fff;
  letter-spacing: 4px;
  cursor: pointer;
  
}
.card__number-item {
  margin-left: 5px;
}
.card__number-item:not(:last-child) {
  margin-right: 30px;
}
.card__block {
  display: flex;
  flex-direction: column;
  color: #fff;
  cursor: pointer;
}
.card__block-cardholder {
  min-width: 90px;
}
.card__block-title {
  font-size: 13px;
  opacity: .7;
  margin-bottom: 7px;
}
.card__block-text {
  font-size: 18px;
  text-transform: uppercase;
}
.focused__elem {
  position: relative;
}
.focused__elem::after {
  position: absolute;
  left: -7px;
  top: -7px;
  z-index: -1;
  content: "";
  width: calc(100% + 10px);
  height: calc(100% + 10px);
  background-color: rgba(0, 0, 0, 0.5);
  border: 2px solid gray;
  border-radius: 5px;
}
.card__cvv {
  padding: 0;
  padding: 30px 0;

}
.cvv__upper {
  height: 50px;
  width: 100%;
  margin-bottom: 10px;
  background-color: #000;
}
.cvv__center {
  display: flex;
  height: 50px;
  width: 400px;
  background-color: #fff;
  border-radius: 8px;
} 
.cvv__center-spacer {
  flex-grow: 1;
  /* border: 2px solid #000; */
}
.cvv__center-text {
  padding: 9px;
  font-size: 20px;
  flex-shrink: 0;
  text-shadow: none
  /* border: 2px solid red; */
}
.cvv__bottom {
  height: 50px;
  /* width: 100%; */
  margin-left: auto;
  padding-right: 15px;
  background-color: transparent;
  /* border: 2px solid #fff; */
}


.paysys-enter-active {
  transition: all 2s ease;
}
.paysys-enter-from { 
  opacity: 0;
}
.paysys-enter-to {
  opacity: 1;
}

.cvv-enter-active,
.card-enter-active {
  transition: all .4s cubic-bezier(0, 0, .8, .9) .4s;
}
.cvv-leave-active,
.card-leave-active {
  transition: all .4s cubic-bezier(.9, .8, 0, 0);
}
.card-leave-to, .cvv-leave-to {
  transform: perspective(1000px) rotate3d(0, 0.5, 0, -90deg);
}
.card-enter-from, .cvv-enter-from {
  transform: perspective(1000px) rotate3d(0, 0.5, 0, 90deg);
}
</style>