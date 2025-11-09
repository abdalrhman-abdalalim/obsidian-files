<button
  onClick={isDisabled ? undefined : handleClick}
  className={isDisabled ? 'opacity-50 cursor-not-allowed' : 'cursor-pointer'}
>
  Click me
</button>