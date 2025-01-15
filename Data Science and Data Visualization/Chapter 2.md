#DataScienceAndDataVisualization
#Perception
#Cognition
#Colour
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
- If visualization relies only on pure raw perception, it will be less effective. 
- A good visualisation works with cognition to guide the user towards insights and allow them to interpret the visualisation. 
- You could think of perception as the foundation on which cognitive understanding is built.
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
- **Rainbow Colormap Warning (Slide 38, 39):** The presentation rightly warns about the problems of using rainbow colourmaps for quantitative data: use value saturation works but not as good don‘t use hue! ⇐ different colours do not map linearly onto data values. This can result in distortions and make it hard to perceive trends and patterns. It's not perceptually uniform.![[QuantitativeDataColour.png]]
- **Colour and Context (Slides 48-55):** These slides are critical: The same colour can appear differently depending on the background. This simultaneous contrast is important to consider during visualisation design.
___
## Popout
