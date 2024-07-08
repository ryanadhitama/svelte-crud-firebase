<!-- src/routes/index.svelte -->
<script>
	import { collection, getDocs } from "firebase/firestore";
    import { db } from "../firebase";
    import { onMount } from "svelte";
  
    let items = [];
  
    onMount(async () => {
        const ref = collection(db, "tasks");
        const snapshot = await getDocs(ref);
        items = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
    });

  </script>
  
  <div class="container mx-auto mt-8 max-w-[560px]">
  <h1 class="text-2xl font-bold mb-4">Items</h1>
  <a href="/create" class="text-blue-500 hover:underline mb-4 inline-block">Create Item</a>
  <ul class="list-disc pl-5">
    {#each items as item}
      <li class="py-2 flex justify-between w-full">
            <span>
            <strong>{item.name}</strong> - {item.description}
          </span>
          <span class="flex gap-2">
            <a href={`/edit/${item.id}`} class="text-blue-700 underline hover:no-underline">Edit</a>
            <a href={`/edit/${item.id}/delete`} class="text-red-500 underline hover:no-underline">Delete</a>
          </span>
      </li>
    {/each}
  </ul>
  </div>



  
