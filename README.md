Introduction
------------

This repository contains translations of Wing version 9 for all Wing Python IDE products
(including Wing Pro, Wing Personal, and Wing 101). The following translations exist:

    PO/en -- Empty translation with all strings; use this to start a new translation
    PO/de -- German (by Christoph Heitkamp)
    PO/fr -- French (by Jean Sanchez and Laurent Fasnacht)
    PO/ru -- Russian (by Alexandr Dragunkin)
    PO/es -- Spanish (incomplete and not currently active)

These can be edited with any number of tools available for working with gettext PO files
(see details below).

All of the translations available for Wing were done by the volunteers listed above.

Overview of Files
-----------------

Wing's translatable strings are split into a number of different files found in the `PO/*` 
directories of this repository.  All of these files are UTF-8 encoded, as indicated with
the 'Content-Transfer-Encoding' header in each file.  This header should not be changed
to another encoding because parts of Wing's translation system currently assumes UTF-8
without checking the file header.

There are quite a few translation files that are generated from strings found in Wing's
source code.  Some are more important than others, as follows:

These contain strings users will see in the UI:

	bootstrap.po
	build-files.po
	src.po
	src_browser.po
	src_cache.po
	src_codewarnings.po
	src_command.po
	src_debug_client.po
	src_debug_tserver.po
	src_diff.po
	src_edit.po
	src_guimgr.po
	src_guiutils.po
	src_guiutils_pysidescintilla.po
	src_package.po
	src_plugins_cluster.po
	src_plugins_container.po
	plugins_cluster_dockercompose.po
	plugins_container_docker.po
	plugins_container_lxc.po
	src_pref.po
	src_process.po
	src_proj.po
	src_pysource.po
	src_refactoring.po
	src_scripting.po
	scripts_debugger_extensions.po
	scripts_django.po
	scripts_editor_extensions.po
	scripts_emacs_extensions.po
	scripts_experimental.po
	scripts_pylintpanel.po
	scripts_brief.po
	src_search.po
	src_testing.po
	src_versioncontrol.po
	src_wingbase.po
	src_wingide.po
	src_wingutils.po
	

These contain strings that are mostly the docstrings for commands.  They are currently
only used in the documentation, which is only in English, so most of these strings can
be skipped.  However, a few are strings that end up in the UI because they are extracted
from strings in code and not docstrings:
	
	src_debug_client_cmdmanager.po
	src_diff_commands.po
	src_edit_commands.po
	src_guimgr_commands.po
	src_proj_commands.po
	src_refactoring_commands.po
	src_search_commands.po
	src_testing_commands.po
	src_versioncontrol_commands.po
	src_wingide_topcommands.po


These are currently unused or only contain error strings and can be entirely skipped:
	
	plugins_container__docker_sleep.po
	scripts_brief.po
	scripts_testapi.po
	src_profile.po
	src_guiutils_scintillaedit.po
	src_docutils_*.po
	src_external_*.po
	src_parsetools.po
	src_wingbase_pexpect.po
	src_wingbase_pexpect_ptyprocess.po


Starting a New Translation
--------------------------

To start a translation for which Wing does not yet have support, you'll need to copy the
`PO/en` files to `PO/xx` where `xx` is replaced with the ISO 639-1 lower case two-letter
language code for the language you are going to translate to.

Editing Your Translation
------------------------

You can use any editor or translation tool that supports `.po` files to work on your translation.
Using a translation tool is typically better than using an unspecialized text editor, because
the tool will suggest translations and make it easier to manage how many and which strings
are still untranslated.

Some possibilities for editors can be found here:

https://www.drupal.org/community/contributor-guide/reference-information/localize-drupal-org/working-with-offline/editors-for-po-files

Building and Testing MO files
-----------------------------

When you are ready, you can try out your translation in Wing 9, as follows:

First convert all the `.po` files in your translation to `.mo` files:

	cd /path/to/wing9-po-all
	python3 msgfmt.py PO/xx/*.po

You'll need to correct the paths in the above to match where you have your wing9-po-all
directory and relace `xx` with the 2-letter language code you are using.

Next copy the `.mo` files into `resources/locale/xx/LC_MESSAGES` in your Wing 9
installation. Depending on your OS and how you installed Wing, you may need to do that as
root or Administrator, and you may want to make a copy of that directory first, so you can
restore it later if needed.  It's also possible to set up a symbolic link so that you
don't need to copy files each time.  See the OS-specific notes below for details.

**Important:** If you are working on an new translation of Wing you'll need to use `fr` or
one of the other existing translations initially instead of the 2-letter translation code
for the language you are translating into. This is needed so that you can select your
translation with User Interface > Display Language in Wing's Preferences dialog.

You will need to restart Wing each time you update `.mo` files so that the new contents are
loaded into the UI.

Some notes for each supported OS:

**Linux**

To set up a symbolic link from your Wing installation to your development area on Linux,
use commands like the following:
	
	cd /usr/lib/wingpro9/resources/locale/xx
	sudo mv LC_MESSAGES LC_MESSAGES.old
	sudo ln -s /path/to/wing9-po-all/PO/xx LC_MESSAGES
	
You will need to replace xx with the correct 2-letter translation code(s) and adjust paths as necessary.

To avoid having to run commands as root, install the .tar installation of Wing instead.

**macOS**

To set up a symbolic link from your Wing installation to your development area on macOS,
use commands like the following:

	cd "/Applications/Wing Pro.app/Contents/Resources/resources/locale/fr"
	mv LC_MESSAGES LC_MESSAGES.old
	ln -s /path/to/wing9-po-all/PO/xx LC_MESSAGES

You will need to replace xx with the correct 2-letter translation code(s) and adjust paths as necessary.

To start Wing bypassing macOS security checks that dislike changing the *.app* contents, run 
from the command line:

	"/Applications/Wing Pro.app/Contents/Resources/wing"

**Windows**

On Windows, the command to run to generate the `.mo` files differs somewhat:

	cd \path\to\wing9-po-all
	python.exe msgfmt.py PO\xx\*.po

You will need to replace xx with the correct 2-letter translation code(s) and adjust paths as necessary.

To create a symbolic link from your Wing installation into your development area on
Windows, run a command like the following as Administrator:

	cd "c:\Program Files\Wing Pro 9\resources\locale\fr"
	move LC_MESSAGES LC_MESSAGES.old
	`mklink /D "c:\Program Files\Wing Pro 9\resources\locale\fr\LC_MESSAGES" c:\path\to\wing9-po-all\PO\xx\LC_MESSAGES`

To avoid having to run commands as Administrator, install the .zip installation of Wing instead.

Submitting Your Translation
---------------------------

Once you've completed enough of the translation for it to be added to Wing, clone the
wing9-po-all repository, drop in your PO/xx directory and add it to the forked repository
with `git add`.  Then submit a pull request and *also* email support@wingware.com so that
we can be sure your pull request is processed quickly.  

Getting Help
------------

Contact support@wingware.com for assistance.
