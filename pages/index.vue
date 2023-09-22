<template>
  <div>

  </div>
</template>
<script>
const marvel = {
  render: () => {
    const urlAPI = '';
    let contentHTML = '';

    fetch(urlAPI)
      .then(res => res.json())
      .then((json) => {
        console.log(json, 'RES.JSON');
      })
  }
};
marvel.render

</script>