# set window title
PS1='\[\033]0;Git-Bash: ${PWD//[^[:ascii:]]/?}\007\]'
PS1="$PS1"'\n'                 # new line
PS1="$PS1"'\[\033[32m\]'       # change to green
PS1="$PS1"'➜ '                # ➜
PS1="$PS1"'\[\033[0m\]'        # change color
MSYS2_PS1="$PS1"




  Let us start by modifying the title. I like to keep something like Git-Bash with the current working directory in the title. For this, remove $TITLEPREFIX from the line PS1='\[\033]0;$TITLEPREFIX:${PWD//[^[:ascii:]]/?}\007\]' and add something like this PS1='\[\033]0;Git-Bash: ${PWD//[^[:ascii:]]/?}\007\]'. This will change the title to “Git-Bash: path to current working directory”.

Next, remove the whole if section since we have added a custom title: Bash

if test -f /etc/profile.d/git-sdk.sh
then
    TITLEPREFIX=SDK-${MSYSTEM#MINGW}
else
    TITLEPREFIX=$MSYSTEM
fi
Next, removing the following lines will remove MINGW64 from the prompt:

PS1="$PS1"'\[\033[35m\]' # change to purple

PS1="$PS1"'$MSYSTEM ' # show MSYSTEM

Things like PS1="$PS1"'\[\033[32m\]'  are used to set the colour of the string that follows. [32m\] denotes that the colour has to be green. Here are few colours that can be applied:

#	COLOUR
30	Black
31	Red
32	Green
33	Yellow
34	Blue
35	Magenta
36	Cyan
37	White
VSCode has it’s own Git integration, so I do not need my command  promp to show me any git related details like brank or uncommitted files  etc. So I removed the following lines to disable git support. Yes I  know that kind of beats the purpose of “git” bash, but then VSCode  already gives me everything. Bash

if test -z "$WINELOADERNOEXEC"
then
    GIT_EXEC_PATH="$(git --exec-path 2>/dev/null)"
    COMPLETION_PATH="${GIT_EXEC_PATH%/libexec/git-core}"
    COMPLETION_PATH="${COMPLETION_PATH%/lib/git-core}"
    COMPLETION_PATH="$COMPLETION_PATH/share/git/completion"
    if test -f "$COMPLETION_PATH/git-prompt.sh"
    then
        . "$COMPLETION_PATH/git-completion.bash"
        . "$COMPLETION_PATH/git-prompt.sh"
        PS1="$PS1"'\[\033[36m\]'  # change color to cyan
        PS1="$PS1"'`__git_ps1` '   # bash function
    fi
fi
After all the editing, this is how your file should look like: Bash

# set window title
PS1='\[\033]0;Git-Bash: ${PWD//[^[:ascii:]]/?}\007\]'
PS1="$PS1"'\n'                 # new line
PS1="$PS1"'\[\033[32m\]'       # change to green
PS1="$PS1"'➜ '                # ➜
PS1="$PS1"'\[\033[0m\]'        # change color
MSYS2_PS1="$PS1"               # for detection by MSYS2 SDK's bash.basrc
This is how it looks like after all the cosmetic changes:

Final Git-Bash
Final Git-Bash
So there you have it, your wonderful looking git-bash nicely  integrated with your VSCode. Go play around with it, add your own  symbols to the prompt using character  

