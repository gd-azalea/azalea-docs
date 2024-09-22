Please see https://github.com/godotengine/godot-demo-projects/blob/master/gui/multiple_resolutions/main.gd for a thorough resolution scaling implementation


Storage is done in SettingsRepository. There are convenience functions in GraphicsLookup and LocaleLookup for storing and retrieving this.
Settings are made in the OptionsMenu, you can get there from StartMenu (it is part of StartMenu)

The _ready() of OptionsMenu loads in the existing values in the settings.

If no values exist, a default setting is applied. This is defined in SettingsRepository's default_settings() function.

In case you are in the editor, the default settings will be the project settings display/window/size/viewport_width/height in Windowed mode. Outside of the editor, it will default to Fullscreen mode with your screen's resolution set.
