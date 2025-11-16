<script>
  import UserRow from "./UserRow.svelte";

  const user = {
    id: "1",
    name: "John",
    address: "Bandung",
  };
</script>

<table>
  <thead>
    <tr>
      <th>Id</th>
      <th>Name</th>
      <th>Address</th>
    </tr>
  </thead>
  <tbody>
    <UserRow {...user} />
  </tbody>
</table>
