<script lang="ts">
  export let turn:number;
  export let current_sign:string;
  export let wins:any;

  let fields:string[] = ['','','','','','','','','']

  function placeSign(i:number) {
    if(fields[i] == '') {
      // This animation can be removed - cause it kinda sucks
      document.getElementById('span-'+i.toString())?.animate(
        [{opacity: 0}, {opacity: 1}],
        {
          easing: "ease",
          duration: 120
        },
      ).play();

      fields.splice(i, 1, current_sign);
      fields = fields;
      turn+=1;

      checkWin();
      if(turn > 9+wins.x+wins.o) {
        console.log("checkmate");
        reset();
      }
    } 
  }

  function checkWin() {
    if((fields[0] == 'X' && fields[1] == 'X' && fields[2] == 'X')||
       (fields[3] == 'X' && fields[4] == 'X' && fields[5] == 'X')||
       (fields[6] == 'X' && fields[7] == 'X' && fields[8] == 'X')||
       (fields[0] == 'X' && fields[3] == 'X' && fields[6] == 'X')||
       (fields[1] == 'X' && fields[4] == 'X' && fields[7] == 'X')||
       (fields[2] == 'X' && fields[5] == 'X' && fields[8] == 'X')||
       (fields[0] == 'X' && fields[4] == 'X' && fields[8] == 'X')||
       (fields[2] == 'X' && fields[4] == 'X' && fields[6] == 'X')||
       
       (fields[0] == 'O' && fields[1] == 'O' && fields[2] == 'O')||
       (fields[3] == 'O' && fields[4] == 'O' && fields[5] == 'O')||
       (fields[6] == 'O' && fields[7] == 'O' && fields[8] == 'O')||
       (fields[0] == 'O' && fields[3] == 'O' && fields[6] == 'O')||
       (fields[1] == 'O' && fields[4] == 'O' && fields[7] == 'O')||
       (fields[2] == 'O' && fields[5] == 'O' && fields[8] == 'O')||
       (fields[0] == 'O' && fields[4] == 'O' && fields[8] == 'O')||
       (fields[2] == 'O' && fields[4] == 'O' && fields[6] == 'O')
    ) {
      if(current_sign == 'X')
        wins.x++;
      else  
        wins.o++;
      
      console.log(current_sign, 'has won');
      reset();
    }
  }

  function reset() {
    // Same here - can be removed
    document.querySelectorAll('span').forEach(el => { 
      el?.animate(
        [{opacity: 1}, {opacity: 0}],
        {
          easing: "ease",
          duration: 80
        },
      ).play();
    })
    
    // If you remove the animations remember to also remove this 
    setTimeout(() => {
      fields = ['','','','','','','','',''];
      turn=1+wins.x+wins.o;
      console.log('help')
    },50) 
  }

</script>

{#each fields as field, id}
  <button on:click={() => placeSign(id)} id={id.toString()}><span id="span-{id}">{field}</span></button>
{/each}

<style>
  button {
    all:unset;
    text-align: center;
    font-size: 50px;
    width: var(--field-size);
    height: var(--field-size);
    background-color: var(--bg-color);
    user-select: none;
  }
</style>