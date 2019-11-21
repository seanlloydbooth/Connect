<template>
  <div class="centered-container">
    <md-content class>
      <div class="title">
        <div
          class="md-body-2"
        >To connect to the Harmony PSA application, please provide the URL you would normally use to log in.</div>
        <br>
        <div class="md-body-1" style="color: grey">Example: mycompany.harmonypsa.com</div>
      </div>

      <div class="form">
        <md-field>
          <label>Harmony URL</label>
          <md-input v-model="login.email" autofocus></md-input>
        </md-field>
      </div>

      <div class="actions md-layout md-alignment-center">
        <md-button class="md-raised md-primary" @click="auth">Continue</md-button>
      </div>

      <div class="loading-overlay" v-if="loading">
        <md-progress-spinner md-mode="indeterminate" :md-stroke="2"></md-progress-spinner>
      </div>
    </md-content>
    <div class="background"/>
  </div>
</template>

<script>
setTimeout(function() {
  var items = [
    {
      label: 'Change Harmony Instance',
      url: 'http://vg1cz.csb.app/',
      subLinks: [],
      icon: 'fa-sign-out'
    }
  ]

  var json = JSON.stringify(items)

  window.location.href =
    'gonative://sidebar/setItems?items=' + encodeURIComponent(json)
}, 0)

export default {
  name: 'App',
  data() {
    return {
      loading: false,
      login: {
        email: ''
      }
    }
  },
  methods: {
    auth() {
      // your code to login user
      // this is only for example of loading
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 5000)

      var url = this.login.email

      var prefix = 'http://'
      if (url.substr(0, prefix.length) !== prefix) {
        url = prefix + url
      }

      if (url === null || url === '') {
        alert('Not valid')
      } else {
        debugger
        window.location.href = 'gonative://config/set?initialUrl=' + url

        setTimeout(function() {
          window.location.href = url
        }, 5000)
      }
    }
  }
}
</script>

<style lang="scss">
.centered-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  min-height: -webkit-fill-available;
  background: #ebeff0;

  .title {
    text-align: center;
    margin-bottom: 30px;
    img {
      margin-bottom: 16px;
      max-width: 160px;
    }
  }
  .actions {
    .md-button {
      margin: 0;
    }
  }
  .form {
    margin-bottom: 60px;
  }
  .md-content {
    z-index: 1;
    padding: 40px;
    width: 80%;
    max-width: 400px;
    position: relative;
    min-height: -webkit-fill-available;
    border-radius: 20px;
  }
  .loading-overlay {
    z-index: 10;
    top: 0;
    left: 0;
    right: 0;
    position: absolute;
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.9);
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
