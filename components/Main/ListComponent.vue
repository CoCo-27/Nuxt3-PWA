<template>
  <div
    class="w-full desktop:w-1/3 h-[852px] flex flex-col gap-4 p-4 relative bg-[#fafafa]"
  >
    <div class="w-6 h-6 left-[16px] top-[16px]">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
      >
        <path
          d="M4.65 17.05C4.55084 17.05 4.46771 17.0164 4.40063 16.9491C4.33354 16.8819 4.3 16.7986 4.3 16.6991C4.3 16.5997 4.33354 16.5167 4.40063 16.45C4.46771 16.3833 4.55084 16.35 4.65 16.35H19.35C19.4492 16.35 19.5323 16.3836 19.5994 16.4509C19.6665 16.5181 19.7 16.6015 19.7 16.7009C19.7 16.8003 19.6665 16.8833 19.5994 16.95C19.5323 17.0167 19.4492 17.05 19.35 17.05H4.65ZM4.65 12.35C4.55084 12.35 4.46771 12.3164 4.40063 12.2491C4.33354 12.1819 4.3 12.0986 4.3 11.9991C4.3 11.8997 4.33354 11.8167 4.40063 11.75C4.46771 11.6833 4.55084 11.65 4.65 11.65H19.35C19.4492 11.65 19.5323 11.6836 19.5994 11.7509C19.6665 11.8181 19.7 11.9015 19.7 12.0009C19.7 12.1003 19.6665 12.1833 19.5994 12.25C19.5323 12.3167 19.4492 12.35 19.35 12.35H4.65ZM4.65 7.65001C4.55084 7.65001 4.46771 7.61639 4.40063 7.54914C4.33354 7.48189 4.3 7.39855 4.3 7.29914C4.3 7.19972 4.33354 7.11668 4.40063 7.05001C4.46771 6.98335 4.55084 6.95001 4.65 6.95001H19.35C19.4492 6.95001 19.5323 6.98364 19.5994 7.05089C19.6665 7.11814 19.7 7.20147 19.7 7.30089C19.7 7.4003 19.6665 7.48335 19.5994 7.55001C19.5323 7.61668 19.4492 7.65001 19.35 7.65001H4.65Z"
          fill="black"
        />
      </svg>
    </div>
    <div
      class="w-full left-[16px] top-[56px] justify-between items-center inline-flex"
    >
      <div class="text-zinc-800 text-2xl font-bold">Laborarbeiten</div>
      <div class="justify-start items-center gap-2 flex">
        <div
          class="p-1 bg-white rounded-2xl justify-start items-center gap-1 flex"
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
                d="M11.075 16.7C10.9758 16.7 10.8927 16.6664 10.8256 16.5991C10.7585 16.5319 10.725 16.4485 10.725 16.3491C10.725 16.2497 10.7585 16.1667 10.8256 16.1C10.8927 16.0333 10.9758 16 11.075 16H12.9C12.9992 16 13.0823 16.0336 13.1494 16.1009C13.2165 16.1681 13.25 16.2514 13.25 16.3509C13.25 16.4503 13.2165 16.5333 13.1494 16.6C13.0823 16.6667 12.9992 16.7 12.9 16.7H11.075ZM7.4 12.35C7.30084 12.35 7.21771 12.3164 7.15063 12.2491C7.08354 12.1819 7.05 12.0985 7.05 11.9991C7.05 11.8997 7.08354 11.8167 7.15063 11.75C7.21771 11.6833 7.30084 11.65 7.4 11.65H16.575C16.6742 11.65 16.7573 11.6836 16.8244 11.7509C16.8915 11.8181 16.925 11.9014 16.925 12.0009C16.925 12.1003 16.8915 12.1833 16.8244 12.25C16.7573 12.3167 16.6742 12.35 16.575 12.35H7.4ZM4.65 7.99999C4.55084 7.99999 4.46771 7.96636 4.40063 7.89911C4.33354 7.83186 4.3 7.74853 4.3 7.64911C4.3 7.5497 4.33354 7.46665 4.40063 7.39999C4.46771 7.33332 4.55084 7.29999 4.65 7.29999H19.35C19.4492 7.29999 19.5323 7.33361 19.5994 7.40086C19.6665 7.46811 19.7 7.55145 19.7 7.65086C19.7 7.75028 19.6665 7.83332 19.5994 7.89999C19.5323 7.96665 19.4492 7.99999 19.35 7.99999H4.65Z"
                fill="black"
              />
            </svg>
          </div>
        </div>
        <div
          class="p-1 bg-[#ffffff] rounded-2xl justify-start items-center gap-1 flex cursor-pointer hover:bg-[#ededed]"
          @click="gotoCreate"
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
                d="M11.65 12.35H6.3V11.65H11.65V6.29999H12.35V11.65H17.7V12.35H12.35V17.7H11.65V12.35Z"
                fill="black"
              />
            </svg>
          </div>
        </div>
      </div>
    </div>

    <div class="flex flex-col gap-4 overflow-y-auto">
      <ItemComponent
        v-for="item in result?.data || []"
        :key="item.id"
        :doctor="doctor"
        :firstName="item.patient?.first_name"
        :lastName="item.patient?.last_name"
        :number="item.patient?.patient_number"
        :status="item.status"
        :workDescription="item.work_description"
        :dentist_firstName="item.dentist?.first_name"
        :dentist_lastName="item.dentist?.last_name"
        :dentist_image="item.dentist?.profile_image?.id"
        :item="item"
        @item-clicked="handleItemClick"
      />
    </div>
  </div>
</template>

<script>
import doctorImage from 'assets/doctor.png';
import ItemComponent from './ItemComponent.vue';

export default {
  name: 'ListComponent',
  components: {
    ItemComponent,
  },

  data() {
    return {
      doctor: doctorImage,
      result: null,
      loading: false,
    };
  },

  props: {
    isMobileView: Boolean,
  },

  created: async function () {
    this.loading = true;
    const runtimeConfig = useRuntimeConfig();
    const response = await fetch(
      'https://app.wunschlachen.de/staging/items/Laboratory_work?fields=*%2Cpatient.first_name%2Cpatient.last_name%2Cpatient.patient_number%2Cdentist.first_name%2Cdentist.last_name%2Cdentist.profile_image.id&=',
      {
        method: 'GET',
        headers: {
          Authorization: runtimeConfig.public.BEARER_TOKEN,
        },
      }
    );

    if (response.ok) {
      this.loading = false;
      this.result = await response.json();
      console.log('result = ', this.result.data);

      // Auto select the first item
      if (this.result.data.length > 0 && this.isMobileView === false) {
        this.handleItemClick(this.result.data[0]);
      }
    } else {
      this.loading = false;
      console.error('Response Error:', response);
    }
  },

  methods: {
    gotoCreate() {
      this.$emit('changeComponent', 'CreateComponent');
    },

    handleItemClick(item) {
      // emit event to parent component (App.vue)
      this.$emit('change-selected-item', item);
    },
  },
};
</script>
