<template>
  <div
    class="flex flex-col desktop:flex-row justify-center items-center gap-[6rem] p-[2rem] bg-[#f5f5f5] w-full min-h-screen"
  >
    <ListComponent />

    <MessageComponent />

    <RainerComponent />
  </div>
</template>

<script>
import ListComponent from '~~/components/Main/ListComponent.vue';
import MessageComponent from '~~/components/Main/MessageComponent.vue';
import RainerComponent from '~~/components/Main/RainerComponent.vue';

export default {
  name: 'app',
  components: {
    ListComponent,
    MessageComponent,
    RainerComponent,
  },
};
</script>
