# Requirements
Basic input used for everything except, [[CheckBox]]-input ^1
-	Laravel 8.x for @class directive

```html
<div {{ $attributes->only(['class']) }}>
	<div class="flex items-center justify-between w-full">
		<label class="inline-block py-1 pl-2 text-sm font-semibold text-gray-100" for="{{ $id }}">{{ $slot }}</label>
		@error($id)
 			<div class="inline-block text-xs text-pink-500">
 				<span>{{ $message }}</span>
 			</div>
		@enderror
 	</div>
	<input @class([
			"w-full p-1 text-white bg-gray-600 border-2 border-white rounded-lg",
			"w-full p-1 text-white bg-gray-600 border-2 border-pink-500 rounded-lg" => $errors->has($id)
 		])
 		type="{{ $type ?? 'text' }}" name="{{ $id }}" {{ $attributes->only(['min', 'max', 'placeholder', 'id', 'value', 'readonly', 'disabled', 'required', 'autofocus']) }} wire:model="{{ $id }}"/>
</div>
```