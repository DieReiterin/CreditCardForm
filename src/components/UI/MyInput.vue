<template>
    <input
    ref="inputref"
    class="form__block-input" 
    :class="{'focused': inputFocused === true}"
    :type="inputName === 'cardholder' ? 'text' : 'tel'"
    :value="inputName === 'cardNumber' ? cardNumberSpacer(inputText) : inputText"
    :maxlength="inputName === 'cardNumber' ? '19' : inputName === 'cardholder' ? '25' : '4'"
    @input="updateInput" 
    >
</template>
<script>
export default {
    name: 'my-input',
    props: {
        inputName: {
            type: String,
            required: true,
        },
        inputText: {
            type: String,
            required: true,
        },
        inputFocused: {
            type: Boolean,
            default: false,
        },
    },
    methods: {
        updateInput(event) {
                this.$emit('updated', event.target.value);
        },
        cardNumberSpacer(num) {
            let result = ''
                for (let i in num) {
                    if (num.length > 4 && num[i] !== ' ' && i == 4) {
                        result += ' ' + num[i];
                    } else if (num.length > 9 && num[i] !== ' ' && i == 9) {
                        result += ' ' + num[i];
                    } else if (num.length > 14 && num[i] !== ' ' && i == 14) {
                        result += ' ' + num[i];
                    } else if (num.length < 20) {
                        result += num[i]
                    }
                }
            return result
            // return num
        }
    },
    watch: {
        inputFocused(val) {
            if(val === true) {
                this.$refs.inputref.focus()
            }
        }
    }
}
</script>
<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
input {
    all: unset;
}
.form__block-input {
    min-width: 100px;
    max-width: 100%; 
    max-height: 50px;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ced6e0;
    border-radius: 5px;
}
.focused {
    border: 1px solid var(--main_color);
    box-shadow: 0px 0px 5px grey;
}
</style>