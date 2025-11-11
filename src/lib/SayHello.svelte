<script>
  let person = $state({
    firstName: "",
    lastName: "",
  });

  let showGreeting = $state(false);

  function sayHello() {
    showGreeting = true;
  }
</script>

<div>
  <input
    type="text"
    id="firstName"
    placeholder="First Name"
    bind:value={person.firstName}
  /><br />
  <input
    type="text"
    id="lastName"
    placeholder="Last Name"
    bind:value={person.lastName}
  /><br />
  <button onclick={sayHello}>Say Hello</button>

  {#if showGreeting}
    <h1>Hello {person.firstName} {person.lastName}</h1>
  {/if}
</div>
