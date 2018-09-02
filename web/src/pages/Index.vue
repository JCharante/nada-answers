<template>
  <q-page>
    <div class="red row justify-center" id="banner">
      <div class="col-xs-12 text-white gt-sm">
        <h3 class="text-center">💩 Nada Answers</h3>
      </div>
      <div class="col-xs-12 col-md-7 text-white" id="pad-me-when-lt-md">
        <p>
          Welcome to Nada Answers...
        </p>
        <p>
          Do you need to ask a question? Are you looking for answers? Nada offers you a space to ask anything you want. However, before each question you must write a petition. If the answer is not what you expected, at least you make catharsis and ask again. Or you know, you stop procrastinating and get back to studying.
        </p>
      </div>
    </div>
    <div class="row justify-center items-center content-center" id="notbanner">
      <div class="col-xs-12 row justify-center">
        <div class="col-xs-12 col-md-7" v-if="answer.length > 0">
          <p>{{ answer }}</p>
        </div>
      </div>
      <div class="col-xs-12 col-md-7 row justify-center">
        <q-field style="width: 100%;">
          <q-input v-model="petition" float-label="Petition"/>
        </q-field>
      </div>
      <div class="col-xs-12 col-md-7 row justify-center">
        <div class="col-xs-10 col-md-10">
          <q-field>
            <q-input v-model="question" float-label="Question"/>
          </q-field>
        </div>
        <div class="col-xs-2 col-md-2 row justify-end items-center">
          <q-btn class="lt-md" icon="send" color="primary" flat @click="onSend()"/>
          <q-btn class="gt-sm" icon="send" color="primary" label="SEND" flat @click="onSend()"/>
        </div>
      </div>
    </div>
  </q-page>
</template>

<style lang="stylus" scoped>
#banner
  background-color: #a40000;
  width: 100%;

#banner div
  //padding-left: 16px;
  //padding-right: 16px;
  max-width: 90vw;

#notbanner div
  max-width: 90vw;

@media only screen and (max-width: 768px) {
  #pad-me-when-lt-md {
    padding-top: 16px;
  }
}
</style>

<script>
import {
  QField,
  QInput,
  QBtn
} from 'quasar'

export default {
  name: 'PageIndex',
  components: {
    QField,
    QInput,
    QBtn
  },
  methods: {
    genAnswer () {
      let responses = ['idk', 'that\'s a pretty weird question to ask', 'try again later', 'umm.. maybe you should go back to studying']
      let randomResponse = responses[Math.floor(Math.random() * responses.length)]
      return randomResponse
    },
    onSend () {
      this.answer = this.genAnswer()
    }
  },
  data () {
    return {
      petition: '',
      question: '',
      answer: ''
    }
  }
}
</script>
