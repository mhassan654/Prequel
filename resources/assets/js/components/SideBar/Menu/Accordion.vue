<template>
  <div class="accordion">
    <transition name="accordion"
                @before-enter="beforeEnter" @enter="enter"
                @before-leave="beforeLeave" @leave="leave">
      <div class="animate-all body" v-show="show">
        <div class="body-inner">
          <slot></slot>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
// Component thanks to https://codepen.io/ktsn
export default {
  name : "Accordion",
  props: ["theme"],
  data() {
    return {
      show  : true,
      status: "CLOSED",
    };
  },
  methods: {
    toggle     : function () {
      this.show = !this.show;
      this.status = this.show ? "OPEN" : "CLOSED";
    },
    beforeEnter: function (el) {
      el.style.height = "0";
    },
    enter      : function (el) {
      el.style.height = el.scrollHeight + "px";
    },
    beforeLeave: function (el) {
      el.style.height = el.scrollHeight + "px";
    },
    leave      : function (el) {
      el.style.height = "0";
    },
  },
};
</script>

<style lang="scss">
.accordion .body {
  overflow-y: scroll;
  height: 75vh !important;
  transition: 500ms ease;
}

.accordion .body-inner {
  padding: 0 0 8px;
  overflow-wrap: break-word;
}
</style>
