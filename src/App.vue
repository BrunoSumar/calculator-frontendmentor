<template>
    <div id="app" :class="themeName">
        <div id="main" >
            <div id="header">
                <span>calc</span>
                <div id="themes">
                    <span>THEME</span>
                    <div>
                        <div
                            v-for="t in [1,2,3]"
                            :class="{active: t==theme}"
                            v-on:click="changeTheme(t)"
                            :key="t"
                        >
                            <span >{{t}}</span>
                        </div>
                    </div>
                </div>
            </div>
            <div id="display"><span>{{ display_val }}</span></div>
            <div id="buttons">
                <Button
                    v-for="btn in btns"
                    :value="btn"
                    :key="btn"
                    :input="input"
                />
            </div>
        </div>
        <a href="https://github.com/BrunoSumar/calculator-frontendmentor">Repositório Github</a>
    </div>
</template>

<script>
 import Button from './components/Button.vue'

 export default {
     name: 'App',
     components: {
         Button,
     },
     data: function() {
         return {
             btns: [
                 7,     8,    9, 'Del',
                 4,     5,    6,   '+',
                 1,     2,    3,   '-',
                 '.',   0,  '/',   'X',
                 'Reset', '='
             ],
             display_val: '',
             theme: 1,
         }
     },
     computed: {
         themeName: function () {
             return ['normal', 'light', 'dark'][this.theme-1];
         }
     },
     methods: {
         input: function(val) {

             if(this.display_val === 'ERROR')
                 this.display_val = '';

             switch(val){
                 case '=':
                     try{
                         this.display_val = eval(this.display_val.split('').map(x => x === 'X' ? '*' : x).join('')).toString()
                     }
                     catch(e){
                         console.error(e);
                         this.display_val = 'ERROR';
                     }
                     break;
                 case 'Reset':
                     this.display_val = '';
                     break;
                 case 'Del':
                     this.display_val = this.display_val.slice(0, -1);
                     break;
                 default:
                     this.display_val = this.display_val.concat(val)
             }
         },
         changeTheme: function(val){
             this.theme = val;
         }
     }
 }
</script>

<style>
 #app{
     background: #3b4664;
     display: flex;
     justify-content: center;

     width: 100%;
     height: 100%;

     -webkit-font-smoothing: antialiased;
     -moz-osx-font-smoothing: grayscale;
     text-align: center;
     color: #2c3e50;
 }



 #main {
     width: 90%;
     height: 100%;
     min-width: 375px;
     max-width: 600px;

     display: flex;
     flex-direction: column;
     justify-content: center;
     color: white;

     font-family: 'Spartan';
     font-weight: 700;
 }

 #main > div {
     margin: .75rem 0;
 }

 #header {
     font-size: 2.1rem;
     display: flex;
     flex-direction: row;
     justify-content: space-between;
     /* align-items: end; */
     line-height: 1.7rem;
 }

 #themes {
     font-size: .8rem;
     display: flex;
     flex-direction: row;
     justify-content: space-between;
     /* font-weight: 600; */

     padding: .3rem;
 }

 #themes > div {
     background: #252c46;
     border-radius: 1rem;
     display: flex;
     flex-direction: row;
     justify-content: space-between;
     align-items: center;
     width: 3.9rem;
     padding: 0 .4rem;
     margin-left: 1rem;
     /* overflow: hidden; */
 }

 #themes > div > div {
     font-size: .8rem;
     border-radius: 2rem;
     width: 1rem;
     height: 1rem;
     display: inline-block;
     /* overflow: hidden; */
 }

 #themes > div > div > span {
     display: inline-block;
     transform: translateY(-2rem);
     height: 3rem;
     width: 1.1rem;
     cursor: pointer;
 }

 .active {
     background: #d53d32;
 }

 #display {
     background: hsl(224, 36%, 15%);
     border-radius: .8rem;
     font-size: 4rem;
     padding: 5%;
     text-align: right;
     direction: rtl;
     text-overflow: ellipsis;
     overflow-x: hidden;
     white-space: nowrap;
     line-height: 5rem;
     min-height: 5rem;

 }

 #display > span {
     direction: ltr;
     display: inline-block;
 }

 #buttons {
     padding: 5%;
     height: 55%;
     display: grid;
     grid-template-columns: auto auto auto auto;
     grid-gap: 5.8%;

     background: #252d44;
     border-radius: .8rem;
 }

 a {
     position: fixed;
     bottom: 1rem;
     left: 1rem;
     color: white;
 }

 @font-face {
     font-family: 'Spartan';
     src: url('/Spartan-VariableFont_wght.ttf');
 }

 /* Themes */

 /* Light */
 div.light {
     background: #e6e6e6 !important;
 }

 .light div, .light a{
     color: #353529 !important;
 }

 .light #buttons {
     background: #d3cdcd;
 }

 .light #display {
     background: #eeeeee;
 }

 .light #themes > div {
     background: #d3cdcd;
 }

 /* Dark */
 div.dark {
     background: #17062a !important;
 }

 .dark div {
     color: #ffe13e !important;
 }

 .dark #buttons {
     background: #1e0837;
 }

 .dark #display {
     background: #1e0836;
 }

 .dark #themes > div {
     background: #1e0837;
 }

 .dark div.active {
     background: #00e4d8 !important;
 }

</style>
