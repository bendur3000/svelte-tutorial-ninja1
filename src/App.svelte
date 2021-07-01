<script>
    import Modal from "./Modal.svelte";
    import AddPersonForm from "./AddPersonForm.svelte";

    let name = "bendur3000";
    let secondName = "pepito";
    let beltColour = "blue";

    $: fullName = `${name} ${secondName}`;
    $: {
        console.log(beltColour);
    }

    const handleClick = () => {
        beltColour = "red";
    };

    /*const handleInput = (e) => {
        beltColour = e.target.value;
    };*/

    // LOOP
    let people = [
        { name: "pepe", beltColour: "blue", age: 20, id: 1 },
        { name: "antonio", beltColour: "black", age: 42, id: 2 },
        { name: "felipe", beltColour: "red", age: 51, id: 3 },
    ];

    const borrarPersona = (e, id) => {
        people = people.filter((person) => person.id != id);
        console.log(e);
    };

    let num = 3;

    let showModal = false;

    const toggleModal = () => {
        showModal = !showModal;
    };

    const addPerson = (e) => {
        console.log(e.detail);
        const person = e.detail;
        people = [person, ...people];
        showModal = false;
    };
</script>

<Modal message="soy la prop" {showModal} isPromo={true} on:click={toggleModal}>
    <AddPersonForm on:addPerson={addPerson} />
    <div slot="title">
        <h3>slot title</h3>
    </div>
</Modal>
<!--<button on:click={toggleModal}>Open Modal</button>-->
<button on:click|once={toggleModal}>Open Modal</button>

{#if num > 20}
    <p>Mayor a 20</p>
{:else if num > 5}
    <p>Mayot a 5</p>
{:else}
    <p>No es mayor a 5</p>
{/if}

<main>
    <h1>Hello {name}!</h1>
    <p>{fullName}</p>
    <p style="color:{beltColour}">{beltColour} belt</p>
    <button on:click={handleClick}>Cambiar el color</button>
    <!--<input type="text" on:input={handleInput} value={beltColour} />-->
    <input type="text" bind:value={beltColour} />

    <input type="text" bind:value={name} />
    <input type="text" bind:value={secondName} />

    {#each people as person (person.id)}
        <div>
            <h4>{person.name}</h4>
            {#if person.beltColour === "black"}
                <p style="color:{beltColour}"><strong>Master OSO</strong></p>
            {/if}
            <p>{person.age} years old, {person.beltColour} belt</p>
            <button on:click={(e) => borrarPersona(e, person.id)}>Borrar</button
            >
        </div>
    {:else}
        <p>No hay personas</p>
    {/each}
</main>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }

    h1 {
        color: #ff3e00;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 100;
    }

    @media (min-width: 640px) {
        main {
            max-width: none;
        }
    }
</style>
