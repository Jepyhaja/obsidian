# Component name

- ## 1. Component description
	> Describe the component here
	> Maybe it is a bit longer text
	> It might require several lines

- ##  2. Component Methods
	- ### Method x
		> describe the component method here
		```php 
		<?php 
			echo 'code here'; 
		?>
		```
		---
	- ### Method x
		```php 
		<?php 
			echo 'code here'; 
		?>
		```
		---
	- ### Method z
		```php 
		<?php 
			echo 'code here'; 
		?>
		```
		---
- ## 3. Component View
	- ### Required parameters
	- ### Required Components
	- ### Html/Blade
		```html
			<div>Component html/blade here</div>
		```
- ## Component Usage
	```html
		<livewire:component :paramX="$param">
			{{__('slot text or html')}}
		</livewire:component>
	```