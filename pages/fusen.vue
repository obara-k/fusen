<template>
  <section class="section">
    <div class="input_wrapper">
      <b-field label="Name">
        <b-input
          v-model="inputs.name"
          placeholder="name"
        ></b-input>
      </b-field>
      <b-field label="icon">
        <b-input
          v-model="inputs.icon"
          placeholder="icon"
        ></b-input>
      </b-field>
      <b-field label="Date">
        <b-datepicker
          :show-week-number="showWeekNumber"
          placeholder="Click to select..."
          v-model="inputs.latestDate"
          icon="calendar-today">
        </b-datepicker>
      </b-field>
      <b-field label="Status">
        <b-select v-model="inputs.latestTenki">
          <option
            v-for="cond in status"
            :key="cond.key"
            :value="cond.key"
          >
            {{ cond.key }}
          </option>
        </b-select>
      </b-field>
      <b-button
        @click="addTenkiCard"
        type="is-info"
      >
        Submit
      </b-button>
    </div>
    <div class="cardWrap">
      <TenkiCard
        class="fusen_card"
        v-for="(member, index) in members"
        :key="index"
        :name="member.name"
        :icon="member.icon"
        :latestDate="member.latestDate"
        :latestTenki="member.latestTenki"
      >
        <b-button
          @click="removeTenkiCard(index)"
          type="is-light"
          icon-right="delete"
        />
      </TenkiCard>
    </div>
  </section>
</template>

<script>
import Card from '~/components/Card'
import TenkiCard from '~/components/TenkiCard'

export default {
  name: 'fusen',

  components: {
    Card,
    TenkiCard
  },
  data() {
    return {
      showWeekNumber: false,
      items: [
        { title: 'Free', description: 'test project'}
      ],
      members: [
        { name: 'Kunito Obara', icon: 'KO', latestDate:'2019/10/08', latestTenki: 'Normal' , log: [
            { date: '2019/10/07' , tenki: 'Good' },
            { date: '2019/10/06' , tenki: 'VeryGood' },
            { date: '2019/10/05' , tenki: 'Bad' },
            { date: '2019/10/04' , tenki: 'VeryBad' }
          ]
        }
      ],
      status: [
        { key: 'VeryGood' },
        { key: 'Good' },
        { key: 'Normal' },
        { key: 'Bad' },
        { key: 'VeryBad' }
      ],
      inputs: {
        name: '',
        latestDate: '',
        latestTenki: '',
        icon: ''
      },
      form: {
        title: '',
        description: '',
      }
    }
  },
  methods: {
    addCard() {
      let temp = []
      const data = JSON.parse(JSON.stringify(this.items))
      const model = JSON.parse(JSON.stringify(this.form))
      temp = data
      temp.push(model)
      this.items = temp
      this.form.title = ''
      this.form.description = ''
    },
    addTenkiCard() {
      let temp = []
      const data = JSON.parse(JSON.stringify(this.members))
      const model = JSON.parse(JSON.stringify(this.inputs))
      temp = data
      temp.push(model)
      this.members = temp
      this.inputs = { name: '', date: '', status: '', icon: ''}
    },
    removeCard(key) {
      this.items.splice(key,1)
    },
    removeTenkiCard(key) {
      this.members.splice(key,1)
    }
  }
}
</script>
<style lang="scss" scoped>
.cardWrap {
  display: flex;
  flex-wrap: wrap;
  justify-content: left;
  .fusen_card {
    flex-grow: 3;
  }
}

</style>
