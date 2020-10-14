<script>
export default {
  name: "modal",
  methods: {
    close() {
      this.$emit("close");
    }
  }
};
</script>
<template>
  <transition name="modal-fade">
    <div class="modal-overlay">
      <div
        class="modal-window"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        <header class="modal-head" id="modalTitle">
          <slot name="header">
            <button
              type="button"
              class="btn-close ml-auto"
              @click="close"
              aria-label="Close modal"
            >
              <i class="far fa-times"></i>
            </button>
          </slot>
        </header>
        <section class="modal-bod" id="modalDescription">
          <slot name="body">
            I'm the default body!
          </slot>
        </section>
        <footer class="modal-foot">
          <slot name="footer"> </slot>
        </footer>
      </div>
    </div>
  </transition>
</template>
<style lang="scss">
.modal-overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-window {
  max-height: 90vh;
  background: #ffffff;
  box-shadow: 2px 2px 40px 1px;
  border-radius: 0.5rem;
  display: flex;
  flex-direction: column;
  overflow-y: auto;
  position: relative;
}

.modal-head {
  padding: 15px;
  display: flex;
  width: 100%;
}

.modal-head {
  position: absolute;
  top: 0;
  z-index: 1001;
  // border-bottom: 1px solid #eeeeee;
  color: #4aae9b;
  justify-content: space-between;
}

.modal-foot {
  // bottom: 0;
  // border-top: 1px solid #eeeeee;
  justify-content: flex-end;
}

.modal-bod {
  // position: relative;
  max-height: 100%;
  overflow-y: auto;
  // padding: 20px 10px;
}

.btn-close {
  border: none;
  font-size: 2rem;
  // padding: 20px;
  cursor: pointer;
  font-weight: bold;
  color: #27aae1;
  background: transparent;
  &:hover,
  &:focus {
    color: black;
  }
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}
.modal-fade-enter,
.modal-fade-leave-active {
  opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.5s ease;
}
</style>
