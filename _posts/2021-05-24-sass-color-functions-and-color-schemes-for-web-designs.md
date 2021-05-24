I recently did a course called Fundamentals of Design by CodeSchool, which is why I have been pretty excited about experimenting with colors. Sass provides really useful color utility functions to manipulate color easily from the Sass code.

I've done a couple of demos using Sass Color functions.

# Use Sass Color Functions to darken the section background.
Making the section background colors slightly darker as you move along the page is a technique which helps create visual hierarchy in a page.

I use the Sass `hsl($hue, $saturation, $lightness)` function to create a white color by providing a hue with 100% saturation, which gives the most vibrant form of this hue and 100% lightness which creates a white colour.

`$section-bg-color: hsl(210,100%,100%);`

I store the section class names in a list.

`$sections: one two three four;`

Then use the Sass darken($color, $amount) function in a for loop to make each section darker by a pre-set percentage.

`
@for $i from 1 through length($sections) {
  .#{nth($sections, $i)}
  {
    background: darken($section-bg-color, $i*$darken-by);
  }
}
`

You can use saturate/desaturate + lighten/darken + complement functions to create a high contrast between type (text) and background color. Refer to the Sass Documentation for all the cool RGB, HSL, Opacity and Other Color functions.

Here's the demo:


# Use Sass Color Functions to alter a base color in various ways.
In another simple demo, I've created shapes and set the background colors using Sass Color Functions. I've made use of Sass Map to store the colors for hover-effect.

I set the background color of circle to the base color, so that we can see the difference from the base color after been altered.

Here are the functions I used to create the different background colors:

# complement($color)
Gives the complement of a color, that is a color with a hue 180 degrees from the given color.

# adjust-hue($color, $degrees)
Changes the hue of a color. Takes a color and a number of degrees (usually between -360deg and 360deg), and returns a color with the hue rotated along the color wheel by that amount.

# hsla($hue, $saturation, $lightness, $alpha)
Creates a Color from hue, saturation, lightness, and alpha values.

As you can see, I have stored these color settings in variables, so they can be changed easily.
`
/*       Color Settings       */
$base-color: #bb0066;
$text-color: #699;
$circle-color: $base-color;
$diamond-color: complement($base-color);
$triangle-color: adjust-hue($base-color, 60deg);
$parallelogram-color: hsla(hue($base-color), 60%,50%, 0.7);
I have found Sass Map really useful for storing the colors for hover effect. Notice in the code below that I'm able to call the Sass color function, darken($color, $amount) for the key values.

// Map to keep the colors for hover effect
$colors: (
  $circle-color: darken($circle-color, 10%),
  $diamond-color: darken($diamond-color, 10%),
  $triangle-color: darken($triangle-color, 10%),
  $parallelogram-color: darken($parallelogram-color, 10%),
  $text-color: $text-color
);
`

I can set the hover color for the shapes simply by using the Map map-get($map, $key), function, which returns the value in a map associated with a given key. Like in the following code:

`
.circle {
  @include create-circle();
  &:hover {
    background: map-get($colors, $circle-color);
  }
}
`

Here is the demo:


# Fundamentals of Design - Color Scheme
I also want to share a bit of what I learnt about colors in the "Fundamentals of Design" course. The course covers all sorts of exciting topics related to designing a web site.

So, here's what I learnt.

## THERE ARE TWO TYPES OF COLORS:
1. Subtractive color: color you can touch.
2. Additive color: color you can't touch.

**Subtractive color** is controlled by **CMYK**. CMYK stands for Cyan, Magenta, Yellow and Black. In theory all of these colors mix to make black.

**Additive color** is controlled using the **RGB** color scheme. RGB as we know, stands for Red, Green and Blue. In theory all the colors mix to create white.

Primarily with web design we deal with RGB color scheme, however, humans don't process color in terms of Red, Green and Blue. We process color in terms of **HSL**, that is, hue, saturation and lightness.

## HUE
Hue is best visualised on a color wheel. Starting at 0deg at Red, as you move around the circle you get different colors, Green at 120deg, Blue at 240deg and Red again at 360deg. The hues are created by varying degrees of the primary colors mixing to form the different hues. With red in the start, followed by yellow then blue, like in the rainbow:

- Red
- Orange(Red+Yellow) 
- Yellow 
- Green(Yellow+Blue) 
- Blue 
- Idigo
- Vioelet(Blue+Red) 
- Red (and all the hues in between)

The div below has background linear-gradient color stops with hue 0deg, 30deg, 60deg, ..., 360deg (and saturation: 100%, lightness: 50%).

It is also interesting to see the hue values of the named CSS colors. The following pen shows the hue values for colors traditionally cited for rainbow: red, orange, yellow, green, blue, indigo, violet/purple, pink.


I used the following Sass code to check the hue:

`
$rainbow-colors: red, orange, yellow, green, blue, indigo, violet, purple, pink;
  @each $color in $rainbow-colors {
    .color-#{$color} {
            color: $color;
            &:after {
                display: inline-block;
                content: "Hue: " + hue($color) + " Saturation: " + saturation($color) + " Lightness: " + lightness($color);
        }
     }
 }
 `
 
## SATURATION
Saturation is a difference between a color and grey, that is the amount of gray added to a color. A hue at 100% saturation is the most vibrant form of that color, whereas a hue at 0% is gray.

## LIGHTNESS
Lightness is the amount of light in a color. A hue at 100% lightness is white and at 0% lightness is black. A hue at 50% lightness is the most purest form of that color.

Example:

Hue	Saturation	Lightness	Color Description
0deg	100%	50%	Is the most purest form of red.
0deg	100%	70%	Has more white, gives a pinkier color.
0deg	100%	25%	Has less white, gives a darker red.
0deg	25%	50%	Gives a pastel pink color.

# COLOR SCHEME FOR A SITE
Color scheme for a site is four or five colors built into your style guide. First, we need to choose a base color, a foundational color from which the rest of the color scheme will be built out of. When choosing a base color, you have to remember different colors create different moods.

## METHODS TO HELP YOU DECIDE THE COLOR SCHEME
After choosing a base color there are multiple methods you can use to decide what the color scheme would be. Some of the basic methods include:

- **Monochromatic color scheme** - all the colors have the same hue and vary in saturation and lightness.
- **Analogous color scheme** - vary in saturation and lightness but the hue both increases and decreases showing the colours adjacent to the base color in the color wheel.
- **Complementary color scheme** - varies in saturation and lightness but has colors of the same hue of the base color and colors of the opposite hue of the base color.
- 
To find the opposite color, take the color which is 180deg away from the color in the color wheel. The complement($color) function in Sass gives you the complement of a color.

# COLOR AND TYPE
Typography must have a **high degree** of contrast between it and it's background. Contrast is the difference in color, it could be the difference in just the hue, saturation or lightness. It could be a small difference or a large difference. Black and white give the biggest contrast.
