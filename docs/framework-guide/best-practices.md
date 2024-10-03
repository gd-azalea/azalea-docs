Keep direct changes as close as possible to their component. Keep reusable logic parts in a globally accessible class.
For example: The WorldTime with GUI. The changes for the GUI, updating the labels and such - keep that in the actual GUI/WorldTimeMarginContainer (the wrapper for the labels).
That way, in order to see how they get updated, you only have to find the GUI element itself.
However the main code is in a global WorldTime class, which has its own test
