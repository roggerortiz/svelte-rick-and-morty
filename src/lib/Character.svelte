<script>
   export let character
</script>

<div class="card text-bg-dark h-100">
   <img
     src={character.image}
     class="card-img-top"
     alt={character.name}
   />
   <div class="card-body p-1 text-center">
     <small class="card-title m-0">{character.name}</small>
   </div>
 </div>