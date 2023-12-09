# Variants
[[Input]]-variant used specifically for type -> checkbox, has 2 variants base and [[Toggle]] ^1

## Animated Toggle
![[Toggle#^1]] ^32496b

## Base variant:

```php
<div {{ $attributes->only(['class']) }}>
	<label for="{{ $id }}">
		<input type="{{ $type }}" {{ $attributes->only(['name', 'id', 'value', 'readonly', 'disabled', 'required', 'autofocus']) }} wire:model="{{ $id }}"/>
		 {{ $slot }}
	</label>
	{{-- Error msg box --}}
	@error($id)
		<div class="alert">
			<span>{{ $message }}</span>
		</div>
	@enderror
</div>
```