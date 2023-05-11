<script>
async function name(){
let link = "https://data.cityofnewyork.us/resource/fcau-jc6k.json"
let response = await fetch(link)
return await response.json()
}
export let dataBIG = name
</script>