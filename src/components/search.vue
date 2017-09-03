<template>
  <div class="search">
    <span class="search__input input-group">
      <input class="input-group__field" type="text">
      <span class="input-group__icon"></span>
    </span>

    <button class="search__btn">Поиск</button>
  </div>
</template>

<script>
    export default {
        name: 'search'
    }
</script>

<style lang="scss">
  .search {
    /*display: flex;*/
  }
  .input-group {
    position: relative;
    margin-right: 8px;
    overflow: hidden;
    input {
      padding: 9px 14px;
      padding-left: 30px;
      border: none;
      border-radius: 3px;
      box-shadow: inset 0 0 5px rgba(#000000, 0.16);

      &:focus {
        outline: none;
        box-shadow: 0 0 5px rgba(#000000, 0.16);
      }
    }
  }
  .search__btn {
    padding: 9px 14px;
    border: none;
    border-radius: 3px;
    background-color: #17709a;
    color: #ffffff;
    text-transform: uppercase;
  }
</style>