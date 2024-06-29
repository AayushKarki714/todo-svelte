<script>
  export let status;
</script>

<select bind:value={status}>
  <option value="">Status</option>
  <option value={true}>Completed</option>
  <option value={false}>Not Completed</option>
</select>
