<script>
    const fetchBieres = async () => {
    try {
      const response = await fetch(`https://api.sampleapis.com/beers/${type}`);
      const data = await response.json();
      bieres.value = data;
    } catch (error) {
      console.error(error);
    }
}  

export default
</script>
