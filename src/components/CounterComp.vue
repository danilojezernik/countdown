<template>
  <h1 class="text-white p-3" v-if="!expired">Countdown until New Year 2023</h1>
  <h1 class="text-white" v-else>Happy New Year to all!</h1>
  <p class="p-3 fw-bold text-white">days : hours : minutes : seconds</p>
  <div v-if="loaded" class="fs-2 fw-bold">

      <span class="p-3 bg-danger text-white border border-danger rounded shadow">
        {{ prikaziDneve }}
      </span>
    <span class="text-white mx-2">:</span>
    <span class="p-3 bg-danger text-white border border-danger rounded shadow">
        {{ prikaziUre }}
      </span>
    <span class="text-white mx-2">:</span>
    <span class="p-3 bg-danger text-white border border-danger rounded shadow">
        {{ prikaziMinute }}
      </span>
    <span class="text-white mx-2">:</span>
    <span class="p-3 bg-danger text-white border border-danger rounded shadow">
        {{ prikaziSekunde }}
      </span>

  </div>
</template>

<script>
export default {
  props: ["year", "month", "date", "hour", "minute", "second", "millisecond"],
  data() {
    return {
      prikaziDneve: 0,
      prikaziUre: 0,
      prikaziMinute: 0,
      prikaziSekunde: 0,
      loaded: false,
      expired: false
    }
  },
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60
    },
    _hours() {
      return this._minutes * 60
    },
    _days() {
      return this._hours * 24
    },
    end() {
      return new Date(
          this.year,
          this.month,
          this.date,
          this.hour,
          this.minute,
          this.second,
          this.millisecond
      )
    }
  },
  mounted() {
    this.prikazi()
  },
  methods: {
    formatNum(num) {
      return num < 10 ? "0" + num : num;
    },
    prikazi() {
      let timer = setInterval(() => {
        let now = new Date();
        //let end = new Date(2022, 4, 13, 19, 30, 10, 10)
        let distance = this.end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          this.expired = true
          this.loaded = true
          return
        }

        let days = Math.floor(distance / this._days);
        let hours = Math.floor((distance % this._days) / this._hours)
        let minutes = Math.floor((distance % this._hours) / this._minutes)
        let seconds = Math.floor((distance % this._minutes) / this._seconds)

        this.prikaziMinute = this.formatNum(minutes)
        this.prikaziSekunde = this.formatNum(seconds)
        this.prikaziUre = this.formatNum(hours)
        this.prikaziDneve = this.formatNum(days)
        this.loaded = true
      }, 1000)
    }
  }
}
</script>
