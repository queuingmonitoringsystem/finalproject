<script lang="ts">
    import { Card, Button, Label, Input, Checkbox } from 'flowbite-svelte';
  
    interface Queue {
      createdAt?: Date;
      id?: number;
      name?: string;
      status?: boolean; // 0: waiting, 1: serving, 2: served
    }
  
    let queues: Queue[] = [];
    const API_URL = "https://675a496f099e3090dbe4271e.mockapi.io/queue";
  
    let servingNow: Queue | null = null;
    let nextQueueId: number | null = null;
    let falseStatusCount: number = 0;
  
    // Fetch queues from the API
    const fetchQueues = async () => {
      try {
        const response = await fetch(API_URL);
        const fetchedQueues: Queue[] = await response.json();
        queues = fetchedQueues; // Assign the fetched data to queues array
  
        // Find the queue that is currently being served
        servingNow = queues.find((queue) => queue.status === true) || null;
        
        // Call function to count the queues with status false
        countFalseStatusQueues();
  
        // If there's a currently serving queue, parse the id and calculate the next queue ID
        if (servingNow) {
          const currentQueueId = Number(servingNow.id);
          nextQueueId = currentQueueId + 1;
        } else {
          nextQueueId = null; // No queue is currently being served
        }
  
      } catch (err) {
        console.error("Error fetching queues:", err);
      }
    };
  
    // Mark the current queue as served and move to the next
    const serveNext = async () => {
      if (servingNow && typeof servingNow.id === "number") {
        // Mark the current serving queue as not serving (status = 0)
        await updateQueueStatus(servingNow.id, 0);
      }
  
      // Get the next queue to serve
      const nextQueue = queues.find((queue) => queue.status === false);
      if (nextQueue && typeof nextQueue.id === "number") {
        // Mark the next queue as serving (status = 1)
        await updateQueueStatus(nextQueue.id, 1);
        servingNow = nextQueue;
      } else {
        servingNow = null;
      }
    };
  
    // Update queue status on the API
    const updateQueueStatus = async (id: number, status: number) => {
      try {
        await fetch(`${API_URL}/${id}`, {
          method: "PUT",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ status }),
        });
        // Refresh queue data
        fetchQueues();
      } catch (err) {
        console.error("Error updating queue status:", err);
      }
    };
  
    // Count queues with false status
    const countFalseStatusQueues = () => {
      falseStatusCount = queues.filter(queue => queue.status === false).length;
    };
  
    // Fetch queues when the component is mounted
    fetchQueues();
  </script>
  
  <div class="mt-9">
    <div class="space-x-4 flex gap-0">
      <Card class="ml-6 size-96 bg-gray-100">
        <div class="flex flex-col space-y-6">
          <div class="text-center">
            <h2 class="text-xl font-medium text-gray-900 dark:text-white text-center">SERVING NOW</h2>
            {#if servingNow}
              <h1 class="text-8xl text-center mt-10 text-lime-900 font-bold">{servingNow.id}</h1>
              <p class="mt-9">SwiftServe is ready to serve you:</p>
              <p class="text-1xl text-center mt-1 text-white bg-lime-900 rounded-xl">{servingNow.name}</p>
            {:else}
              <h1 class="text-8xl text-center mt-10 text-lime-900 font-bold">No Queue</h1>
              <p class="mt-9">Please wait for the next queue.</p>
            {/if}
          </div>
        </div>
      </Card>
  
      <div class="relative grid grid-cols-2 gap-3 p-0">
        <Card class="bg-lime-900">
          <h1 class="mb-2 mt-4 text-6xl text-center tracking-tight text-white dark:text-white">{nextQueueId !== null ? nextQueueId : 'No queue being served'}</h1>
          <p class="font-normal text-center text-white dark:text-gray-400 leading-tight">Upcoming Number</p>
        </Card>
  
        <Card class="bg-gray-200">
          <h5 class="mb-2 mt-4 text-center text-6xl tracking-tight text-gray-900 dark:text-white">{falseStatusCount}</h5>
          <p class="font-normal text-center text-gray-700 dark:text-gray-400 leading-tight">Number of Queues</p>
        </Card>
  
        <Card href="/cards">
          <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Noteworthy technology acquisitions 2021</h5>
          <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">Here are the biggest enterprise technology acquisitions of 2021 so far, in reverse chronological order.</p>
        </Card>
  
        <Card href="/cards">
          <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">Noteworthy technology acquisitions 2021</h5>
          <p class="font-normal text-gray-700 dark:text-gray-400 leading-tight">Here are the biggest enterprise technology acquisitions of 2021 so far, in reverse chronological order.</p>
        </Card>
      </div>
    </div>
  </div>
  