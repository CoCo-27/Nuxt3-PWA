<template>
  <!-- For Mobile -->
  <div
    v-if="isMobileView"
    class="flex flex-col desktop:flex-row justify-center items-center p-[2rem] bg-[#f5f5f5] w-full min-h-screen"
  >
    <component
      :is="currentComponent"
      @changeComponent="changeComponent"
    ></component>
  </div>

  <!-- For Desktop -->
  <div
    v-else
    class="flex flex-row justify-center items-center gap-[2rem] p-[2rem] bg-[#f5f5f5] w-full min-h-screen"
  >
    <template
      v-if="
        currentComponent === 'ListComponent' ||
        currentComponent === 'MessageComponent' ||
        currentComponent === 'RainerComponent'
      "
    >
      <ListComponent @changeComponent="changeComponent" />
      <MessageComponent @changeComponent="changeComponent" />
      <RainerComponent @changeComponent="changeComponent" />
    </template>
    <template v-else>
      <CreateComponent @changeComponent="changeComponent" />
    </template>
  </div>
</template>

<script>
import ListComponent from '~~/components/Main/ListComponent.vue';
import MessageComponent from '~~/components/Main/MessageComponent.vue';
import RainerComponent from '~~/components/Main/RainerComponent.vue';
import CreateComponent from '~~/components/Main/CreateComponent.vue';

export default {
  name: 'app',
  components: {
    ListComponent,
    MessageComponent,
    RainerComponent,
    CreateComponent,
  },

  data() {
    return {
      currentComponent: 'ListComponent', // default component
      isMobileView: false,
    };
  },
  mounted() {
    this.checkViewport();
    window.addEventListener('resize', this.checkViewport);
  },
  destroyed() {
    window.removeEventListener('resize', this.checkViewport);
  },
  watch: {
    isMobileView(value) {
      if (!value) {
        // Reset to default component for desktop view
        this.currentComponent = 'ListComponent';
      }
    },
  },
  methods: {
    checkViewport() {
      this.isMobileView = window.innerWidth <= 1200;
    },
    changeComponent(newComponent) {
      this.currentComponent = newComponent;
    },
  },
};
</script>
