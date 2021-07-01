<script>
    import { createEventDispatcher } from "svelte";

    let dispath = createEventDispatcher();

    let name;
    let beltColour;
    let age;

    let aguador = false;
    let running = false;

    let skills = [];

    const handleSubmit = () => {
        const person1 = {
            name: name,
            beltColour: beltColour,
            age,
            skills: skills,
            id: Math.random(),
        };
        dispath("addPerson", person1);
        console.log(name, beltColour, age, aguador, running, skills);
    };
</script>

<h3>Add a new person</h3>
<form on:submit|preventDefault={handleSubmit}>
    <input type="text" placeholder="name" bind:value={name} />
    <input type="text" placeholder="belt colour" bind:value={beltColour} />
    <input type="number" placeholder="age" bind:value={age} />
    <label>Skills:</label>
    <!-- <input type="checkbox" checked={true} />lucha<br />
    <input type="checkbox" bind:checked={aguador} />agua<br />
    <input type="checkbox" bind:checked={running} />running<br /> -->
    <input type="checkbox" bind:group={skills} value="luchador" />lucha<br />
    <input type="checkbox" bind:group={skills} value="aguador" />agua<br />
    <input type="checkbox" bind:group={skills} value="running" />running<br />
    <label>Belt Colour:</label>
    <select bind:value={beltColour}>
        <option value="black">black</option>
        <option value="orange">orange</option>
        <option value="red">red</option>
        <option value="yellow">yellow</option>
    </select>
    <button>Add Person</button>
</form>
