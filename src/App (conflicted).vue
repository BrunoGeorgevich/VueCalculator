<template>
  <div class="Calculator">
    <Display class="Display" :text="previous + operator.text + current"> </Display>
    <CustomButton @button-was-clicked="clear" number="C" isNumber=true disabled="{{isEmpty}}"></CustomButton>
    <CustomButton @button-was-clicked="sign" number="+/-" isNumber=true disabled="{{isEmpty}}"></CustomButton>
    <CustomButton @button-was-clicked="percent" number="%" isNumber=true disabled="{{isEmpty}}"></CustomButton>
    <CustomButton @button-was-clicked="divide"  number="/" isOperator=true disabled="{{operator.text !== '' || isEmpty}}"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="7"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="8"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="9"></CustomButton>
    <CustomButton @button-was-clicked="multiply" :class="{ Operator:true, DisabledButton:operator.text !== '' || isEmpty}" number="*"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="4"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="5"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="6"></CustomButton>
    <CustomButton @button-was-clicked="add" :class="{ Operator:true, DisabledButton:operator.text !== '' || isEmpty}" number="+"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="1"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="2"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number" number="3"></CustomButton>
    <CustomButton @button-was-clicked="minus" :class="{ Operator:true, DisabledButton:operator.text !== '' || isEmpty}" number="-"></CustomButton>
    <CustomButton @button-was-clicked="append" class="Number Zero" number="0"></CustomButton>
    <CustomButton @button-was-clicked="dot" :class="{ Number:true, DisabledButton:hasDot || isEmpty}" number="."></CustomButton>
    <CustomButton @button-was-clicked="equal" :class="{ Operator:true, DisabledButton:previous === '' || isEmpty}" number="="></CustomButton>
  </div>
</template>

<script>

  import CustomButton from "./components/CustomButton";
  import Display from "./components/Display";

  export default {
    components: {Display, CustomButton},
    data: function () {
      return {
        current:"",
        previous:"",
        operator: {
          text:"",
          execute:""
        }
      }
    },
    methods: {
      append: function (number) {
        this.current += String(number);
      }, 
      dot: function () {
        if (!this.hasDot && !this.isEmpty) this.current += '.';
      },
      clear: function () {
        this.current = "";
        this.previous = "";
        this.operator.text = "";
        this.operator.execute = "";
      },
      sign: function () {
        this.current = this.current.indexOf('-') === -1 ? '-' + String(this.current) : this.current.split('-')[1];
      },
      percent: function () {
        var a = parseFloat(this.current);
        this.clear();
        this.current = String(a/100);
      },
      operatorWasClicked: function() {
        this.previous = this.current;
        this.current = "";
      },
      divide: function () {
        this.operatorWasClicked();
        this.operator.text = "/";
        this.operator.execute = (a,b) => a/b;
      },
      multiply: function () {
        this.operatorWasClicked();
        this.operator.text = "*";
        this.operator.execute = (a,b) => a*b;
      },
      add: function () {
        this.operatorWasClicked();
        this.operator.text = "+";
        this.operator.execute = (a,b) => a+b;
      },
      minus: function () {
        this.operatorWasClicked();
        this.operator.text = "-";
        this.operator.execute = (a,b) => a-b;
      },
      equal: function () {
        var a = parseFloat(this.previous);
        var b = parseFloat(this.current);
        var operator = this.operator.execute;
        this.clear();
        this.current = String(operator(a,b));
      }
    },
    computed: {
      hasDot() {
        return this.current.indexOf('.') !== -1;
      },
      isEmpty() {
        return this.current.length === 0;
      }
    }
  }
</script>

<style>
  .Calculator {
    display: grid;
    grid-template-columns: 25% 25% 25% 25%;
    grid-template-rows: 16.666% 16.666% 16.666% 16.666% 16.666% 16.666%;
    background: #32d296;
    width: 300px;
    height: 400px;
    font-size: 20px;
  }

  .Display {
    display: inline-grid;
    grid-column-start: 1;
    grid-column-end: 5;
    width: 100%; height: 100%;
    background: #151515;
    color: white;
    text-align: right;
  }
</style>
