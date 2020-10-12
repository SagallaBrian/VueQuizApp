<template>
  <div>
    <b-container fluid="lg" class="pt-3 pb-5">
      <div class="footer text-md-right">
         <h6 class="font-weight-normal text-success">This is Powered by Komplab Tech</h6>

      </div>
      
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Foota",
  props: {
    Footamessa: {
      type: String,
      default: "Footer Message",
    },
  },
};
</script>