<script>
  import { getContext } from "svelte"

  const { styleable, Provider } = getContext("sdk")
  const component = getContext("component")
  export let inactiveColor;
  export let activeColor;
  export let inaccentColor;
  export let accentColor;
  export let onActive;
  export let onInActive;
  export let defaultValue;
  export let isDisabled;

  let isActive = defaultValue;
  $: dataContext = {
    isActive
  }
  const handleButtonClick = () => {
    if(isDisabled) return;
    
    isActive = !isActive;
    if(isActive) {
      onActive();
    } else {
      onInActive();
    }
  };
</script>

<div use:styleable={$component.styles}>
  <Provider data={dataContext}>
    <div class="toggle">
      <div style="background: {isActive ? activeColor : inactiveColor};" class="toggle-button {isActive && 'toggle-button-active'}" on:click={handleButtonClick}>
        <div style="background: {isActive ? accentColor: inaccentColor};" class="toggle-inner-circle {isActive && 'toggle-inner-circle-active'}">
        </div>
      </div>
    </div>
    <slot />
  </Provider>
</div>

<style>

  .toggle{
    display: flex;
    position: relative;
    left: 50%;
    transform: translate(-50%);
  }


  .toggle-button {
    width: 60px;
    height: 35px;
    border-radius: 30px;
    padding: 5px;
    transition: all 200ms ease-in-out;
  }

  .toggle-button > .toggle-inner-circle {
    width: 25px;
    height: 25px;
    border-radius: 50%;
    transition: all 200ms ease-in-out;
  }

  .toggle-inner-circle-active {
    margin-left: 25px;
  }


</style>