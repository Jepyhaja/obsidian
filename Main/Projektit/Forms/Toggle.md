# Toggle

Toggle [[CheckBox]] that uses TailwindCSS and some vanilla CSS to render animated transition between on (chekced) and off (unchecked) states. ^1

## Blade component:
```php
<div {{ $attributes->merge(['class' => "flex items-center justify-start w-full py-2"])->only(['class']) }}>
	<label for="{{ $id }}" class="flex items-center cursor-pointer">
 	
	<div class="relative">
		<input type="checkbox" id="{{ $id }}" class="sr-only" {{ $attributes->only(['name', 'id', 'value', 'readonly', 'disabled', 'required', 'autofocus']) }} wire:model="{{ $id }}">
		<div class="block h-8 bg-gray-600 border-2 border-white rounded-full w-14 bg"></div>
		<div class="absolute w-6 h-6 transition bg-gray-100 rounded-full dot left-1 top-1"></div>
	</div>
	
	 <div class="ml-3 font-medium text-white">
	 {{ $slot }}
	 </div>
 
 </label>
</div>
```

## Required CSS:
```css

/* Checkbox toggle visuals */
input:checked ~ .dot {
 transform: translateX(100%);
 @apply bg-purple-700;
}

input:checked ~ .bg {
 @apply border-purple-300;
}

```

^ba2d63
