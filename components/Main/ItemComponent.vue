<template>
  <div
    class="min-h-[112px] p-4 bg-white rounded-lg shadow flex-col justify-between items-start inline-flex cursor-pointer hover:bg-[#ededed]"
    @click="handleClick"
  >
    <div class="self-stretch justify-between items-center gap-2 inline-flex">
      <div class="justify-start items-center gap-2 flex">
        <div
          class="px-2 py-1 bg-opacity-10 rounded-2xl border justify-center items-center flex"
          :class="{
            'bg-lime-700 border-lime-700 text-lime-700': status === 'open',
            'bg-blue-700 border-blue-700 text-blue-700':
              status === 'dispatched',
          }"
        >
          <div class="text-[10px] font-normal">{{ status }}</div>
        </div>
        <div class="text-zinc-800 text-base font-bold">
          {{ lastName }}, {{ firstName }}
        </div>
      </div>
      <div
        class="px-2 py-1 bg-red-600 bg-opacity-10 rounded-2xl border border-red-600 justify-center items-center flex"
      >
        <div class="text-red-600 text-[8px] font-normal">1</div>
      </div>
    </div>
    <div
      class="self-stretch text-black text-sm font-normal overflow-hidden whitespace-nowrap text-overflow-ellipsis"
    >
      {{ workDescription }}
    </div>
    <div
      class="self-stretch justify-between items-center gap-4 inline-flex overflow-hidden whitespace-nowrap text-overflow-ellipsis"
    >
      <div class="text-black text-opacity-50 text-xs font-normal">
        #{{ number }}
      </div>
      <div class="justify-start items-center gap-1 flex">
        <img class="w-3.5 h-3.5 rounded-[14px]" :src="doctor" />
        <div class="text-black text-xs font-normal">Dr. Peter Silie</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ItemComponent',

  props: {
    item: { type: Object },
    doctor: { type: String },
    firstName: { type: String },
    lastName: { type: String },
    number: { type: String },
    status: { type: String },
    workDescription: { type: String },
  },

  methods: {
    handleClick() {
      // Emit a custom event with item data
      this.$emit('item-clicked', this.item);
    },
  },
};
</script>
