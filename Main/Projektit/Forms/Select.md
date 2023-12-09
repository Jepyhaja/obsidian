# Select input
Component for selectin one or many values from a list. Use with ['id' => 'name'] to use with database attaching. ^1

```php
<div {{ $attributes->only(['class']) }}>
 	<div class="flex items-center justify-between w-full">
 		<label class="inline-block py-1 pl-2 text-sm font-semibold text-gray-100" for="{{ $id }}">{{ $slot }}</label>
 		@error($id)
 			<div class="inline-block text-xs text-pink-500">
 				<span>{{ $message }}</span>
 			</div>
 		@enderror
 	</div>
 	<select @class([
			"w-full p-1 text-white bg-gray-600 border-2 border-white rounded-lg",
			"w-full p-1 text-white bg-gray-600 border-2 border-pink-500 rounded-lg" => $errors->has($id)
		])
		name="{{ $id }}" wire:model="{{ $id }}" {{ $attributes->only(['placeholder', 'id', 'value', 'readonly', 'disabled', 'required', 'autofocus', 'default']) }}>
 	@foreach ($options as $option_key => $option)
	 	<option value="{{ $option_key }}">{{ $option }}</option>
 	@endforeach
 	</select>
</div>

```