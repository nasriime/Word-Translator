<template>
  <div class="text-center" id="app">
      <h1>Word Translator</h1>
      <h5>Powered by Vue.js</h5>
      <hr>
      <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
      <TranslateOutput v-text ="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'

export default {
  name: 'app',
  components:{
      TranslateForm,
      TranslateOutput
  },
  data:function(){
      return{
          translatedText : ''
      }
  },
  methods:{
      translateText:function(text,language){
          this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20170412T123101Z.b88938f2cba7bdd0.9a4255a93975175423d9bb1eecd154128808ff28&lang='+language+'&text='+text)
          .then((response)=>{
              this.translatedText = response.body.text[0];
          });
      }
  }
}
</script>

<style>
body {
    background: #fefefe;
}
</style>
