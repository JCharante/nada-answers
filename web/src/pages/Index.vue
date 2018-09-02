<template>
  <q-page>
    <div class="red" id="banner" style="max-width: 100%">
      <div class="row" style="width: 600px; margin: 0 auto; padding: 24px;">
        <div class="col-12 text-white" style="width: 100%">
          <h3 class="text-center">💩 Nada Answers</h3>
        </div>
        <div class="col-12 text-white">
          <p>
            Welcome to Nada Answers...
          </p>
          <p>
            Do you need to ask a question? Are you looking for answers? Nada offers you a space to ask anything you want. However, before each question you must write a petition. If the answer is not what you expected, at least you make catharsis and ask again. Or you know, you stop procrastinating and get back to studying.
          </p>
        </div>
      </div>
    </div>
    <div style="max-width: 100%;">
      <div class="row" style="width: 600px; margin: auto;">
        <div class="col-12" v-if="answer.length > 0">
          <p>{{ answer }}</p>
        </div>
        <div class="col-12">
          <q-field>
            <q-input v-model="petition" float-label="Petition"/>
          </q-field>
        </div>
        <div class="col-10">
          <q-field>
            <q-input v-model="question" float-label="Question"/>
          </q-field>
        </div>
        <div class="col-2" style="margin: auto;">
          <q-btn icon="send" label="SEND" flat @click="onSend()"/>
        </div>
      </div>
    </div>
  </q-page>
</template>

<style lang="stylus" scoped>
#banner
  background-color: #a40000;
  width: 100%
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
