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
            'bg-yellow-500 border-yellow-500 text-yellow-500':
              status === 'dispatched',
            'bg-blue-700 border-blue-700 text-blue-700':
              status === 'in_production',
            'bg-zinc-800 border-zinc-800 text-zinc-800': status === 'done',
          }"
        >
          <div class="text-[10px] font-normal">{{ status }}</div>
        </div>
        <div v-if="item.patient" class="text-zinc-800 text-base font-bold">
          {{ firstName }}, {{ lastName }}
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
      <div v-if="item.dentist" class="justify-start items-center gap-1 flex">
        <img class="w-3.5 h-3.5 rounded-[14px]" :src="this.imageSrc" />
        <div class="text-black text-xs font-normal">
          Dr. {{ dentist_firstName }} {{ dentist_lastName }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ItemComponent',

  data() {
    return {
      imageSrc: null,
    };
  },

  props: {
    item: { type: Object },
    doctor: { type: String },
    firstName: { type: String },
    lastName: { type: String },
    number: { type: String },
    status: { type: String },
    workDescription: { type: String },
    dentist_firstName: { type: String },
    dentist_lastName: { type: String },
    dentist_image: { type: String },
  },

  mounted() {
    const runtimeConfig = useRuntimeConfig();
    fetch(`https://app.wunschlachen.de/staging/assets/${this.dentist_image}`, {
      method: 'GET',
      headers: {
        Authorization: runtimeConfig.public.BEARER_TOKEN,
      },
    })
      .then((response) => response.blob())
      .then((data) => {
        this.imageSrc = URL.createObjectURL(data);
      })
      .catch((error) => console.error(error));
  },

  methods: {
    handleClick() {
      // Emit a custom event with item data
      this.$emit('item-clicked', this.item);
    },
  },
};
</script>
