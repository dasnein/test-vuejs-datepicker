<template>
  <div id="app">
    <h2>Switch language</h2>
    <p>current: {{ language }}</p>
    <nav>
      <button class="change-lang" data-lang="en" @click="changeLang">en</button>
      <button class="change-lang" data-lang="ru" @click="changeLang">ru</button>
      <button class="change-lang" data-lang="it" @click="changeLang">it</button>
    </nav>
    <hr>
    <div class="example">
      <datepicker
        ref="datepicker"
        :mondayFirst="true"
        :fullMonthName="true"
        format="MMMM, d"
        maximumView="month"
        :value="date"
        :yearsChoosable="false"
        @opened="onOpen"
        @selected="onSelect"
        :language="langs[language]"
        />
    </div>
  </div>
</template>

<script>
import Datepicker from 'vuejs-datepicker';
import * as langs from 'vuejs-datepicker/dist/locale'

export default {
  name: 'App',
  components: {
    Datepicker
  },

  data () {
    return {
      date: null,
      language: 'en',
      langs: langs
    }
  },

  methods: {
    onOpen () {
      if (!this.date) {
        const startDate = new Date(2020, 0, 1)
        this.$refs.datepicker.changeDate(startDate)
      }
    },
    onSelect (date) {
      this.date = date
    },
    changeLang (e) {
      const newLang = e.target.dataset.lang
      if (newLang in langs) {
        this.language = newLang
      }
    }
  }
}
</script>

<style>
#app {
  padding-left: 5em;
}

.change-lang {
  width: 2em;
  height: 2em;
  padding: 0;
  margin-right: 1em;
}
</style>
