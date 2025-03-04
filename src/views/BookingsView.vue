<template>
  <div class="p-6 max-w-lg mx-auto">
    <h1 class="text-2xl font-bold mb-4">Select a Booking Date</h1>
    
    <!-- Date Picker -->
    <input 
      type="date" 
      v-model="selectedDate" 
      class="border p-2 rounded w-full mb-4" 
      @change="fetchAvailableSlots"
    />
    
    <!-- Time Slots -->
    <div v-if="loading" class="text-center text-gray-500">Loading...</div>
    <ul v-else-if="timeSlots.length" class="space-y-2">
      <li 
        v-for="slot in timeSlots" 
        :key="slot" 
        class="p-3 bg-blue-500 text-white rounded cursor-pointer hover:bg-blue-600">
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