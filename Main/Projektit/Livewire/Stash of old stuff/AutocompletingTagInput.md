
# Autocompleting Tag Input

Input that creates tag from given autocompleted input values.  ^1

## Blade component:
```php
<div class="relative">
	<div class="relative">
	<input type="text"
 		class="relative w-full py-2 pl-3 pr-10 text-left bg-white border border-gray-300 rounded-md shadow-sm cursor-default focus:outline-none focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
		placeholder="{{ $placeholder }}"
		wire:model="query"
		wire:keydown.escape="hideDropdown"
		wire:keydown.tab="hideDropdown"
		wire:keydown.Arrow-Up="decrementHighlight"
		wire:keydown.Arrow-Down="incrementHighlight"
		wire:keydown.enter.prevent="selectItem"/>
	</div>
	@if(!empty($query) && $showDropdown)
		<div class="absolute z-10 w-full mt-1 bg-white border border-gray-300 rounded-md shadow-lg">
			@if (!empty($items))
				@foreach($items as $i => $item)
					<a wire:click="selectItem({{ $i }})"
						class="block py-1 px-2 text-sm cursor-pointer hover:bg-blue-50 {{$highlightIndex === $i ? 'bg-blue-50' : '' }}">
						{{ $item['name'] }}</a>
				@endforeach
			@else
			<span class="block px-2 py-1 text-sm">No results!</span>
			@endif
		</div>
	@endif
	<div class="flex flex-wrap w-full pt-3 space-x-2 space-y-1.5">
		@foreach ($selectedItems as $selectedItem)
			<div class="transition duration-100 inline-flex px-2 py-1 text-xs text-white bg-purple-500 rounded-md hover:glow-red first:mt-1.5 first:ml-2 border border-purple-500 pointer-events-none">
				{{ $selectedItem['name'] }}
				<span
					class="inline-block ml-1 cursor-pointer pointer-events-auto removeTag hover:text-red-400"
					wire:click="removeItem({{ $selectedItem['id'] }})">
					<i class="fas fa-times"></i>
				</span>
			</div>
		@endforeach
	</div>
</div>
```

## Required Livewire Class example:
```php

<?php
namespace App\Http\Livewire\Autocomplete;

use App\Models\Spell;
use Livewire\Component;
use App\Http\Livewire\Autocomplete\WithAutocomplete;

class PlayerClass extends Component
{
 	use WithAutocomplete;

	public Spell $spell;
 
	public function mount(Spell $spell)
	{
		 $this->spell = $spell;
		 $this->selectedItems = $this->spell->getSelectedPlayerClasses();
		 $this->setModel(\App\Models\PlayerClass::class);
	}
	
	public function emitToParent()
	{
		$this->emit('classTagged', collect($this->selectedItems)->pluck('id'));
	}
	
	public function render()
	{
		return view('livewire.autocomplete', [
			'placeholder' => 'Search classes...'
		]);
	}
}
```

## Required TRAIT
![[WithAutocomplete TRAIT#^1]]