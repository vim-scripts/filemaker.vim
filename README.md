Official project home is now at [GitHub](https://github.com/chivalry/filemaker.vim).

filemaker.vim
=============

Combining [FileMaker](http://www.filemaker.com) with [Vim](http://www.vim.org) may seem like an odd coupling, but I use both every day, and have been getting more and more atuned to the "Vim" way of doing things. Years ago, when I was using [TextMate](https://macromates.com) I wrote a [bundle](https://code.google.com/p/filemaker-textmate-bundle/) for it that made for easier FileMaker calculation editing in TextMate. This project has the same goal for Vim.

The filemaker.vim plugin provides syntax highlighting and snippet support for FileMaker calculations to be edited in Vim. It detects the filetype for the extensions `.filemaker`, `.fmcalc`, `.fm` and `.fmfn` and also recognizes FileMaker calcs that have been opened using the [QuickCursor](https://github.com/jessegrosjean/quickcursor) app on OS X.

Why Vim
-------

Just about everyone looking at this project probably knows FileMaker but may be unfamiliar with Vim. As great as FileMaker is for quickly building database applications, its leaves a lot to be desired in its calculations dialogs. Using an external text editor alleviates that problem for me. Not wanting to get caught again in the vaporware problem that TextMate gave us for many years, the safest choice of text editors on the Mac comes down to either [BBEdit](http://www.barebones.com/products/bbedit/) or Vim, both of which have been under active development for over 20 years and I've used both in one form or another for nearly that long.

Vim won out for two reasons: extensibility and open source. I've honestly never seen software that can be customized to the extent that Vim can. If you don't like how Vim behaves, you can generally change it, and there are hundreds of plugins available that allow you to simply plug some text files in and get even more functionality.

And because it's open source, the likelihood of it becoming abandonware is slim, especially given its popularity among programmers. The [\#vim IRC channel](http://vim.wikia.com/wiki/Vim_on_Freenode) consistently has hundreds of users online ready to answer any questions. And should Vim itself become stagnant, there are already [ports](http://neovim.org) of it in development.

Of course, there's the final reason, which is that once you become proficient in Vim, editing text is unbelievably fast. If you give it a try, you'll become amazed at how much you can acomplish in strikingly few keystrokes. Don't let Vim's reputation for having a steep learning curve disuade you. I can tell you from experience the return on time investment will be amply repaid.

QuickCursor
-----------

QuickCursor is an OS X app that allows the editing of appliation text fields in an external text editor. For example, while I'm in the text field for a FileMaker calculation, I can press `Cmd-Opt-Ctrl-V` and it will open that calculation in [MacVim](https://code.google.com/p/macvim/). But this procedure has two downsides.

First of all, as nice as QuickCursor is, it's no longer being supported because of its inability to work with Apple's sandbox, but my old version does seem to work with OS X Yosemite.

Second, my version of FileMaker apparently uses DOS returns in calculation dialog boxes even though I'm running this on a Mac. Therefore when a FileMaker calculation is opened in Vim the DOS returns are automatically replaced with Unix returns. This doesn't seem to be a problem, but you should be aware that saving a Vim buffer back into a FileMaker calculation is changing the carriage returns at the end of each line.

My point is, QuickCursor is one of the pieces that will make your editing of FileMaker calculations within Vim (or any external text editor, for that matter) much smoother. If you didn't buy it when it was available in the Mac App Store, QuickCursor's author, [Jesse Grosjean](http://blog.hogbaysoftware.com) has kindly given permission for us to make Version 1 available on [Dropbox](https://www.dropbox.com/s/flkam037ia2pblm/QuickCursor.app.zip). He's also made the source code available for [version 2](https://github.com/jessegrosjean/quickcursor). Finally, you can try one of [the workarounds](http://rocketink.net/2013/05/quickcursor-keyboard-maestro.html) people have come up with using other tools such as [Keyboard Maestro](http://www.keyboardmaestro.com/main/). I can't comment on how useful these are, being satisfied with QuickCursor.

Installation
------------

filemaker.vim is compatible with [Vundle.vim](https://github.com/gmarik/Vundle.vim) and [Pathogen](http://www.vim.org/scripts/script.php?script_id=2332). The easiest way to install is with Vundle by adding `Plugin 'chivalry/filemaker.vim'` to your `.vimrc` and running `:PluginInstall` from within Vim. Alternatively, if you already have Pathogen then clone the `filemakervim` project into `~/.vim/bundle`.

    cd ~/.vimrc/bundle
    git clone https://github.com/chivalry/filemaker.vim.git

If you don't use Vundle or Pathogen (and really, you should, Vim's native plugin management is non-existant), then you'll need to place the files manually as follows, creating the folders in `.vim` as needed.:

    filemakervim/ftdetect/filemakervim.vim -> ~/.vim/ftdetect/filemakervim.vim
    filemakervim/ftplugin/filemakervim.vim -> ~/.vim/ftplugin/filemakervim.vim
    filemakervim/syntax/filemakervim.vim   -> ~/.vim/syntax/filemakervim.vim

Perhaps in the future I'll look into an installer script to do this automatically. If you're using FileMaker and Vim on Windows, place the files in the analogous `vimfiles` folder (I think).

To take full advantage of filemaker.vim you'll need [UltiSnips](https://github.com/sirver/ultisnips) in addition to Vim. With Vundle, the installation of UltiSnips is just as easy as it is for filemaker.vim.

See `:help filemakervim` (or `:help fmv` for short) for complete documentation. This file is found in the repository at https://github.com/chivalry/filemaker.vim/blob/master/doc/filemakervim.txt.

Features
--------

filemaker.vim has two main features. First of all, it (generally) detects the following patterns for syntax highlighting:

- Local and global variables
- Calculation variables that begin with an underscore (i.e., `_variable`)
- Mathematical, logical and string operators
- String and number literals
- Built-in FileMaker functions
- Custom functions that begin with a prefix and a dot (i.e., `dev.MyCustomFunction`)
- Block and in-line comments
- Confirmed compatibility with MacVim and command-line Vim on OS X.

The second major feature is snippet support using UltiSnips. You don't need UltiSnips to use filemaker.vim, but you'll definately want it. It allows the typing of triggers followed by a trigger key (generally `tab`) and fills in a snippet based on the trigger. Although a textual description won't due the feature justics (see the vidos linked to on the UltiSnips page) as an example, if I type `mid<tab>` I get the following:

    Middle( 
      text;
      start;
      numberOfCharacters
    )

The word `text` is highlighted for me so that I can enter the first parameter. Pressing `Ctrl-B` then takes me to the `start` parameter, where I can type over the template text for it and press `Ctrl-B` again to get to the third parameter, enter it, press `Ctrl-B` one more time and it takes me outside the function. filemaker.vim has entries for every FileMaker function there is (OK, `Pi` doesn't have a snippet, but even `External` is included, which it probably doesn't really need anymore), including all of the `Get` functions with mnemonic abbreviations such as `getfc` for `Get( FoundCount )`. But filemaker.vim is even smarter than that.

UltiSnips includes Python interpolation, which means that we can use Python code to provide even more intelligence to our snippets. A major example in filemaker.vim is the `Get` function. Typing `get<tab>` inserts the following:

    Get( (AccountExtendedPrivileges|AccountName|AccountPrivilegeSetName|...|WindowZoomLevel) )

That's every parameter that `Get` accepts. The snippet places you at the beginning of that list and as you begin to type it narrows down the list of available parameters:

    Get( Accou(ntExtendedPrivileges|ntName|ntPrivilegeSetName) )

Once you wheedle the list down to a single possible parameter, that's all filemaker.vim provides, and `Ctrl-B`ing takes you outside the function.

All of the functions that take a list of possible parameters, such as `TextFont`, `TextStyleAdd`, and `GetContainerAttribute`, include this feature.

Another nicety is that the design functions that take a file name as a parameter, which is almost always going to be `Get( FileName )`, fill that in for you automatically. As an example, `fn<tab>` expands to:

    FieldNames(
      Get( FileName );
      layoutName
    )

If this turns out to be a feature some don't prefer, an override setting might be provided in the future. But given that the text `Get( FileName )` are highlighted in the resulting expansion and you can immediately type over them, I don't see a downside yet.

The last snippet feature is that some functions, those which often take the same other functions as parameters, have those sub-functions filled in by default. For example, `ts<tab>` expands to:

    Timestamp(
      Date(
        day;
        month;
        year
      );
      Time(
        hours;
        minutes;
        seconds
      )
    )

However, the top-level parameters are tabstops for the snippet, so the initial jump to them highlights their entirety so that they can be overwritten by simply typing. Jumping to the next tabstop without overriding them takes you to the sub-function parameters.

Formatting and Conventions
--------------------------

FileMaker calculation formatting conventions are notoriously divergent and at this point filemaker.vim uses mine. This expresses itself in how the snippets are inserted and in what variables and custom functions it recognizes in the syntax highlighting.

Syntax highlighting uses regular expressions to match text to language tokens, and honestly I'm no regex expert. For years, however, I've used the convention of beginning my calculation variables with an underscore and my custom functions with a three or four letter code followed by a dot. Recognizing these is much easier than recognizing anything FileMaker would accept, so for the time being that's what filemaker.vim does.

If you don't use this convention the rest of the syntax highlighting will still work and prove useful. If someone out there *is* a regex expert and would like to assist on this front, the help would be very welcome.

Function formatting is also a convention affected by filemaker.vim. I generally format functions with the following rules:

- Single parameter functions appear on a single line.
- Mult-parameter functions generally have each of their parameters on their own line.
- Parameters are indented by two spaces more than their function.
- There's no space between a function name and the opening parenthesis.
- There's a space between the parentheses and the parameters.
- There's no space between a parameter and its following semicolon.
- When multiple parameters appear on a single line there's a space between the semicolon and the next parameter.

filemaker.vim, by default, follows these conventions strictly. I'll admit that this isn't always the best option for readibility (which is the purpose of my general conventions), but for an early version it was easiest to use the same conventions across the board.

Some customization is possible, however, and I plan to include more down the road. For the time being you can override two of the defaults by setting global variables within your `.vimrc` file. 

    set g:FMVAddSpaceAfterFunction=1 " places a space between a function name and the opening parenthsis
    set g:FMVPadSpacesWithinParens=0 " does not place a space between parentheses and parameters

See the help file (`:help fmv-overriding-conventions`) for additional information.

Future Enhancements
-------------------

This is version 1, and it does most of what I set out to do to make it useful, but I do have plans for future features, and am very interested in feedback regarding their anticipated usefulness as well as their priority.

- Recognition of any calculation variable (i.e., no need to prepend an underscore)
- Recognition of any custom or external function (i.e., no need to prepend a code followed by a dot)
- Addition of an indent file that allows for automatic formatting of calculations
- Ability to customize triggers without having to edit the original snippets file
- Ability to provide variable triggers for fuctions such as `Case` and `Substitute`
- Integrated function documentation
- Integration with other Vim plugins, such as [YouCompleteMe](https://github.com/Valloric/YouCompleteMe)
- Optional inclusion of popular FileMaker plugin external functions
- Optional inclusion of a standard library of custom function snippets
- Are FileMaker functions language-dependent? If so, multiple language support
- Syntax recognition for languages commonly embedded within FileMaker strings (SQL, Groovy, PHP, JavaScript, AppleScript)

Snippet Triggers
----------------

Every included function (except the `Get` function's parameters and `DatabaseNames`, for which such a snippet is pretty useless) has a snippet that is the same as the function's name in lower-case letters. So you know right away that the trigger for `RightValues` is `rightvalues`, but most have abbreviated but unique triggers (`ritv` in this case). Although UltiSnips supports duplicate triggers, using them seriously reduces the time savings, so if a function has a trigger, that trigger is unique. When selecting between competing functions I tried to make the most common function the one with the most obvious trigger.

The triggers for `Get` functions are generally `get` followed by the letters in the words making up the parameter, such as `getfp` for `Get( FilePath )`, but using that technique does result in some duplicates. When that's the case I tried to use the default on the more common function and added a logical letter to the alternative.

Finally, triggers are *generally* case-insenstive. In other words, `getv`, `Getv`, and `GETV` are all triggers for the `GetValue` function.

To find the abbreviated trigger use the help system with the function name, as in `:help fmv-filter`.
