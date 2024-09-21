Ref: https://docs.google.com/spreadsheets/d/17f0dQawb-s_Fd7DHgmVvJoEGDMH_yoSd8EYigrb0zmM/edit?gid=296134756#gid=296134756

There is a settings file in the DB that can track options selected by the player. If this has not been set, things like locale are auto-detected by OS.get_locale().

If the locale is found in the translations, it will load this by default. If a non-matching locale is found, it will default to US_en.

Translations for items, quests, etc are added in the current.db itself.

Translations for menus and GUI elements are added in the res://translations/ folder in CSV format, for example: res://translations/main_menu.csv

You can request the current appropriate language in code via LocaleLookup.findLanguage(). This both returns an ISO code as well as sets it in the TranslationServer of Godot.

Meaning you can manually pass it around or lookup GUI/menu keys such as $"Buttons/Load game".text = tr("MAIN_LOAD_GAME")

To test languages, you can set the 'test_locale' in LocaleLookup.
