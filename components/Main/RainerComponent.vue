<template>
  <div
    class="w-full desktop:w-1/3 h-[852px] flex flex-col gap-4 p-4 relative bg-neutral-50"
  >
    <div class="self-stretch justify-between items-center gap-2 inline-flex">
      <div class="justify-start items-center gap-2 flex">
        <div
          class="px-4 py-2 bg-lime-700 bg-opacity-10 rounded-3xl border border-lime-700 justify-center items-center flex"
          :class="{
            'bg-lime-700 border-lime-700 text-lime-700':
              selectedItem?.status === 'open',
            'bg-yellow-500 border-yellow-500 text-yellow-500':
              selectedItem?.status === 'dispatched',
            'bg-blue-700 border-blue-700 text-blue-700':
              selectedItem?.status === 'in_production',
            'bg-zinc-800 border-zinc-800 text-zinc-800':
              selectedItem?.status === 'done',
          }"
        >
          <div class="text-sm font-normal">
            {{ selectedItem?.status }}
          </div>
        </div>
      </div>
      <div
        class="justify-start items-center gap-2 flex cursor-pointer"
        @click="goToCreate"
      >
        <div
          class="bg-[#fafafa] rounded-2xl justify-start items-center gap-1 flex hover:bg-[#ededed]"
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
                d="M5.39995 19H6.37495L16.65 8.725L15.675 7.75L5.39995 18.025V19ZM18.15 8.225L16.175 6.25L17.35 5.075C17.4833 4.94167 17.65 4.875 17.85 4.875C18.05 4.875 18.2166 4.94167 18.35 5.075L19.325 6.05C19.4583 6.18333 19.525 6.35 19.525 6.55C19.525 6.75 19.4583 6.91667 19.325 7.05L18.15 8.225ZM5.44995 19.7C5.23328 19.7 5.05412 19.6292 4.91245 19.4875C4.77078 19.3458 4.69995 19.1667 4.69995 18.95V18.025C4.69995 17.925 4.71662 17.8333 4.74995 17.75C4.78328 17.6667 4.84162 17.5833 4.92495 17.5L15.675 6.75L17.65 8.725L6.89995 19.475C6.81662 19.5583 6.73328 19.6167 6.64995 19.65C6.56662 19.6833 6.47495 19.7 6.37495 19.7H5.44995ZM16.15 8.225L15.675 7.75L16.65 8.725L16.15 8.225Z"
                fill="#333333"
              />
            </svg>
          </div>
        </div>
      </div>
    </div>
    <div class="self-stretch h-7 justify-start items-start gap-2 inline-flex">
      <div class="grow shrink basis-0 text-zinc-800 text-xl font-bold">
        {{ selectedItem?.patient?.first_name }}
        {{ selectedItem?.patient?.last_name }}
      </div>
      <div
        class="w-[101.38px] text-right text-black text-opacity-20 text-2xl font-bold"
      >
        {{ selectedItem?.patient?.patient_number }}
      </div>
    </div>
    <div class="self-stretch justify-between items-center gap-4 inline-flex">
      <div class="justify-start items-center gap-1 flex">
        <img class="w-3.5 h-3.5 rounded-[14px]" :src="doctor" />
        <div class="text-black text-xs font-normal">Labor Wunderheilung</div>
      </div>
      <div class="justify-start items-center gap-1 flex">
        <img
          class="w-3.5 h-3.5 rounded-[14px]"
          :src="dentistItem?.profile_image"
        />
        <div v-if="dentistItem" class="text-black text-xs font-normal">
          Dr. {{ dentistItem.first_name }}, {{ dentistItem.last_name }}
        </div>
      </div>
    </div>
    <div class="self-stretch text-black text-base font-normal">
      {{ selectedItem?.work_description }}
    </div>
    <div
      class="self-stretch h-fit p-4 bg-[#ededed] rounded-lg flex-col justify-start items-start gap-2 flex"
    >
      <div class="self-stretch text-black text-xs font-bold">
        Eingereichte Unterlagen:
      </div>
      <div class="self-stretch justify-start items-center gap-2 inline-flex">
        <img class="w-10 h-10" src="/images/rectangle.png" />
        <div
          class="grow shrink basis-0 flex-col justify-center items-start gap-1 inline-flex"
        >
          <div class="text-black text-sm font-bold">File1234.jpg</div>
          <div class="text-black text-opacity-50 text-[8px] font-normal">
            Uploaded: 26.03.2023 22:14 Uhr
          </div>
        </div>
        <div class="w-6 h-6 relative">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
          >
            <path
              d="M12 15.45L8.89999 12.35L9.39999 11.85L11.65 14.1V5.3H12.35V14.1L14.6 11.85L15.1 12.35L12 15.45ZM6.79999 18.7C6.36665 18.7 6.00832 18.5583 5.72499 18.275C5.44165 17.9917 5.29999 17.6333 5.29999 17.2V14.95H5.99999V17.2C5.99999 17.4 6.08332 17.5833 6.24999 17.75C6.41665 17.9167 6.59999 18 6.79999 18H17.2C17.4 18 17.5833 17.9167 17.75 17.75C17.9167 17.5833 18 17.4 18 17.2V14.95H18.7V17.2C18.7 17.6333 18.5583 17.9917 18.275 18.275C17.9917 18.5583 17.6333 18.7 17.2 18.7H6.79999Z"
              fill="black"
            />
          </svg>
        </div>
      </div>
      <div class="self-stretch justify-start items-center gap-2 inline-flex">
        <img class="w-10 h-10" src="/images/rectangle.png" />
        <div
          class="grow shrink basis-0 flex-col justify-center items-start gap-1 inline-flex"
        >
          <div class="text-black text-sm font-bold">File1234.jpg</div>
          <div class="text-black text-opacity-50 text-[8px] font-normal">
            Uploaded: 26.03.2023 22:14 Uhr
          </div>
        </div>
        <div class="w-6 h-6 relative">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
          >
            <path
              d="M12 15.45L8.89999 12.35L9.39999 11.85L11.65 14.1V5.3H12.35V14.1L14.6 11.85L15.1 12.35L12 15.45ZM6.79999 18.7C6.36665 18.7 6.00832 18.5583 5.72499 18.275C5.44165 17.9917 5.29999 17.6333 5.29999 17.2V14.95H5.99999V17.2C5.99999 17.4 6.08332 17.5833 6.24999 17.75C6.41665 17.9167 6.59999 18 6.79999 18H17.2C17.4 18 17.5833 17.9167 17.75 17.75C17.9167 17.5833 18 17.4 18 17.2V14.95H18.7V17.2C18.7 17.6333 18.5583 17.9917 18.275 18.275C17.9917 18.5583 17.6333 18.7 17.2 18.7H6.79999Z"
              fill="black"
            />
          </svg>
        </div>
      </div>
      <div class="self-stretch justify-start items-center gap-2 inline-flex">
        <img class="w-10 h-10" src="/images/rectangle.png" />
        <div
          class="grow shrink basis-0 flex-col justify-center items-start gap-1 inline-flex"
        >
          <div class="text-black text-sm font-bold">File1234.jpg</div>
          <div class="text-black text-opacity-50 text-[8px] font-normal">
            Uploaded: 26.03.2023 22:14 Uhr
          </div>
        </div>
        <div class="w-6 h-6 relative">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
          >
            <path
              d="M12 15.45L8.89999 12.35L9.39999 11.85L11.65 14.1V5.3H12.35V14.1L14.6 11.85L15.1 12.35L12 15.45ZM6.79999 18.7C6.36665 18.7 6.00832 18.5583 5.72499 18.275C5.44165 17.9917 5.29999 17.6333 5.29999 17.2V14.95H5.99999V17.2C5.99999 17.4 6.08332 17.5833 6.24999 17.75C6.41665 17.9167 6.59999 18 6.79999 18H17.2C17.4 18 17.5833 17.9167 17.75 17.75C17.9167 17.5833 18 17.4 18 17.2V14.95H18.7V17.2C18.7 17.6333 18.5583 17.9917 18.275 18.275C17.9917 18.5583 17.6333 18.7 17.2 18.7H6.79999Z"
              fill="black"
            />
          </svg>
        </div>
      </div>
    </div>
    <div
      class="self-stretch h-[104px] px-4 py-2 bg-[#ededed] rounded-lg flex-col justify-start items-start gap-2 flex"
    >
      <div class="self-stretch justify-start items-center gap-2 inline-flex">
        <div
          class="grow shrink basis-0 text-black text-opacity-75 text-xs font-bold"
        >
          Eingereichte Unterlagen:
        </div>
        <div class="w-6 h-6 relative bg-white rounded-2xl">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
          >
            <rect width="24" height="24" rx="12" fill="white" />
            <path
              d="M11.65 12.35H6.30005V11.65H11.65V6.3H12.35V11.65H17.7V12.35H12.35V17.7H11.65V12.35Z"
              fill="black"
            />
          </svg>
        </div>
      </div>
      <div
        class="self-stretch p-4 opacity-25 justify-center items-center gap-2 inline-flex"
      >
        <div class="w-6 h-6 relative">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="25"
            height="24"
            viewBox="0 0 25 24"
            fill="none"
          >
            <path
              d="M6.99999 18.7C5.83332 18.7 4.84165 18.2935 4.02499 17.4806C3.20832 16.6677 2.79999 15.6742 2.79999 14.5C2.79999 13.35 3.21249 12.3625 4.03749 11.5375C4.86249 10.7125 5.79999 10.3 6.84999 10.3C7.01665 8.86667 7.63749 7.675 8.71249 6.725C9.78749 5.775 11.05 5.3 12.5 5.3C14.0878 5.3 15.4348 5.85303 16.5409 6.9591C17.647 8.06518 18.2 9.41215 18.2 11V12.3H19C19.9 12.3 20.6583 12.6083 21.275 13.225C21.8917 13.8417 22.2 14.6 22.2 15.5C22.2 16.4 21.9 17.1583 21.3 17.775C20.7 18.3917 19.95 18.7 19.05 18.7H13.65C13.2167 18.7 12.8583 18.5583 12.575 18.275C12.2917 17.9917 12.15 17.6333 12.15 17.2V11.2L9.89999 13.45L9.39999 12.975L12.5 9.875L15.6 12.975L15.1 13.45L12.85 11.2V17.2C12.85 17.4 12.9333 17.5833 13.1 17.75C13.2667 17.9167 13.45 18 13.65 18H19C19.7 18 20.2917 17.7583 20.775 17.275C21.2583 16.7917 21.5 16.2 21.5 15.5C21.5 14.8 21.2583 14.2083 20.775 13.725C20.2917 13.2417 19.7 13 19 13H17.5V11C17.5 9.61667 17.0125 8.4375 16.0375 7.4625C15.0625 6.4875 13.8833 6 12.5 6C11.1167 6 9.93749 6.4875 8.96249 7.4625C7.98749 8.4375 7.49999 9.61667 7.49999 11H6.94999C6.03332 11 5.22915 11.3417 4.53749 12.025C3.84582 12.7083 3.49999 13.5333 3.49999 14.5C3.49999 15.4667 3.84165 16.2917 4.52499 16.975C5.20832 17.6583 6.03332 18 6.99999 18H9.49999V18.7H6.99999Z"
              fill="black"
            />
          </svg>
        </div>
        <div class="text-black text-sm font-bold">Hier hochladen</div>
      </div>
    </div>
  </div>
</template>

<script>
import doctorImage from 'assets/doctor.png';

export default {
  name: 'RainerComponent',

  data() {
    return {
      doctor: doctorImage,
    };
  },

  props: {
    selectedItem: Object, // Added new prop to receive the selected item
    dentistItem: Object,
  },

  watch: {
    dentistItem: {
      handler: function (val) {
        console.log('dentistItem changed to!!!!!!!!!!!!!!!!!!:', val);
      },
      deep: true,
    },
  },

  methods: {
    goToCreate() {
      this.$emit('changeComponent', 'CreateComponent');
    },
  },
};
</script>
