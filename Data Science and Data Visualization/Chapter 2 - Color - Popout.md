#DataScienceAndDataVisualization
#Perception
#Cognition
#Colour
#Popout 
___
## Perception Vs Cognition

| Perception                                                                                                                                                                      | Cognition                                            |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------- |
| \-  Identification and interpretation of sensory information.    <br>- From the physical stimulus to recognizing information.<br>- Shaped by learning, memory, and expectation. | \- The processing of information, applying knowledge |
| ⇒ Hear someone speak: Perception                                                                                                                                                | ⇒ Understand the language: Cognition                 |
__Cognition’s Task:__ Cognition is about using that perceived information, applying knowledge, categorising objects, assessing relationships, drawing conclusions, and problem-solving ⇒ _In a sense, ==cognition creates meaning out of perception.==_

| Perception                                                                                                          | Cognition                                                                                                         |
| :------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| \- Eye, optical nerve, visual cortex<br>\- Basic perception<br>- First processing<br>- Not conscious <br>- Reflexes | \- Recognizing objects <br>- Relations between objects<br>- Conclusion drawing<br>- Problem solving<br>- Learning |
**Impact on Visualization:** 
- If visualisation relies only on pure raw perception, it will be less effective. 
- A good visualisation works with cognition to guide the user towards insights and allow them to interpret the visualisation. 
- Perception is the foundation on which cognitive understanding is built.
___
## What We See Vs. What is there?
\- Our perception is not a perfect reflection of reality. Optical illusions (like the Dalmatian or the Ames Room) show how our brains can be tricked.
___
## Human Visual System
- **Beyond Rods and Cones (Slides 15, 16):** While the slide introduces them, it's worth knowing that cones come in three types (L, M, S, also related to Red, Green, and Blue), which have overlapping spectral sensitivities (Slide 17), This overlap allows us to see a spectrum of colours not just 3 primary ones. Also, Rods are more sensitive to light and thus responsible for night vision.
- **The Fovea (Slide 16, 18):** The fovea is key to detail vision because it's dense with cones. But this also means a very small part of our visual field is in focus at a given time. This explains the need for saccades (rapid eye movements) as introduced on slide 20.
- **Colour Wavelengths (Slide 24):** The presentation correctly links spectral colour to single wavelengths, but the idea of "unsaturated" colours (e.g., pink, brown) as mixtures of multiple wavelengths is significant. These unsaturated colors often require the processing of information by multiple receptors, rather than one specific cone being activated.
- **Colour as a Combined Phenomenon (Slide 26):** It's crucial to understand that colour perception isn't just about wavelength; it's also about light intensity/energy. This idea that we need a relative understanding of colour perception is highlighted in later slides as well.
- **Colour Blindness (Slide 42):** The slide touches upon the most common types (red-green) but doesn't mention other rarer kinds and the causes which is a mutation or alteration of these light-sensitive pigments, affecting how someone perceives colour.
___
## Colour
- **Color as a Tool, Not an Afterthought (Slides 34-35):** Color is not for aesthetic appeal but for effective communication. It should be used purposefully and consistently, based on the data type shown, its inherent properties and how it needs to be viewed.
- **HSV Color Model (Slide 28):** Using HSV (Hue, Saturation, Value) rather than RGB can improve intuitive understanding and choice of colours. Hue relates to colour categories, saturation to purity, and value to lightness/darkness. ![[HSVModel.png|640 x 640]]
- **ColorBrewer (Slide 36):** This is an important real-world tool worth exploring. It helps people choose colour palettes suitable for different types of data and also considers colour blindness.
- **Rainbow Colormap Warning (Slide 38, 39):** The presentation rightly warns about the problems of using rainbow colourmaps for quantitative data: use value saturation works but not as good don‘t use hue! ⇐ Different colours do not map linearly onto data values. This can result in distortions and make it hard to perceive trends and patterns. It's not perceptually uniform.![[QuantitativeDataColour.png]]
- **Colour and Context (Slides 48-55):** These slides are critical: The same colour can appear differently depending on the background. This simultaneous contrast is important to consider during visualisation design.
___
## Pop Out (Chapter 2: Pop Out)
\- **Properties detected by the low-level visual system**:
- Processing is extremely rapid (200-250 milliseconds)
- Accurate
- Process in parallel.
\- Happens before focused attention → pre-attentive
\- Attention is significant for cognition
\- Independent of the number of distractors

