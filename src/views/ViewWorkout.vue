<template>
  <div></div>
</template>

<script>
import { ref } from "vue";
import { supabase } from "../supabase/init";
import { useRoute } from "vue-router";

export default {
  name: "view-workout",
  setup() {
    // Create data / vars
    const data = ref(null);
    const dataLoaded = ref(null);
    const errorMsg = ref(null);
    const statusMsg = ref(null);
    const route = useRoute();

    // Get current Id of route
    const currentId = route.params.workoutId;

    // Get workout data
    const getData = async () => {
      try {
        const { data: workouts, error } = await supabase
          .from("workouts")
          .select("*")
          .eq("id", currentId);
        data.value = workouts;
        dataLoaded.value = true;
        console.log(data.value);
        if (error) throw error;
      } catch (error) {
        errorMsg.value = error.message;
        setTimeout(() => {
          errorMsg.value = null;
        }, 5000);
      }
    };

    getData();

    // Delete workout

    // Edit mode

    // Add exercise

    // Delete exercise

    // Update Workout

    return { data, dataLoaded, errorMsg, statusMsg };
  }
};
</script>
