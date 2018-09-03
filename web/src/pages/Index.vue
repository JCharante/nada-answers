<template>
  <q-page>
    <div class="red row justify-center" id="banner">
      <div class="col-xs-12 text-white gt-sm">
        <h3 class="text-center" style="margin-top: 0;">💩 Nada Answers</h3>
      </div>
      <div class="col-xs-12 col-md-7 col-lg-5 text-white not-too-wide pad-me-when-lt-md" style="padding-bottom: 16px;" v-if="answer.length === 0">
        <p>
          Welcome to Nada Answers...
        </p>
        <p>
          Do you need to ask a question? Are you looking for answers? Nada offers you a space to ask anything you want. However, before each question you must write a petition. If the answer is not what you expected, at least you make catharsis and ask again. Or you know, you stop procrastinating and get back to studying.
        </p>
      </div>
      <div class="col-xs-12 col-md-7 col-lg-5 text-white not-too-wide pad-me-when-lt-md" style="padding-bottom: 16px;" v-if="answer.length > 0">
        <p>Nada answers:</p>
        <p style="font-size: 24px;">{{ answer }}</p>
      </div>
    </div>
    <div class="row justify-center items-center content-center" id="notbanner">
      <div class="col-xs-12 row justify-center">
        <div class="col-xs-12 col-md-7 col-lg-5 row justify-center not-too-wide">
          <q-field style="width: 100%;">
            <q-input v-model="petition" @keydown="onKeyDown" float-label="Petition" :disable="answer.length > 0"/>
          </q-field>
        </div>
      </div>
      <div class="col-xs-12 row justify-center">
        <div class="col-xs-12 col-md-7 col-lg-5 row justify-center not-too-wide">
          <div class="col-xs-10 col-md-10 col-lg-10">
            <q-field>
              <q-input v-model="question" float-label="Question" :disable="answer.length > 0"/>
            </q-field>
          </div>
          <div class="col-xs-2 col-md-2 col-lg-2 row justify-end items-center">
            <q-btn class="lt-md" icon="send" color="primary" flat @click="onSend()" v-if="answer.length === 0"/>
            <q-btn class="gt-sm" icon="send" color="primary" label="SEND" flat @click="onSend()" v-if="answer.length === 0"/>
            <q-btn class="lt-md" icon="add" color="primary" flat @click="onNew()" v-if="answer.length > 0"/>
            <q-btn class="gt-sm" icon="add" color="primary" label="NEW" flat @click="onNew()" v-if="answer.length > 0"/>
          </div>
        </div>
      </div>
    </div>
    <div class="row justify-center items-center content-center" style="padding-top: 15vh;">
      <div class="col-xs-12 col-md-7 col-lg-5 not-too-wide">
        <q-card style="width: 100%">
          <q-card-main>
            <blockquote>
              We are not permitted to choose the frame of our destiny. But what we put into it is ours.
              <small><cite>Dag Hammarskjöld</cite></small>
            </blockquote>
          </q-card-main>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<style lang="stylus" scoped>
#banner
  background-color: #a40000;
  width: 100%;

.not-too-wide
  max-width: 90vw;

#banner div
  //padding-left: 16px;
  //padding-right: 16px;
  //max-width: 90vw;

#notbanner div
  //max-width: 90vw;

@media only screen and (max-width: 768px) {
  .pad-me-when-lt-md {
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
      let responses = ['idk', 'that\'s a pretty weird question to ask', 'try again later', 'umm.. maybe you should go back to studying', 'Trust and thou shall know.']
      let randomResponse = responses[Math.floor(Math.random() * responses.length)]
      return this.hiddenAnswer.length > 0 ? this.hiddenAnswer : randomResponse
    },
    onSend () {
      this.answer = this.genAnswer()
    },
    onNew () {
      this.answer = ''
      this.petition = ''
      this.question = ''
      this.hiddenAnswer = ''
    },
    // Get the next key in the phrase
    getNextKey (curLen) {
      if (curLen < this.primaryPhrase.length) {
        return this.primaryPhrase.substring(curLen, curLen + 1)
      } else {
        return ''
      }
    },
    onKeyDown (e) {
      let key = e.key
      let secretModeJustGotToggled = false

      if (key === '.') {
        this.secretModeToggled = !this.secretModeToggled
        secretModeJustGotToggled = true
      }

      if (this.secretModeToggled) {
        // Cancel Default
        e.preventDefault()

        // Add the fake letters to petition
        this.petition = this.petition.concat(this.getNextKey(this.petition.length))

        // Log the entered key into the answer
        // Only if they are normal characters (not control, not shift), and if the secret mode didn't just get toggled
        // To avoid adding the initial period
        if (key.length === 1 && !secretModeJustGotToggled) {
          this.hiddenAnswer = this.hiddenAnswer.concat(e.key.replace('^[A-Za-z0-9- ]+$', ''))
        }
      } else if (!this.secretModeToggled && secretModeJustGotToggled) {
        // If secret mode just got turn off, then don't add the period to the petition
        e.preventDefault()
      }
    }
  },
  data () {
    return {
      petition: '',
      question: '',
      answer: '',
      hiddenAnswer: '',
      secretModeToggled: false,
      primaryPhrase: 'Nada please answer the following question'
    }
  }
}
</script>
