<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <v-date-picker
      is-inline
      is-expanded
      mode="range"
      isDate="date"
      v-model="selectedDate"
      :select-attribute="selectAttribute"
      :drag-attribute="dragAttribute"
      :attributes="attributes"
      :theme-styles="themeStyles"
      >
      <!-- <span slot="header-title" slot-scope="{yearLabel, monthLabel}">
        {{yearLabel}}년 {{monthLabel}}
      </span> -->
    </v-date-picker>
    <div>Selected date: <span>{{ selectedDateText }}</span></div>
  </div>
</template>

<script>
import Vue from 'vue';
import VCalendar from 'v-calendar';
import 'v-calendar/lib/v-calendar.min.css';
Vue.use(VCalendar);

export default {
  name: 'V-datepicker',
   data() {
    return {
      selectedDate: {
        start: new Date(),
        end: new Date()
      },
      attributes: [
        {
          dates: {}, // Every day,
          popover: {
            component: null,
            visibility: 'hidden'
          }
        }
      ],
      dragAttribute: {
        highlight({ onStart, onEnd }) {
          return {
            backgroundColor: (onStart || onEnd)? '#00dbbf' : '#e1fffb',
          }
        },
        contentStyle({ onStart, onEnd }) {
          return {
            color: (onStart || onEnd)? '#ffffff' : '#686868',
          }
        }
      },
      selectAttribute:{
        highlight({ onStart, onEnd }) {
          return {
            backgroundColor: (onStart || onEnd)? '#00dbbf' : '#e1fffb',
          }
        },
        contentStyle({ onStart, onEnd }) {
          return {
            color: (onStart || onEnd)? '#ffffff' : '#686868',
          }
        }
      },
      //본문 스타일
      themeStyles: {
        // 테두리
        wrapper: {
          background: '#fff',
          color: '#686868',
          'border-bottom': '1px solid #eee'
        },
        // 헤더
        header: {
          padding: `40px 0 25px 0`,
        },
        weeks: {
          padding: `0 0 38px`,
        },
        // 날짜
        weekdays: {
          color: '#686868', // New color
          // fontWeight: '600', // And bolder font weight
          padding: `25px 0`,
        },
        //이번달이 아닌 날짜
        dayCellNotInMonth: {
          color: '#686868',
          opacity: 0.4,
        }
      }
    }
  },
  props: {
    msg: String
  },
  computed: {
    selectedDateText () {
      return `${this.getTextFormat(this.selectedDate.start)} ~ ${this.getTextFormat(this.selectedDate.end)}`;
    }
  },
  methods: {
    getTextFormat(val) {
      let y = val.getFullYear()
      let m = val.getMonth()+1
      let d = val.getDate()
      return `${y}-${ m<10 ? '0'+m : m}-${ d<10 ? '0'+d : d}`
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
