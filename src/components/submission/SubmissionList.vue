<script setup lang="ts">
import { ref, onMounted } from "vue";
import { useUrlStore } from "../../stores/url";

const items = ref([]);
/*const headers = reactive([
  { text: "#", value: "id" },
  { text: "User", value: "usernmae" },
  { text: "Problem", value: "problem_id" },
  { text: "Result", value: "result" },
  { text: "Time", value: "time_cost" },
  { text: "Memory", value: "memory_cost" },
  { text: "Submission Time", value: "submission_time" },
]);*/

const submissions_url = useUrlStore().submissions_url;
onMounted(async () => {
  submissions_url.searchParams.set("offset", "0");
  const resp = await fetch(submissions_url);
  const data = await resp.json();
  items.value = data.submissions;
  console.log(data);
});

/*function get_color(result: string): string {
  switch (result) {
    case "Accepted":
      return "green";
    case "Failed":
      return "error";
    case "Compile Error":
      return "warning";
  }
  return "grey";
}*/
</script>

<template>
  <v-container fluid style="padding-left: 6vw; padding-right: 6vw">
    <v-card>
      <v-card-title class="text-h4 text--primary"> Submissions </v-card-title>
      <v-card-text>
        <!-- <v-data-table :headers="headers" :items="items">
          <template v-slot:item.result="{ item }">
            <v-chip :color="get_color(item.result)" outlined>
              {{ item.result }}
            </v-chip>
          </template>
        </v-data-table> -->
      </v-card-text>
    </v-card>
  </v-container>
</template>