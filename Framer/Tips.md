

# Height 
- h-fit & min-h-viewport 



# Site Structure
- `Navbar + main(web pages) + Footer` - good for SEO & accessibility 
- section - `top/bottom padding`, child frames `left/right padding` 
- `max-w` so content not stretch on large screens
- `h-fit` with padding (t/b-100, l/r-20) 
- use semantic HTML



# Sync transition
- when one elem transition moves it's siblings/parent - make sure to have transition on all of them or in parent container



# rem 
- for text units (1rem = 16px) 



# Hacks:
* Scale tool - press `k` to precisely resize items for different breakpoints 
* copy/paste style of elements - `ctrl + shift + c / v`
* Can set style on a `link` variable - isn't set - bg-red - signal to add link in big projects to debug 
* preference - auto switch to layers panel
* style > filters>.........
* Setting > Details page of your `Blog` page -> add your variables for title/desc -> for better SEO


# Variants
* prepare every asset on base variant & by visibility toggles, animate them on variants


# new color style with light/dark modes colors
- use separate variables for dark/light modes
- Dark/Light Mode toggle - component by framer university


# Text
- Highlight word & change bg/color specific for the selected character or word

# inline content Editing
- CMS(direct select & change Data for specific item)


- Use relevant Media and Text only
- remove custom cursor on small screen 
- tap color for mobile
- lock areas that u won't let touched
- assign style to all elements - text, color for easy global changes
- make every value variable in component - for easy changes.

1. Vector sets: assets -> vector -> new set of vector assets.
2. Icons from multiple paths: group them (`ctrl+g`) and tweak properties.

# position
- Sticky only works when all parent have `overflow-visible`.
- to apply `fixed`, element should be on root level.
- Accordion - give `h-0` to closed panel and on click on header, change it to `h-fit`
  with animation
- use `max-w` to limit width of content.
- use `sticky` for Navbar with a padding in section equal to Navbar height.
- if there is an image in the container, give `contain: paint layout` to it to prevent layout shift.
- if your top pin is activated element will grow to bottom, if bottom active - grow to top.