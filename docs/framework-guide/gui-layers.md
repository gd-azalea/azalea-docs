#GUI layers

To ensure that the right elements come out on top, every GUI element needs to be part of a CanvasLayer, with a certain layer level. The higher the number, the more visible it is (ie 120 covers up 110, 100, 90, etc; wheras 20 only covers up 10, 5, etc). To keep margin for expansion, never pick the extremes (121-128 or 0-10). Between layers, try to have 10 layers available as well, to allow new layers to 'slide in' as needed.

Here is an overview of the layers used:

- Loading blackout - res://scenes/menus/Loading.tscn - 120
- GUI (Time, Date) - res://scenes/gui/GUI.tscn - 50

## Z-index

Y sorting should usually handle this, but players and npcs are not in the same structure as the level, due to being able to load those around. As such we have some custom code to do exactly the same by dynamic z-index changing. Higher z-index means drawing in front of others.

Landscape/background: 0
Behind default: 3 
Default z-index: 5
In front of default : 7