\- **Features vs. Conjunctions (Slides 69, 70):** Single features like a difference in hue or shape will allow us to identify an outlier quickly. If the outlier is defined by a combination of features (e.g., red AND a circle), the pre-attentive process fails, requiring a slower, more cognitive search. This is why it is emphasized to avoid using a combination of visual features to highlight the same property, which is what is done in conjunction.
\- **Pre-attentive Properties in Practice (Slides 71, 73, 74):** You can see the pre-attentive properties in the slides, including Orientation, Hue, Closure, Size, and Curvature. These are the basis for how to highlight, filter, and group data points.
___
## Task (slides 72)
- _**Target detection:**_ Detect the presence or absence of a target
- _**Boundary detection:**_ Detect a texture boundary between two groups of elements, where the elements in each group have a common visual property
- **Region tracking:** Track one or more elements with a unique visual feature as they move in time and space
- **Counting and estimation:** Users count or estimate the number of elements with a unique visual feature
___
## Pre-attentive processing in vis
- Can be used to draw attention to areas of interest.
- Can be used to express similarity/ group memberships.
- Visual features must be carefully designed.
- Conjunctions must be avoided: Colourful vis **Vs** highlight.
___
## Change blindness
- **The detail of an image cannot be remembered across separate scenes:** except in areas with focused attention.
- **Interruption** (e.g. a blink, eye saccade or blank screen) amplifies this effect.
- **Not failure of vision system:** Failure due to inappropriate ==attentional guidance==.

\- **Various theories about causes:**
- *Overwriting*: information that was not abstracted is lost
- *First impression*: only the initial view is abstracted
- *Nothing is stored*: only abstract concepts are committed to memory.
- *Everything is stored, and nothing is compared*: we compare only when we are forced to
- *Feature combination*: scenes are combined as long as they make sense

\- **Influencing factors**:
- Attention
- Expectation (knowing something will change)
- Semantic importance of changed object
- Low-level object properties are overlooked more easily

⇒ To find meaning in what we see, we must ==selectively pay attention to what is important==. Low-level vision is driven by ==object features rather than a conscious effort== where to look (e.g., pre-attentive processing). Attention is driven by ==preexisting knowledge, expectations, and goals stored in long-term memory==.
___
## Gestalt Principles
- **GESTALT PRINCIPLES** Patterns that transcend the visual stimuli that produced them"
> The whole is something other than the sum of its parts ⇐  Kurt Koffka Vs 
> The whole is greater than the sum of the parts.
- **PROXIMITY**: Grouping/linking by placing entities nearby
- **SIMILARITY**: Co-modulation of a Chanel colour, shape, size, value, orientation, texture... Adding a glyph, label, frame, background"
___
## Colour - Perception Issues
- **Popout**: work for ==1-2== simultaneously but not for more.
	- Slower in a cluttered environment.
	- The size of the coloured object is relevant.
- **Similarity**: Modulate everything else, blurring, darkening, desaturating.
	- Don’t use it unless the sole objective is to guide attention toward one (set of) items.
___
## Grouping: Increasing the connection between objects
- Proximity
- Colour
- Size 
- Shape
- Connected items with a line or curve. Surround items with an outline, surface, and volume.
- Similarity
- Connection
- Enclosure
___
## Continuity - Closure - Symmetry
\- Our mind will separate things with ==smooth and continuous curve==s.
\- Our mind will imagine the line to make it closure.
\- Our mind will think the objects always symmetric.
