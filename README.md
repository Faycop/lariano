# Lariano 0.7.4 - Spaghetti, Pizza and Responsive Grids

Lariano is a REALLY (only **84 byte** for core functionality when compiled) lightweight SASS based framework - **with NO Dependencies :)** -  that allows you to define 4 typology of devices on which you will have:

 - a grid based on whatever number of columns you like
 - whatever gutter you want for each one
 - whatever should be the media query to trigger the responsive
 - how much should be larger the container

## Introduction
Lariano is born with the idea that using a framework, you should write css only when needed and only what you need.
And of course it must be SIMPLE to suit every occasion ;)
With the power of SASS, Lariano doesn't write CSS if you don't use it, so it's a nice tool to rely on and to build grids with your idea first in line.

## License
Lariano is distribuited under [MIT License](http://en.wikipedia.org/wiki/MIT_License)

## Compatibility
Compatibility is up to every browser that supports `css3 box-sizing` such as Internet Explorer 8 and so on.

## Changelog
> ...
> v0.7.3
> - Added "all" typology to mixin lariano-move

> v0.7.4
> - Changed the value of the @include lariano-container for resetting it. Now is @include lariano-container(reset)
> - Fixed a bug on wich defining standard-measure column like @include lariano-col(half) didn't put the gutter
> - Now Lariano provides an extra variable called "$genericGutter" wich defines the gutter for the standard-measure columns in absence of a defined typology
> - Added the possibility to do something like @include lariano-col(desktop,half) on wich provides the gutter of the defined typology instead of the $genericGutter value
> - Merged the mixin @lariano-col-reset in @lariano-col. now the syntax is: @include lariano-col(desktop, reset) or even @lariano-col(all, reset) or @lariano-col(reset) to undo the columns on every typology

## Configuration
The configuration will be something like that:

```sass
$large: (
	name: 'large',
	media: 1200px,
	container: 1200px,
	columns: 12,
	gutter: 32px
);

$desktop: (
	name: 'desktop',
	media: 980px,
	container: 980px,
	columns: 10,
	gutter: 28px
);
$tablet: (
	name: 'tablet',
	media: 768px,
	container: 768px,
	columns: 8,
	gutter: 20px
);
$mobile: (
	name: 'mobile',
	alt: 'mb-first',
	media: 745px,
	container: 585px,
	columns: 4,
	gutter: 10px
);

// This is for the standard-measure columns like full, half, third etc.
// You can allways use something like @include lariano-col(tablet,third); to use the gutter of the targeted typology
$genericGutter: 32px;
```

##Mixin
Lariano is based on a series of mixins which you can use as you want to build your awesome responsive grid:

```sass
@include lariano-container($typology:all)
@include lariano-media-query($typology)
@include lariano-col($typology, $columns:1, $gutter: default, $direction: default)
@include lariano-col-reset($typology:all)
@include lariano-move($service, $typology, $columns:1, $direction: left)
```

### lariano-container($typology)
Use it to define an element who will contain something (default `all`).
Admitted values:
- `all`
- `reset`
- `large`
- `desktop`
- `tablet`
- `mobile` 

`all` will make the container responsive for all 4 typologies
`reset` will reset the container
```sass
@include lariano-container(desktop);
```
---
### lariano-media-query($typology)
Use it to code something that will go inside the media query of the single typology.
Admitted values: `large`, `tablet`, `mobile` 

```sass
@include lariano-media-query(mobile){
	text-align: left;
	display: inline-block;
};
```
---
### lariano-col($typology, $columns:1, $gutter: default, $direction: default)
The key of the grid, you can use it in various way.

Admitted values for `$typology`:
- `large`
- `desktop`
- `tablet`
- `mobile`
- `mb-first`
- `full`
- `three-quarters`
- `two-third`
- `half`
- `third`
- `fourth`
- `fifth`
- `sixth`
- `seventh`
- `eighth`
- `ninth`
- `tenth`
- `reset`

Admitted values for `$columns`:
- from `0` to `X` - based on how many columns you define
- `full`
- `three-quarters`
- `two-third`
- `half`
- `third`
- `fourth`
- `fifth`
- `sixth`
- `seventh`
- `eighth`
- `ninth`
- `tenth`

Admitted values for `$gutter`:
- `gutter`
- `no-gutter`

> `mb-first` will use the same configuration of the `mobile` typology without the media-query
```sass
.sidebar {
	@include lariano-col(large, 12);
	@include lariano-col(desktop, 5, no-gutter);
	@include lariano-col(tablet, 3, gutter, right);
	@include lariano-col(mobile, 2, no-gutter);
}
```
> Using a standard measure such as `half`, `third`, etc will use the `$genericGutter` variable to define the gutter
```sass
.sidebar {
	@include lariano-col(fifth);
}
```
> But you can also use the typology parameter to use the gutter of that target
```sass
.sidebar {
	@include lariano-col(desktop, half);
}
```

---
### lariano-move($service, $typology, $columns:1, $direction: left)
Moves an element using 4 `$service`:
- `offset`
- `inset`
- `push`
- `pull`

#### lariano-move(offset, ...)
Offset an element from its position to `X` columns using CSS `margin`

Admitted values for `$typology`:
- `large`
- `desktop`
- `tablet`
- `mobile`
- `mb-first`
- `full`
- `three-quarters`
- `two-third`
- `half`
- `third`
- `fourth`
- `fifth`
- `sixth`
- `seventh`
- `eighth`
- `ninth`
- `tenth` 

Admitted values for `$columns`:
- from `0` to `X` (based on how many columns you define)

Admitted values for `$direction`:
- `left`
- `right`

```sass
.sidebar {
	@include lariano-col(desktop, 3);
	@include lariano-move(offset, desktop, 1, right);
}

footer {
	@include lariano-col(mobile, 2);
	@include lariano-move(offset, half);
}
```
---
#### lariano-move(inset, ...)
Inset an element from its position to `X` columns using CSS `padding`

Admitted values for `$typology`:
- `large`
- `desktop`
- `tablet`
- `mobile`
- `mb-first`
- `full`
- `three-quarters`
- `two-third`
- `half`
- `third`
- `fourth`
- `fifth`
- `sixth`
- `seventh`
- `eighth`
- `ninth`
- `tenth` 

Admitted values for `$columns`:
- from `0` to `X` (based on how many columns you define)

Admitted values for `$direction`:
- `left`
- `right`

```sass
.sidebar {
	@include lariano-col(desktop, 3);
	@include lariano-move(inset, desktop, 1, right);
}
```
---
#### lariano-move(push, ...)
Push an element from its position to `X` columns using CSS `position: relative` and `left`

Admitted values for `$typology`:
- `large`
- `desktop`
- `tablet`
- `mobile`
- `mb-first`
- `full`
- `three-quarters`
- `two-third`
- `half`
- `third`
- `fourth`
- `fifth`
- `sixth`
- `seventh`
- `eighth`
- `ninth`
- `tenth` 

Admitted values for `$columns`:
- from `0` to `X` (based on how many columns you define)

```sass
.sidebar {
	@include lariano-col(desktop, 3);
	@include lariano-move(push, desktop, 2);
}
```
---
#### lariano-move(pull, ...)
Pull an element from its position to `X` columns using CSS `position: relative` and `left`

Admitted values for `$typology`:
- `large`
- `desktop`
- `tablet`
- `mobile`
- `mb-first`
- `full`
- `three-quarters`
- `two-third`
- `half`
- `third`
- `fourth`
- `fifth`
- `sixth`
- `seventh`
- `eighth`
- `ninth`
- `tenth` 

Admitted values for `$columns`:
- from `0` to `X` (based on how many columns you define)

```sass
.sidebar {
	@include lariano-col(tablet, 5);
	@include lariano-move(pull, tablet, 3);
}
```
