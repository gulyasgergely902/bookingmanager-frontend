<template>
  <div class="p-6 max-w-lg mx-auto">
    <h1 class="text-2xl font-bold mb-4">Bookings</h1>
    
    <fieldset class="fieldset w-xs bg-base-200 border border-base-300 p-4 rounded-box">
        <legend class="fieldset-legend">Date</legend>
        <input type="date" v-model="selectedDate" class="border p-2 rounded w-full mb-4" @change="fetchAvailableSlots"/>
        <p class="fieldset-label">Choose a date for the booking.</p>
    </fieldset>
    <div class="divider"></div>
    <span v-if="loading" class="loading loading-spinner loading-md"></span>
    <ul v-else-if="timeslot_count > 0" class="list bg-base-100 rounded-box shadow-md">
        <li class="p-4 pb-2 text-xs opacity-60 tracking-wide">Available time slots</li>
        <li v-for="slot in timeslots" :key="slot.id" class="list-row">
            <ListItem :date=slot.date :time=slot.time :duration=slot.duration />
        </li>
    </ul>
    <div v-else class="text-gray-500">No slots available for this date.</div>
  </div>
</template>

<script setup lang="ts">
    import ListItem from '../components/ListItem.vue';
    import { ref, onMounted } from 'vue';
    import axios from 'axios';

    const today = new Date().toISOString().split("T")[0];
    const selectedDate = ref(today);

    const loading = false;

    const timeslot_count = ref(0);
    interface Timeslot {
      id: number;
      date: string;
      time: string;
      duration: number;
      available: number;
    }

    const timeslots = ref<Timeslot[]>([]);

    const fetchAvailableSlots = async () => {
      try {
        const response = await axios.get(`http://127.0.0.1:5000/bookings?date=${selectedDate.value}`);
        if (response.data && response.data.slots) {
          timeslot_count.value = response.data.count;
          timeslots.value = response.data.slots;
        } else {
          console.error("Unexpected response structure: ", response.data);
          timeslots.value = [];
        }
      } catch (error) {
        console.error("Error fetching timeslots; Error: ", error);
      }
    };

    onMounted(async () => {
      await fetchAvailableSlots();
    });
</script>

<style>
  * {
    font-family: "Space Grotesk", sans-serif;
  }
</style>