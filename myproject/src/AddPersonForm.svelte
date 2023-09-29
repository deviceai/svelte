<script>
    import {createEventDispatcher} from 'svelte';
    let dispatch = createEventDispatcher();
    export let showAddPersonForm = false;
    let name;
    let beltcolor;
    let age;

    let some;
    // let fighting = false;
    // let sneaking = false;
    // let running = false;

    let skills = []

    const handleSubmit = () =>{
        // console.log(name, beltcolor, age, fighting, sneaking, running);
        // console.log(name, beltcolor, age, skills);
        const person = {
            name,
            beltcolor,
            age,
            skills,
            id: Math.random()
        };
        dispatch('addPerson', person);
    };
</script>
{#if showAddPersonForm}
<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="backdrop"  on:click|self>
    <div class="modal">
        <div>
            <h3>Add new person</h3>
            <form on:submit|preventDefault={handleSubmit}>
                <input type="text" placeholder="name" bind:value={name}>
                <input type="text" placeholder="belt color" bind:value={beltcolor}>
                <input type="number" placeholder="age" bind:value={age}>
                <!-- svelte-ignore a11y-label-has-associated-control -->
                <label>Skills:</label>
                <!-- <input type="checkbox" bind:checked={fighting}> fighting<br>
                <input type="checkbox" bind:checked={sneaking}> sneaking<br>
                <input type="checkbox" bind:checked={running}> running<br> -->

                <!-- group binding -->
                <input type="checkbox" bind:group={skills} value = "fighting"> fighting<br>
                <input type="checkbox" bind:group={skills} value = "sneaking"> sneaking<br>
                <input type="checkbox" bind:group={skills} value = "running"> running<br>

                <!-- svelte-ignore a11y-label-has-associated-control -->
                <label>Belt color:</label>
                <select bind:value={beltcolor}>
                    <option value="black">black</option>
                    <option value="red">red</option>
                </select>
                <button>Add person</button>
            </form>
        </div>
    </div>
</div>
{/if}

<style>
.backdrop{
    width: 100%;
    height: 100%;
    position: fixed;
    background: rgba(0, 0, 0, 0.8);
}
.modal{
    padding: 10px;
    border-radius: 10px;
    max-width: 400px;
    margin: 10% auto;
    text-align: center;
    background: white ;
}
/* .promo .modal {
    background: crimson;
    color: white;
} */
</style>