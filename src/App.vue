<template>
  <div id="app" class="h-100">
    <div class="container h-100">
      <div class="row h-100">
        <div class="col-12 h-100 d-flex justify-content-center align-items-center">
          <div class="col-md-8 rounded px-5 py-4 shadow bg-white">
            <CheckoutForm />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CheckoutForm from './components/CheckoutForm.vue'

export default {
  name: 'App',
  components: {
    CheckoutForm
  }
}
</script>

