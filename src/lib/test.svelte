<script lang="ts">
    const API_URL = "https://675a496f099e3090dbe4271e.mockapi.io/queue";
  
    // Function to update the status of a specific queue by ID
    const updateQueueStatus = async (id: number, status: boolean) => {
      try {
        const response = await fetch(`${API_URL}/${id}`, {
          method: "PUT",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ status }),
        });
  
        if (response.ok) {
          console.log(`Queue with ID ${id} updated to status: ${status}`);
        } else {
          console.error(`Failed to update queue with ID ${id}`);
        }
      } catch (err) {
        console.error(`Error updating status for queue ID ${id}:`, err);
      }
    };
  
    // Function triggered by the button
    const setQueue2ToTrue = async () => {
      await updateQueueStatus(3, true);
    };
  </script>
  
  <div>
    <button
      on:click={setQueue2ToTrue}
      class="px-4 py-2 bg-blue-500 text-white font-bold rounded hover:bg-blue-600"
    >
      Set ID 2 Status to True
    </button>
  </div>
  