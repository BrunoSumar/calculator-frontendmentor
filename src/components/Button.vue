<template class="button">
    <input
        type="button"
        :value="value"
        :class="btn_type"
        v-on:click="input(value)"
    >
</template>

<script>

 export default {
     name: 'App',
     components: {
     },
     props: [ 'value', 'input'],
     computed: {
         btn_type: function() {
             switch(this.value){
                 case 0:
                 case 1:
                 case 2:
                 case 3:
                 case 4:
                 case 5:
                 case 6:
                 case 7:
                 case 8:
                 case 9:
                     return 'number';
                 case '=':
                     return 'equal';
                 case '+':
                     return 'plux';
                 case '-':
                     return 'minus';
                 case '.':
                     return 'dot';
                 case '/':
                     return 'div';
                 default:
                     return this.value;
             }
         },
     }

 }
</script>

<style scoped>
 input {
     font-size: 2.2rem;
     font-weight: 600;
     color: #424b5a;
     cursor: pointer;

     border: 0;
     border-radius: .7rem;
     box-shadow: 0 .3rem  #b2a295;
     /* box-sizing: border-box; */
 }

 input:active {
     box-shadow: unset;
     transform: translateY(.35rem)
 }

 .Reset {
     background-color: #647299;
     box-shadow: 0 .3rem  #424e74;
     color: white;

     grid-column-start: 1;
     grid-column-end: 3;

 }

 .Del {
     background-color: #647299;
     box-shadow: 0 .3rem  #424e74;
     color: white;
 }


 .equal {
     background-color: #d13f30;
     box-shadow: 0 .3rem  #8f2316;
     color: white;

     grid-column-start: 3;
     grid-column-end: 5;
 }

 /* Themes */

 /* Light */
 .light input {
     background: #e5e4e0;
     box-shadow: 0 .3rem #a79d91;
 }

 .light .equal {
     background: #c85401;
     box-shadow: 0 .3rem #893a02;
 }

 .light .Reset, .light .Del {
     background: #388187;
     box-shadow: 0 .3rem #1c6168;
 }

 /* Dark */
 .dark input {
     background: #331b4d;
     color: #ffe846;
     box-shadow: 0 .3rem #851c9d;
 }

 .dark .equal {
     background: #00decf;
     box-shadow: 0 .3rem #6df9f0;
     color: #002830;
 }

 .dark .Reset, .dark .Del {
     background: #56077c;
     box-shadow: 0 .3rem #bf16f5;
     color: #fefff8;
 }

</style>
