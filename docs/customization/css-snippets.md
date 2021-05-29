---
title: Custom CSS snippets
summary: List of useful CSS snippets to modify Stash's appearance.
authors:
    - WithoutPants
    - Trizkat
    - seducingbits
    - cafuneandchill
    - peolic
    - henningBunk
    - AnTiMatteIR
date: 2021-05-24
---

# Custom CSS snippets

**Custom CSS** allows you to modify Stash's stock style sheets.

The following is a list of some useful CSS snippets. You may use them by copying-and-pasting them into the Custom CSS editor found in the `Settings` > `Interface Configuration` panel or by navigating to `127.0.0.1:9999/settings?tab=interface`

!!! info
    CSS tweaks usually require flushing the browser's cache or performing a "hard reload".
    This can be achieved by holding <kbd>Shift</kbd> or <kbd>Ctrl</kbd> (depending on the browser) while reloading the page.

!!! warning
    Future releases of Stash may break some or all CSS tweaks.

## Scenes

### Fit more thumbnails on each row
Reduce left and right padding on Scene and Performer grid pages allowing for more thumbnails on each row.

```css
.grid { padding: 0px !important; }
```

### Allow longer strings when displaying "Studio as Text" on scene thumbnails

```css
.scene-studio-overlay {
	font-weight: 600 !important;
	opacity: 1 !important;
	width: 60% !important;
	text-overflow: ellipsis !important;
}
```

### Hide scene specs (resolution, duration) from scene card

```css
.scene-specs-overlay {
  display: none;
}
```

### Hide studio logo/text from scene card

```css
.scene-studio-overlay {
  display: none;
}
```

### Make the list of tags take up less width
```css
.bs-popover-bottom {
  max-width: 500px
}
```

### Swap studio and resolution/duration positions
```css
.scene-studio-overlay {
  bottom: 1rem;
  right: 0.7rem;
  height: inherit;
  top: inherit;
}

.scene-specs-overlay {
  right: 0.7rem;
  top: 0.7rem;
  bottom: inherit;
}
```

### Adjust the mouse over behaviour in wall mode
```css
@media (min-width: 576px) {
 .wall-item:hover::before {
   opacity: 0;  
 }

 .wall-item:hover .wall-item-container {
   transform: scale(1.5);
 }
}
```

## Performers

### Show entire performer image in performer card

```css
.performer.image {
  background-size: contain !important;
}
```

## Galleries

### Grid view for galleries

```css
.col.col-sm-6.mx-auto.table .d-none.d-sm-block {
    display: none !important;
}
.col.col-sm-6.mx-auto.table .w-100.w-sm-auto {
    width: 175px !important;
    background-color: rgba(0, 0, 0, .45);
    box-shadow: 0 0 2px rgba(0, 0, 0, .35);
}
.col.col-sm-6.mx-auto.table tr {
    display: inline-table;
}
```

### Don't crop preview thumbnails
```css
.flexbin > * > img {
  object-fit: inherit;
  max-width: none;
  min-width: initial;
}
```

## Global

### Change the order of navigation bar buttons

Use `order` values below 0 to move specific buttons to the left of the non-ordered buttons,  
and values above 1 to move them to the right of the non-ordered buttons.

**Before:**  
![image](/img/css-snippets-navbar-before.png)  
**After:**  
![image](/img/css-snippets-navbar-after.png)  

```css
nav .navbar-nav:first-child {
  display: flex;
  flex-direction: row;
}
div.nav-link[data-rb-event-key="/tags"] {
  order: -2;
}
div.nav-link[data-rb-event-key="/movies"] {
  order: -1;
}
div.nav-link[data-rb-event-key="/scenes"] {
  order: 1;
}
```

### Hide specific navigation bar buttons

Hide links to specific sections from the header.

```css
/* Example: Hide markers */
div.nav-link[data-rb-event-key="/scenes/markers"] {
  display: none;
}
```

### Hide the Donate button

```css
.btn-primary.btn.donate.minimal {
  display: none;
}
```

### Blur NSFW images

Use for when working on Stash but don't want to expose NSFW images and text. May not be exhaustive:

```css
.scene-card-preview-video,
.scene-card-preview-image,
.image-card-preview-image,
.image-thumbnail,
.gallery-card-image,
.performer-card-image,
img.performer,
.movie-card-image,
.gallery .flexbin img,
.wall-item-media,
.scene-studio-overlay .image-thumbnail,
.image-card-preview-image,
#scene-details-container .text-input,
#scene-details-container .scene-header,
#scene-details-container .react-select__single-value,
.scene-details .pre,
#scene-tabs-tabpane-scene-file-info-panel span.col-8.text-truncate > a,
.gallery .flexbin img,
.movie-details .logo {
 filter: blur(8px);
}

.scene-card-video {
 filter: blur(13px);
}

.jw-video,
.jw-preview,
.jw-flag-floating,
.image-container,
.studio-logo,
.scene-cover {
 filter: blur(20px);
}

.movie-card .text-truncate,
.scene-card .card-section {
 filter: blur(4px);
}
```