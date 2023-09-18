<template>
  <div
    class="w-full desktop:w-1/3 h-[852px] flex flex-col justify-between gap-4 pb-6 relative bg-neutral-50"
  >
    <div
      v-if="isMobileView"
      class="h-fit p-4 bg-white rounded-bl-lg rounded-br-lg shadow flex-col justify-start items-start gap-2 inline-flex"
    >
      <div class="self-stretch justify-between items-center gap-2 inline-flex">
        <div
          class="pl-2 pr-4 py-2 bg-[#fafafa] rounded-[100px] justify-start items-center gap-2 flex cursor-pointer hover:bg-white"
          @click="gotoPre"
        >
          <div class="w-6 h-6 relative">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
            >
              <path
                d="M6.64999 12.35L12.5 18.2L12 18.7L5.29999 12L12 5.29999L12.5 5.79999L6.64999 11.65H18.7V12.35H6.64999Z"
                fill="black"
              />
            </svg>
          </div>
          <div class="text-black text-base font-normal">Übersicht</div>
        </div>
        <div
          class="px-4 py-2 bg-[#fafafa] rounded-[100px] justify-start items-center gap-2 flex cursor-pointer hover:bg-white"
          @click="goToDetail"
        >
          <div class="text-black text-base font-normal">Details</div>
        </div>
      </div>
      <div class="self-stretch justify-between items-center gap-2 inline-flex">
        <div class="justify-start items-center gap-2 flex">
          <div
            class="px-2 py-1 bg-opacity-10 rounded-2xl border justify-center items-center flex"
            :class="{
              'bg-lime-700 border-lime-700 text-lime-700':
                selectedItem.status === 'open',
              'bg-yellow-500 border-yellow-500 text-yellow-500':
                selectedItem.status === 'dispatched',
              'bg-blue-700 border-blue-700 text-blue-700':
                selectedItem.status === 'in_production',
              'bg-zinc-800 border-zinc-800 text-zinc-800':
                selectedItem.status === 'done',
            }"
          >
            <div class="text-[10px] font-normal">{{ selectedItem.status }}</div>
          </div>
          <div
            v-if="selectedItem.patient"
            class="text-zinc-800 text-base font-bold"
          >
            {{ selectedItem.patient?.first_name }},
            {{ selectedItem.patient?.last_name }}
          </div>
        </div>
        <div></div>
      </div>
      <div class="self-stretch text-black text-xs font-normal">
        {{ selectedItem.work_description }}
      </div>
      <div class="self-stretch justify-between items-center gap-4 inline-flex">
        <div class="text-black text-opacity-50 text-xs font-normal">
          #{{ selectedItem.patient?.patient_number }}
        </div>
        <div
          v-if="selectedItem?.dentist"
          class="justify-start items-center gap-1 flex"
        >
          <img class="w-3.5 h-3.5 rounded-[14px]" :src="imageSrc" />
          <div class="text-black text-xs font-normal">
            Dr. {{ selectedItem?.dentist?.first_name }}
            {{ selectedItem?.dentist?.last_name }}
          </div>
        </div>
      </div>
    </div>

    <div v-else></div>

    <div
      class="flex flex-col-reverse space-y-reverse space-y-4 w-full h-full pl-4 pb-2 overflow-y-auto overflow-x-hidden"
    >
      <div
        class="flex items-end space-x-4"
        v-for="(info, index) in this.messagesvalue"
        :key="index"
      >
        <img class="w-3.5 h-3.5 rounded-[14px]" :src="imageSrc" />
        <div
          class="space-y-1 px-4 py-2 bg-white rounded-tl-lg rounded-tr-lg rounded-br-lg shadow flex-col justify-start items-start gap-1 inline-flex"
        >
          <div class="min-w-[295px] flex justify-between items-center text-xs">
            <div class="font-bold text-black">
              Dr. {{ selectedItem?.dentist?.first_name }}
              {{ selectedItem?.dentist?.last_name }}
            </div>
            <div class="text-black text-opacity-50">vor 3 min</div>
          </div>
          <div class="text-sm text-black">
            {{ info.data.message }}
          </div>
        </div>
      </div>
    </div>

    <div class="w-full px-4 justify-center items-center inline-flex">
      <div class="bg-white rounded-[100px] w-full px-4 py-2 gap-2 inline-flex">
        <div class="w-6 h-6 relative">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
          >
            <path
              d="M11.65 12.35H6.29999V11.65H11.65V6.29999H12.35V11.65H17.7V12.35H12.35V17.7H11.65V12.35Z"
              fill="black"
            />
          </svg>
        </div>
        <div class="grow shrink basis-0 text-black text-sm font-normal">
          schreiben...
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MessageComponent',

  data() {
    return {
      imageSrc: null,
      messagesvalue: [],
    };
  },

  mounted() {
    console.log('Messages ID === ', this.selectedItem?.Messages);

    this.fetchMessages();
    this.fetchImage();
  },

  props: {
    isMobileView: Boolean,
    selectedItem: Object, // Added new prop to receive the selected item
  },

  watch: {
    selectedItem: {
      handler(newVal, oldVal) {
        if (newVal) {
          this.fetchImage();

          this.fetchMessages();
        }
      },
      deep: true,
    },
  },

  methods: {
    gotoPre() {
      console.log(this.messagesvalue);
      this.$emit('changeComponent', 'ListComponent');
    },

    goToDetail() {
      this.$emit('changeComponent', 'RainerComponent');
    },

    async fetchImage() {
      const runtimeConfig = useRuntimeConfig();
      fetch(
        `https://app.wunschlachen.de/staging/assets/${this.selectedItem?.dentist?.profile_image.id}`,
        {
          method: 'GET',
          headers: {
            Authorization: runtimeConfig.public.BEARER_TOKEN,
          },
        }
      )
        .then((response) => response.blob())
        .then((data) => {
          this.imageSrc = URL.createObjectURL(data);
        })
        .catch((error) => console.error(error));
    },

    async fetchMessages() {
      const runtimeConfig = useRuntimeConfig();

      const messageRequests = this.selectedItem?.Messages.map((message) =>
        fetch(`https://app.wunschlachen.de/staging/items/messages/${message}`, {
          method: 'GET',
          headers: {
            Authorization: runtimeConfig.public.BEARER_TOKEN,
          },
        })
      );

      const messages = await Promise.all(messageRequests);
      const jsonMessages = await Promise.all(
        messages.map((message) => message.json())
      );

      this.messagesvalue = jsonMessages;
    },
  },
};
</script>
