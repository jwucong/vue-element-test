<template>
  <div class="home">
    <online-nps></online-nps>
		<nps-details></nps-details>
  </div>
</template>

<script>
// @ is an alias to /src
import OnlineNps from '@/views/OnlineNps/List'
import NpsDetails from '@/views/OnlineNps/Details'

export default {
  name: 'home',
  components: {
		OnlineNps,
		NpsDetails
  }
}
</script>
