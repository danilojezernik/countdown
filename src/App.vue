<template>
  <div class="container mt-5 text-center">

    <counter
    :year="2022"
    :month="12"
    :date="31"
    :hour="23"
    :minute="59"
    :second="59"
    :millisecond="99"
    />

  </div>

</template>

<script>
import Counter from "@/components/CounterComp.vue"
export default {
  components:{
    Counter
  }
}
</script>
