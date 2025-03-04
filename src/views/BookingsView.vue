<template>
  <div class="p-6 max-w-lg mx-auto">
    <h1 class="text-2xl font-bold mb-4">Booking</h1>
    
    <fieldset class="fieldset w-xs bg-base-200 border border-base-300 p-4 rounded-box">
        <legend class="fieldset-legend">Date</legend>
        <input type="date" v-model="selectedDate" class="border p-2 rounded w-full mb-4" @change="fetchAvailableSlots"/>
        <p class="fieldset-label">Choose a date for the booking.</p>
    </fieldset>
    <div class="divider"></div>
    <span v-if="loading" class="loading loading-spinner loading-md"></span>
    <ul v-else-if="timeSlots.length" class="list bg-base-100 rounded-box shadow-md">
        <li class="p-4 pb-2 text-xs opacity-60 tracking-wide">Available time slots</li>
        <li v-for="slot in timeSlots" :key="slot" class="list-row">
            {{ slot }}
        </li>
    </ul>
    <div v-else class="text-gray-500">No slots available for this date.</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedDate: new Date().toISOString().split('T')[0],
      timeSlots: [],
      loading: false,
    };
  },
  methods: {
    async fetchAvailableSlots() {
      if (!this.selectedDate) return;
      
      this.loading = true;
      // Simulating API call
      setTimeout(() => {
        this.timeSlots = this.getMockTimeSlots();
        this.loading = false;
      }, 1000);
    },
    getMockTimeSlots() {
      // Simulating available slots based on the selected date
      const slots = ["09:00 AM", "10:30 AM", "01:00 PM", "02:45 PM", "04:15 PM"];
      return Math.random() > 0.3 ? slots : []; // Sometimes return empty slots for realism
    }
  },
  mounted() {
    this.fetchAvailableSlots();
  }
};
</script>

<style>

</style>