Textarea component that follows the same conventions as the [[Input]] ^1

```html
<div {{ $attributes->only(['class']) }}>
	<label class="inline-block py-1 pl-2 text-sm font-semibold text-gray-100" for="{{ $id }}">{{ $slot }}</label>
	<textarea class="w-full p-1 text-white bg-gray-600 border-2 border-white rounded-lg" type="{{ $type ?? 'text' }}" name="{{ $id }}" {{ $attributes->only(['placeholder', 'id', 'readonly', 'disabled', 'required', 'autofocus', 'cols', 'rows']) }} wire:model="{{ $id }}">
	</textarea>

	@error($id)
		<div class="alert">
			<span>{{ $message }}</span>
		</div>
	@enderror
</div>
```