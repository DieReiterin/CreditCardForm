<template>
    <select v-if="selectType === 'month'" class="form__block-select"
    v-bind:class="{'focused': selectFocused === true}"
    @change="updateSelect"
    :value="selectValue"
    >
        <option value="">Month</option>       
        <option value="01">01</option>
        <option value="02">02</option>
        <option value="03">03</option>
        <option value="04">04</option>
        <option value="05">05</option>
        <option value="06">06</option>
        <option value="07">07</option>
        <option value="08">08</option>
        <option value="09">09</option>
        <option value="10">10</option>
        <option value="11">11</option>
        <option value="12">12</option>
    </select>
    <select v-if="selectType === 'year'" class="form__block-select"
    v-bind:class="{'focused': selectFocused === true}"
    @change="updateSelect"
    :value="selectValue"
    >
        <option value="">Year</option>
        <option value="2023">2023</option>
        <option value="2024">2024</option>
        <option value="2025">2025</option>
        <option value="2026">2026</option>
        <option value="2027">2027</option>
        <option value="2028">2028</option>
        <option value="2029">2029</option>
        <option value="2030">2030</option>
        <option value="2031">2031</option>
        <option value="2032">2032</option>
        <option value="2033">2033</option>
        <option value="2034">2034</option>
    </select>
</template>
<script>
export default {
    name: 'my-select',
    props: {
        selectType: {
            type: String,
            required: true,
        },
        selectFocused: {
            type: Boolean,
            default: false,            
        },
        selectValue: {
            type: String,
            required: true,          
        },
    },
    methods: {
        updateSelect(event) {
            this.$emit('updated', event.target.value);
        }
    },
}
</script>
<style scoped>
select {
    all: unset;
}
.form__block-select {
  width: 115px;
  height: 25px;
  padding: 12px 10px 8px;
  font-size: 16px;
  font-weight: 500;
  color: #1a3b5d;
  margin-right: 15px;
  border: 1px solid #ced6e0;
  border-radius: 5px;
  background: transparent;
  background-image: url("data:image/svg+xml;utf8,<svg fill='black' height='24' viewBox='0 0 24 24' width='24' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/><path d='M0 0h24v24H0z' fill='none'/></svg>");
  background-repeat: no-repeat;
  background-position-x: 100%;
  background-position-y: 10px;
  
}
.focused {
    border: 1px solid var(--main_color);
    box-shadow: 0px 0px 5px grey;
}
</style>