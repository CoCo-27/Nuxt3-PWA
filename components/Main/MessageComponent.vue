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
          <div class="text-zinc-800 text-base font-bold">
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
        <div class="justify-start items-center gap-1 flex">
          <img
            class="w-3.5 h-3.5 rounded-[14px]"
            :src="result?.data.profile_image"
          />
          <div v-if="dentistItem" class="text-black text-xs font-normal">
            Dr. {{ dentistItem.first_name }} {{ dentistItem.last_name }}
          </div>
        </div>
      </div>
    </div>

    <div v-else></div>
    <div
      class="absolute top-[600px] left-[16px] flex items-end space-x-4 w-full h-auto"
    >
      <img class="w-3.5 h-3.5 rounded-[14px]" :src="doctor" />
      <div class="bg-white rounded-lg shadow flex flex-col space-y-1 py-2 px-4">
        <div class="flex justify-between items-center text-xs">
          <div class="font-bold text-black">Dr. Peter Silie</div>
          <div class="text-black text-opacity-50">vor 3 min</div>
        </div>
        <div class="text-sm text-black">
          Guten Tag Herr Paetz wie kann ich Ihnen <br />heute helfen?
        </div>
      </div>
    </div>

    <div
      class="absolute left-[82px] right-[16px] top-[692px] w-auto h-auto px-4 py-2 bg-lime-600 bg-opacity-10 rounded-tl-lg rounded-tr-lg rounded-bl-lg shadow flex flex-col justify-start items-start gap-1"
    >
      <div class="self-stretch justify-between items-center gap-1 inline-flex">
        <div class="text-black text-xs font-bold">Ich</div>
        <div class="text-black text-opacity-50 text-xs font-normal">
          vor 3 min
        </div>
      </div>
      <div class="text-black text-sm font-normal">
        Heute benötige ich einiges von Ihnen <br />es wird ein großer Auftrag.
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
import doctorImage from 'assets/doctor.png';

export default {
  name: 'MessageComponent',

  data() {
    return {
      doctor: doctorImage,
    };
  },

  props: {
    isMobileView: Boolean,
    selectedItem: Object, // Added new prop to receive the selected item
    dentistItem: Object,
  },

  watch: {
    selectedItem: {
      handler: function (val) {
        console.log('selectedItem changed to:', val);
      },
      deep: true,
    },
  },

  mounted() {
    console.log('dentist == ', this.dentistItem);
  },

  methods: {
    gotoPre() {
      this.$emit('changeComponent', 'ListComponent');
    },

    goToDetail() {
      this.$emit('changeComponent', 'RainerComponent');
    },
  },
};
</script>
