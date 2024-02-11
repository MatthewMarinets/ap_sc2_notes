# Cloak icons
A quick guide to making unit-specific cloaking icons in GIMP.

## Method
1. Load up a ui_techpurchase_*_hired.dds icon
2. Scale the image
   * Make it square
   * Scale the image (76x76 is the standard icon size)
3. Add an outline
  1. Add a new layer
  2. On old layer: right-click -> Alpha to Selection
  3. Selection -> Grow Selection (1~2px)
  4. On new layer: paintbucket outline colour within selction
    * #0cffff = corsair outline
    * #009a63 = terran cloak blur
4. Mess with colours
  * Colors -> Hue-Chroma -> Crank the Chroma
    * (100 looks blue on ghost)
    * 30 chroma, -35 hue looks like a decent green
    * 30 chroma, +10 hue makes for a good bluish backing-colour
  * Increase the exposure
    * 0.9~1.2, play with it
    * (contrast improves if you set the black level ~0.05 while doing this)
5. Add a backing image
   * Duplicate the image, apply colour corrections to get a hue-shifted version
   * Adjust levels, make it dark
6. Add stripes to filter
  * Option 1: Paintbucket pattern fill "Stripes Fine"
  * Option 2: TV scanlines -- not preferred
    * Filter -> Distort -> Video Degradation
    * Mode: Luminance
    * Pattern: Striped (or Large Striped)
  * Colors -> Levels -> change output levels (minimum has to go way up)
7. Add a blur
  * New layer
  * Linear blur: maybe 20? play with it
  * Gaussian Blur: ~5
  * Apply stripes to the blur layer (no need for colour compression)

## Testing
Miscellaneous commands to unlock units and cloak upgrades:
```
?GiveTerranTech 0 268435455 0 268435455 0 0 0 0 0 268435455

Wraith -- progressive 18 -- 262144, 524288
Banshee -- progressive 2 -- 4, 8
progressive: index 6
?giveterrantech 0 0 0 0 0 0 4
```