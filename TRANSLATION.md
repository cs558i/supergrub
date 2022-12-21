***** For Translators *****

For translations Super GRUB2 Disk uses gettext, which means that if you've provided translations for almost any other program before, the system should be familiar to you. The po files for Super GRUB2 Disk are in the po/ directory in the source tree.

For instructions on starting a new translation see "info -f gettext --node=Creating" or http://www.gnu.org/software/gettext/manual/gettext.html#Creating (which are different ways to view the same manual).

To contribute to an existing translation simply open po/LL.po (where "LL" is the language code in question) with your favorite PO editor (KBabel, Gtranslator, Emac's PO mode, and others) or any with your favorite text editor. If you chose to use a text editor you'll see that the po file contains many pairs like:

msgid "Color ON/OFF"
msgstr "Farbe AN/AUS"

Where the original string from the source (in English) is within quotes after msgid, and the translated string is in quotes after msgstr. If you see an entry like this:

msgid "Color ON/OFF"
msgstr ""

where there is no text between the quotes after msgstr then it means that that no translation has been provided for that string. So if you can, please provide one!

Another thing to look for is an entry like this:

#, fuzzy
msgid "Detect any GRUB legacy configuration file (menu.lst)"
msgstr "Detecta cualquier archivo de configuracion GRUB2 (grub.cfg)"

Where there is a comment "#, fuzzy" before the entry. A "fuzzy" translation like this means that the string still needs to be translated, but there is a similar string already from a different part of the code which *has* been translated. In this case, the string "Detect any GRUB2 configuration file (grub.cfg)" was in another part of the code and was translated into Spanish as "Detecta cualquier archivo de configuracion GRUB2 (grub.cfg)". Since the strings are very similar (one about GRUB2, the other about GRUB legacy), it offers the existing translation as an option. In this case it isn't quite right,  and the proper translation for "Detect any GRUB legacy configuration file (menu.lst)" would probably be "Detecta cualquier archivo de configuracion GRUB legacy (menu.lst)". After changing the string, or confirming that the guessed translation works for the new string as well, you'll need to remove the "#, fuzzy" as fuzzy translations are not used by Super GRUB2 Disk (instead the string will fall back to the original English).

That should be all you need to know about PO files for wokring with Super GRUB2 Disk, but for full documentation of the format see "info -f gettext --node=PO\ Files" or http://www.gnu.org/software/gettext/manual/html_node/PO-Files.html#PO-Files .


When you run ./supergrub-mkrescue (see INSTALL file) for the first time after adding a new translation (by creating a new po file) you will be asked to enter the name of your language, in your language. This is used in the title of the menu entry for your new language in the language selection menu. This information is then stored in menus/sgd_locale/LL_info.cfg (where "LL" is the two letter language code for your new language).

In order to test your translation please check:
  Build Super Grub2 Disk
section at INSTALL file.


***** For Developers *****
If you're developing a script for Super GRUB2 Disk and would like it to be translated, it's pretty simple. Just take the string you want to use, like "hello, world" and add a '$' before the first quotation mark, to make it $"hello world". After adding a new translated string run ./update_po to update the files in the po/ directory. If you're adding a new file with translated strings you'll need to add that file's path to the file xgettext_file_list before running ./update_po .

Example code before:

menuentry "Print familiar greeting" {
  echo "hello, world"
  sleep 5
}

Example code after:

menuentry $"Print familiar greeting" {
  echo $"hello world"
  sleep 5
}
