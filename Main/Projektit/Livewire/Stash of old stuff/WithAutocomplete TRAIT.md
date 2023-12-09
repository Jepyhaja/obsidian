Autocomplete functionality with the ability to save selected data as an array of objects. ^1
```php
<?php

namespace App\Http\Livewire\Autocomplete;

trait WithAutocomplete
{

	public $query= '';
	public array $items = [];
	public array $selectedItems = [];
	public int $highlightIndex = 0;
	public bool $showDropdown = true;
	public $model;

	public abstract function emitToParent();

	public function mount()
	{
		$this->reset();
	}

	public function setModel(string $path)
	{
		$this->model = $path;
	}

	public function reset(...$properties)
	{
		$this->items = [];
		$this->highlightIndex = 0;
		$this->query = '';
		$this->selectedItems = [];
		$this->showDropdown = true;
	}

	public function removeItem($remove)
	{
		$this->selectedItems = collect($this->selectedItems)
		->filter(fn($item) => $item['id'] !== $remove)->toArray();
		$this->emitToParent();
	}

	public function hideDropdown()
	{
		$this->showDropdown = false;
	}

	public function incrementHighlight()
	{
		if($this->highlightIndex === count($this->items) - 1){
		$this->highlightIndex = 0;
		return;
	}

	$this->highlightIndex++;
	}

	public function decrementHighlight()
	{
		if($this->highlightIndex === 0){
			$this->highlightIndex = count($this->items) - 1;
			return;
		}

		$this->highlightIndex--;
	}

	public function selectItem($id = null)
	{
		$id = $id ?: $this->highlightIndex;
		$item = $this->items[$id] ?? null;
		if($item){
			$this->showDropdown = true;
			$this->query = '';
			if(!in_array($item, $this->selectedItems)){
				array_push($this->selectedItems, $item);
				$this->emitToParent();
			}
		}
	}
	public function updatedQuery()
	{
		$this->items = $this->model::where('name', 'like', '%' . $this->query. '%')
		->whereNotIn('id', collect($this->selectedItems)->pluck('id'))
		->take(5)
		->get()
		->toArray();
	}
}

```