#GUI layers

To ensure that the right elements come out on top, every GUI element needs to be part of a CanvasLayer, with a certain layer level. The higher the number, the more visible it is (ie 120 covers up 110, 100, 90, etc; wheras 20 only covers up 10, 5, etc). To keep margin for expansion, never pick the extremes (121-128 or 0-10). Between layers, try to have 10 layers available as well, to allow new layers to 'slide in' as needed.

Here is an overview of the layers used:

- Loading blackout - 120
- GUI (Time, Date) - 50
