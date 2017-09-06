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
    display: flex;
  }
  .input-group {
    position: relative;
    display: inline-block;
    width: 312px;
    margin-right: 8px;
    /*overflow: hidden;*/
    input {
      width: 100%;
      height: 100%;
      padding-left: 30px;
      border-radius: 3px;
      border: 1px solid #d5d5d5;
      box-shadow: inset 0 0 5px rgba(#000000, 0.16);

      &:focus {
        outline: none;
        box-shadow: 0 0 5px rgba(#000000, 0.16);
      }
    }
    &__icon {
      position: absolute;
      top: 50%;
      left: 10px;
      transform: translateY(-50%);
      display: inline-block;
      width: 14px;
      height: 14px;
      background-image: url(../assets/search.png);
      background-repeat: no-repeat;
      background-position: 50% 50%;
      background-size: contain;
    }
  }
  .search__btn {
    padding: 8px 14px;
    border: none;
    border-radius: 3px;
    background-color: #17709a;
    color: #ffffff;
    font-size: 12px;
    text-transform: uppercase;
  }
</style>