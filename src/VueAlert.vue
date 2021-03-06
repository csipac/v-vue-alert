<template>
  <transition :name="alertTransition" mode="out-in">
    <div class="vue-alert alert" :class="[ alertType, alertTransition ]" :key="triggerTransition"  v-if="alertShow">
      <p>{{alertMessage}}</p>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'VueAlert',
  data () {
    return {
      alertForceRender: false,
      alertMessage: '',
      alertType: '',
      alertTransition: '',
      alertShow: true,
      triggerTransition: true,
      default: {
        duration: 5000,
        forceRender: true,
        message: '',
        type: 'hide',
        transition: 'fade'
      }
    }
  },
  methods: {
    clearDefault () {
      this.default.type = 'hide'
    },
    setDefault ({ message = this.default.message, type = this.default.type, duration = this.default.duration, transition = this.default.transition, forceRender = this.default.forceRender } = {}) {
      this.default.message = message
      this.default.type = type
      this.default.duration = duration
      this.default.transition = transition
      this.default.forceRender = forceRender
      return this
    },
    show ({ message = this.default.message, type = this.default.type, duration = this.default.duration, transition = this.default.transition, forceRender = this.default.forceRender } = {}) {
      this.alertShow = true
      this.alertMessage = message
      this.alertType = `alert-${type}`
      this.alertTransition = transition
      this.alertForceRender = forceRender
      if (this.alertTimeout) {
        clearTimeout(this.alertTimeout)
      }
      /* istanbul ignore else */
      if (duration) {
        this.alertTimeout = setTimeout(() => {
          if (this.default.type == 'hide') {
            this.hide()
          } else {
            this.show({
              duration: false
            })
          }
        }, duration)
      }
      if (this.alertForceRender) {
        this.triggerTransition = !this.triggerTransition
      }
    },
    hide () {
      this.alertShow = false
      if (this.alertTimeout) {
        clearTimeout(this.alertTimeout)
      }
    },
    danger (args) {
      this.show({ type: 'danger', ...args })
    },
    info (args) {
      this.show({ type: 'info', ...args })
    },
    success (args) {
      this.show({ type: 'success', ...args })
    },
    warning (args) {
      this.show({ type: 'warning', ...args })
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity .3s
}
.fade-enter, .fade-leave-to {
  opacity: 0
}

.smooth {
  transition: all 0.5s ease;
}

.alert {
  padding: 15px;
  border: 1px solid transparent;
  border-radius: 4px;
}

.alert-info {
  color: #ffffff;
  background-color: #209cee;
  border-color: #1d8cd6;
  text-align: center;
}

.alert-success {
  color: #ffffff;
  background-color: #23d160;
  border-color: #1fbc56;
  text-align: center;
}

.alert-warning {
  color: #ffffff;
  background-color: #ffdd57;
  border-color: #e5c74e;
  text-align: center;
}

.alert-danger {
  color: #ffffff;
  background-color: #ff3860;
  border-color: #e53256;
  text-align: center;
}
</style>
