#DataScienceAndDataVisualization 
#Channel #Design #Mark #Rank 
___
## Marks & Channels
- **Marks**: represent items or links
	- Items:
		- Points (0D), Lines (1D), and Areas (2D).
		- 3D mark: Volume, but rarely used
	- Links: Containment and Connection
![[Containment_Connection.png|640 x 480]]
- **Channels**: change appearance based on attribute
	- Channel = visual variable: Change appearance proportional to or based on attributes
	- Position, Color, Shape, Tilt (Angle), and Size (Length, Area, Volume).
![[Visual Variables.png| 640 x 480]]
___
## Using marks and channels
![[Using Marks & Channel.png]]
![[RankOfChannels.png]]
___
## Principles of Expressiveness and Effectiveness
- **Expressiveness principle:** The visual encoding should express all of, and only, the information in the dataset attributes.
- **Effectiveness principle:** The importance of the attribute should match the salience of the channel.
- **Means:** The most important attributes should be encoded with the most effective channels to be most noticeable, Then the following important attributes match with less effective channels.
___
## Characteristics of Channel
- **Selective:** Is a mark distinct from other marks? Can we make the difference between the two marks?
- **Associative:** Does it support grouping?
- **Quantitative:** Can we quantify the difference between two marks? (Magnitude vs identity channels)
- **Order (Magnitude vs Identity):** Can we see a change in order?
- **Length:** How many unique marks can we make?
____
## Position
| **Pros**         | - The strongest visual variables<br>- Suitable for all data types                      |
| ---------------- | -------------------------------------------------------------------------------------- |
| **Cons**         | - Sometimes not available (spatial data, map) <br>- Cluttering (many items overlapped) |
| **Selective**    | Yes                                                                                    |
| **Associative**  | Yes                                                                                    |
| **Quantitative** | Yes                                                                                    |
| **Order**        | Yes                                                                                    |
| **Length**       | Big                                                                                    |
⇒ Good Channel (Bad at 3D)
___
## Length & Size
| **Pros**         | - Easy to see which one is bigger<br>- Aligned bars use position redundantly |
| ---------------- | ---------------------------------------------------------------------------- |
| **Cons**         | - Sometimes not available (spatial data, map)                                |
| **Selective**    | Yes                                                                          |
| **Associative**  | Yes                                                                          |
| **Quantitative** | Yes                                                                          |
| **Order**        | Yes                                                                          |
| **Length**       | Yes                                                                          |
⇒ Good Channel (Good for 1D, OK for 2D, Bad for 3D)
___
## Value / Luminance / Saturation
| **Pros**         | - OK for quantitative data when length & size are used<br> |
| ---------------- | ---------------------------------------------------------- |
| **Cons**         | - Not many shades are recognisable.                        |
| **Selective**    | Yes                                                        |
| **Associative**  | Yes                                                        |
| **Quantitative** | Somewhat                                                   |
| **Order**        | Yes                                                        |
| **Length**       | Limited (7 - 8)                                            |
___
## Colour
| **Pros**         | - Good for qualitative data (identity channel)<br>        |
| ---------------- | --------------------------------------------------------- |
| **Cons**         | - Do not work for quantitative data<br>- Lots of pitfalls |
| **Selective**    | Yes                                                       |
| **Associative**  | Yes                                                       |
| **Quantitative** | No                                                        |
| **Order**        | No                                                        |
| **Length**       | Limited                                                   |
___
## Shape
| **Pros**         | - Great to recognize many classes |
| ---------------- | --------------------------------- |
| **Cons**         | - No grouping, ordering           |
| **Selective**    | Yes                               |
| **Associative**  | Limited                           |
| **Quantitative** | No                                |
| **Order**        | No                                |
| **Length**       | Vast                              |
___
## Accuracy of Channels
![[Channel Accuracy.png]]
___
## Factors of Accuracy
- *Alignment*
- *Distractors*
- *Distance*
- *Common Scale*
![[Rank of Items.png]]
___
## Separability of Attributes
![[Separability of Attributes.png]]