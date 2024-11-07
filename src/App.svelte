<script>
	let list1 = ['Item 1', 'Item 2', 'Item 3'];
	let list2 = ['Item 4', 'Item 5', 'Item 6'];
  
	function handleDragStart(event, item) {
	  event.dataTransfer.setData('text/plain', item);
	}
  
	function handleDrop(event, targetList) {
	  event.preventDefault();
	  const item = event.dataTransfer.getData('text/plain');
	  if (item) {
		if (targetList === 'list1') {
		  list1.push(item);
		  list2 = list2.filter(i => i !== item);
		} else {
		  list2.push(item);
		  list1 = list1.filter(i => i !== item);
		}
	  }
	}
  
	function handleDragOver(event) {
	  event.preventDefault();
	}
  </script>
  
  <style>
	.container {
	  display: flex;
	  justify-content: space-around;
	}
  
	.list {
	  width: 200px;
	  padding: 10px;
	  border: 1px solid #ccc;
	  margin: 20px;
	  display: inline-block;
	  vertical-align: top;
	}
  
	.list-item {
	  padding: 8px;
	  margin: 5px 0;
	  background-color: #f0f0f0;
	  cursor: grab;
	  border: 1px solid #ccc;
	}

  </style>
  
  <div class="container">
	<div class="list" on:dragover={handleDragOver} on:drop={(e) => handleDrop(e, 'list1')}>
	  <h3>List 1</h3>
	  {#each list1 as item}
		<div 
		  class="list-item" 
		  draggable="true" 
		  on:dragstart={(e) => handleDragStart(e, item)}
		>
		  {item}
		</div>
	  {/each}
	</div>
  
	<div class="list" on:dragover={handleDragOver} on:drop={(e) => handleDrop(e, 'list2')}>
	  <h3>List 2</h3>
	  {#each list2 as item}
		<div 
		  class="list-item" 
		  draggable="true" 
		  on:dragstart={(e) => handleDragStart(e, item)}
		>
		  {item}
		</div>
	  {/each}
	</div>
  </div>
  