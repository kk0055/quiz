<template>
  <div>
     <b-nav tabs>
        <b-nav-item href="#" disabled>Quiz</b-nav-item>
        <b-nav-item href="#" disabled>Counter:{{numCorrect}}/{{numTotal}}</b-nav-item>
      </b-nav>
  </div>
</template>

<script>
export default {
  props: [
    'numCorrect',
    'numTotal'
  ]
}
</script>