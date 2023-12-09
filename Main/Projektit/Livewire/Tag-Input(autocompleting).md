# AutocompletingTagInput

- ## 1. Component description and requirements
	- ### Description
	> This component is used for inputting tags, it may create tags from given collection or based on DB Queries. If you want to use DB Queries, it can be achieved by declaring the model path you want to query for, and what attribute the user can search with. If you instead want to use a collection, declare a collection of items you wish to filter and the filterable attribute. Filter attribute defaults to 'name'.
	- ### Requirements
		- [[Autocompleting_trait]]
		- [[Tagging_trait]]
	
- ##  2. Component Methods
	- ### Mount
		```php 
		<?php 
			public function mount(?string $model = null, $filter = null)
		 	{
				$this->model = $model;
			 	$this->filter = $filter ?? 'name';
		 	}
		?>
		```
		---
	- ### EmitClassChange
		> If this component has a parent livewire component you may send updated data to it using this method and adding a listener for it on the parent component
		```php 
			 public function emitTagChange()
			 {
				$this->emit('userTagged', collect($this->tags)->pluck('id'));
			 }
		```
		---
	- ### Select Item
		> This function replaces the function from Taggable_Trait to work with Autocompleting_Trait. It will add a tag based on which item user selected from the results list. 
		```php  
		public function selectItem($id = null)
 		{
			$id = $id ?: $this->highlightIndex;
			$item = $this->items[$id] ?? null;
			if($item){
				$this->showDropdown = false;
				$this->query = null;
				$this->items = [];
				$this->addTag($item);
			}
		}
		```
		---
- ## 3. Component View
	- ### Required parameters
		- name -> To identify input
		- label -> Input label
		- placeholder -> Input placeholder text
		- filter -> Attribute to filter with, what the user searches for
		- collection -> A collection of items the user search tags from based on filter
		- model	-> A model the user can search tags from based on filter
	- ### Required Components
		- [[Input]]
	- ### Html/Blade
		```html
		<div class="relative w-full">
			 @error('query')
				 <p class="alert">
				 {{ __('Missing a model to query from or a collection of filterable items') }}
				 </p>
			 @enderror
			 <div class="w-full">
				 <x-form.input
					 class="text-gray-100"
					 id="{{ $name }}"
					 placeholder="{{ $placeholder }}"
					 wire:model="query"
					 wire:blur="hideDropdown"
					 wire:focus="showDropdown"
					 wire:keydown.escape="hideDropdown"
					 wire:keydown.tab="hideDropdown"
					 wire:keydown.arrow-up="decrementHighlight"
					 wire:keydown.arrow-down="incrementHighlight"
					 wire:keydown.enter.prevent="selectItem"
				 >
					{{ $label }}
				</x-form.input>
			 </div>
			 @if(!empty($query) && $showDropdown)
				 <div class="absolute z-10 w-full mt-1 bg-white border border-gray-300 rounded-md shadow-lg">
					 @if (!empty($items))
						 @foreach($items as $i => $item)
							 <a
							 wire:click="selectItem({{ $i }})"
							 class="block py-1 px-2 text-sm cursor-pointer hover:bg-blue-50 {{ $highlightIndex === $i ? 'bg-blue-50' : '' }}">
								{{ $item['full_name'] }}
							 </a>
						 @endforeach
					 @else
						<span class="block px-2 py-1 text-sm">No results!</span>
					 @endif
				 </div>
			 @endif
			 <div class="flex flex-wrap w-full pt-3 space-x-2">
				 @foreach ($tags ?? [] as $key => $tag)
					 @if(gettype($tag) == 'string')
						 <div class="transition duration-100 inline-flex px-2 py-1 text-xs text-white bg-primary-500 rounded-md hover:glow-red mt-1.5 ml-2 border border-primary-500 pointer-events-none">
						 {{ $tag }}
							 <span
								class="inline-block ml-1 cursor-pointer pointer-events-auto removeTag hover:text-red-400"
								wire:click="removeTag({{ $key }})">
								<i class="fas fa-times"></i>
							 </span>
						 </div>
					 @else
						 <div class="transition duration-100 inline-flex px-2 py-1 text-xs text-white bg-primary-500 rounded-md hover:glow-red mt-1.5 ml-2 border border-primary-500 pointer-events-none">
							{{ $tag['name'] }}
							 <span
								class="inline-block ml-1 cursor-pointer pointer-events-auto removeTag hover:text-red-400"
								wire:click="removeTag({{ $key }})">
								<i class="fas fa-times"></i>
							 </span>
						 </div>
					 @endif
				 @endforeach
			 </div>
		</div>
		```
- ## 4. Calling the component
	```html
		<livewire:autocompleting-tag-input
			name="tag_users"
			:label="__('Tag users')"
			:placeholder="__('Search users to tag')"
			filter="full_name"
			//use which ever you need
			:collection="$users"
			:model="$modelPath"
		/>
	```
- ## 5. Full Component Class
	```php
	<?php
		namespace App\Http\Livewire;

		use App\Traits\Livewire\Autocompleting;
		use App\Traits\Livewire\Tagging;
		use Livewire\Component;

		class AutocompletingTagInput extends Component
		{

		  use Autocompleting, Tagging;

		  public $name;
		  public $label;
		  public $placeholder;
		  public $collection;

		  public function mount(?string $model = null, string $filter = 'name')
		  {
		    $this->model = $model;
		    $this->filter = $filter;
		  }

		  public function emitTagChange()
		  {
		    $this->emit('classTagged', collect($this->tags)->pluck('id'));
		  }

		  public function selectItem($id = null)
		  {
		    $id = $id ?: $this->highlightIndex;
		    $item = $this->items[$id] ?? null;

		    if($item){
		      $this->showDropdown = false;
		      $this->query = null;
		      $this->items = [];
		      $this->addTag($item);
		    }
		  }

		  public function render()
		  {
		  return view('livewire.autocompleting-tag-input');
		  }
		} 
	```