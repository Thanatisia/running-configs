# Configuration dotfile usages

## Installation
### Neovim
- Change directory into 'src/configs-neovim'
    ```bash
    cd src/configs-neovim
    ```

- Operating System/Platform
    - Linux
        - Copy the 'src/' directory to '~/.configs/nvim'
            ```bash
            cp -rv src/ ~/.configs/nvim
            ```
        - (Optional) Work with a custom shell environment
            - Create a custom bashshell
                ```bash
                : " 
                Start in portable mode
                "
                ## [User Environment Space]
                ### User Variables
                user="$USERNAME"
                datafldr="data/$user"
                progfldr="/path/to/nvim"
                datapath=$progfldr/$datafldr
                personalfldr=$datapath/nvim/vimfiles
                LSP_Path="/path/to/your/LSP/directory/root"

                ### Compilation
                LSP_servers_bin="$LSP_Path/Lua/lua-language-server/lua-language-server-[version]-win32-x64/bin/;$LSP_Path/Markdown/Marksman/v[version]:$LSP_Path/C++/LSP/LLVM-[version]-win64/LLVM/bin/"

                ### Prepare Workspace
                #### Create userspace portable data folder if folder doesnt exists
                if [[ ! -d "$datapath" ]]; then
                    # If folder does not exist
                    echo -e "Creating: $datapath"
                    mkdir -pv "$datapath"
                fi

                if [[ ! -d "$progfldr" ]]; then
                    # If folder does not exist
                    echo -e "Creating: $progfldr"
                    mkdir -pv "$progfldr"
                fi

                #### Local Variables
                other_paths="$LSP_servers_bin:$progfldr/Neovim/bin:"

                #### Set Environment Variables]
                ##### For Portability

                #### Change Roaming APPDATA folder to another directory of your choice
                PATH+="$other_paths:"
                APPDATA="$datapath"
                LOCALAPPDATA="$datapath"

                #### Get Environment Variables

                #### Program Variables
                function main() {
                    PROG_FLDR=/usr/local/bin/
                    PROG_FILE="nvim"
                    PROG_PARAMS=("$@")
                    # PROG_RUN= 

                    #### Main (Processing)
                    echo -e "User : $user"
                    echo -e "System Path : $PATH"
                    echo -e "APPDATA (Roaming) : $APPDATA"
                    echo -e "Running : $PROG_RUN"

                    echo -e ""

                    "$PROG_FLDR/$PROG_FILE" "${PROG_PARAMS[@]}" && \
                        echo -e $PROG_RUN ran successfully || \
                        echo -e error running $PROG_RUN

                    #### Output
                    read -p "Paused."
                }

                if [[ "${BASH_SOURCE[0]}" == "${0}" ]]; then
                    echo -e "$@"
                    main $@
                fi
                ```
            - Source the shell
                ```bash
                source /path/to/shell/script
                ```
    - Windows
        - Copy the 'src/' directory to a dedicated '/path/to/nvim' directory of your choice
            ```bash
            cp -rv src/ /path/to/nvim
            ```
        - (Optional) Work with a custom shell environment
            - Create a custom batch (dos) shell
                + This when ran will start in portable mode
                + Please replace all elements with '[version]'
                ```console
                @echo off
                SETLOCAL EnableDelayedExpansion

                :: [User Environment Space]
                :: User Variables
                SET user=%USERNAME%
                SET datafldr=data\%user%
                SET progfldr=%USERPROFILE%\path\to\your\nvim\project\root
                SET datapath=%progfldr%\%datafldr%
                SET personalfldr=%datapath%\nvim\vimfiles
                SET LSP_Path=\path\to\LSP\directory\root

                :: Compilation
                SET LSP_servers_bin=%LSP_Path%\Lua\lua-language-server\lua-language-server-[version]-win32-x64\bin\;%LSP_Path%\Markdown\Marksman\[version];%LSP_Path%\C++\LSP\LLVM-[version]-win64\LLVM\bin\

                :: Prepare Workspace
                :: Create userspace portable data folder if folder doesnt exists
                IF NOT EXIST "%datapath%" (
                    :: If folder does not exist
                    mkdir "%datapath%"
                )
                IF NOT EXIST "%progfldr%" (
                    :: If folder does not exist
                    mkdir "%progfldr%"
                )

                :: [Local Variables]
                SET other_paths=%LSP_servers_bin%;%progfldr%\Neovim\bin;%USERPROFILE%\Desktop\Portable\Utilities\NodeJS\node-[version]-win-x64;

                :: [Set Environment Variables]
                :: For Portability

                :: Change Roaming APPDATA folder to another directory of your choice
                SET PATH=%other_paths%;%PATH%
                SET APPDATA=%datapath%
                SET LOCALAPPDATA=%datapath%

                :: [Get Environment Variables]

                :: [Program Variables]
                SET PROG_FLDR=%progfldr%\Neovim\bin
                SET PROG_FILE=nvim.exe
                SET PROG_PARAMS=%*
                SET PROG_RUN="%PROG_FLDR%\%PROG_FILE%" %PROG_PARAMS%

                :: Main (Processing)
                echo User : %user%
                echo System Path : %PATH%
                echo APPDATA (Roaming) : %APPDATA%
                echo Running : %PROG_RUN%

                echo/

                %PROG_RUN% && (
                    echo %PROG_RUN% ran successfully.
                ) || (
                    echo error running %PROG_RUN%. 
                )

                echo/

                :: Output
                pause
                ```
            - Source the shell
                ```console
                .\path\to\your\shell\script{.bat}
                ```
        - (Optional) If you are using bash from msys2 or GitPortable
            - Copy the example .bashrc file provided by the project to the home directory (%HOMEDIR%)
                - msys2
                    - Notes
                        + msys2 is a collection of software including (a build of) MinGW{-w64} while
                        + mingw{-w64} has a compiler
                    - Using batch
                        ```console
                        cp \path\to\msys\[version]\etc\.bash_profile %USERPROFILE%/.bashrc
                        ```
                    - Using bash
                        ```bash
                        cp -v /path/to/msys/[version]/etc/.bash_profile $HOME/.bashrc
                        ```
                - {Portable}Git
                    - Using batch
                        ```console
                        cp \path\to\Git\etc\.bash_profile %USERPROFILE%/.bashrc
                        ```
                    - Using bash
                        ```bash
                        cp -v /path/to/Git/etc/bash.bashrc $HOME/.bashrc
                        ```
            - Customize the custom bashrc file for your bash shell
                - Set Environment Variables
                    ```bash
                    ENV_VAR="value"
                    ```
                - Append system paths accordingly
                    ```bash
                    PATH+="your:new:paths:"
                    ```
                - Set alias mappings
                    ```bash
                    alias alias_program="command"
                    ```
            - Reload the shell
                ```bash
                source ~/.bashrc
                ```
        - (Optional) If you are using Windows Terminal
            - (Optional) Create a new profile for the bash shell
                + Press the hotkey keybind '<Ctrl+,>'
                - Press 'Add a new profile'
                    + Press 'New empty profile'
                    - Default Recommended Changes
                        > You can leave the others as default, however at the very least, the following should be changed 
                        + Name : Set the name of the new profile
                        + Command line : Set the shellscript/executable to be executed when started (i.e. custom shell script)
                        - Starting directory : Set your custom starting directory here; You can specify this directly in your custom shellscript (if you are using)
                            - Default Environment Variables
                                + Windows - Current user's Home drive and Home directory: %USERPROFILE%
                    + Save changes

### Tmux
- Change directory into 'src/configs-tmux'
    ```bash
    cd src/configs-tmux
    ```

- Operating System/Platform
    - Linux
        - Copy the tmux configuration file '.tmux.conf' to the home directory root ('~/' | '$HOME')
            ```bash
            cp .tmux.conf $HOME
            ```
        - Copy the tmux custom configuration subdirectory (referenced by .tmux.conf) to the home directory configurations directory ('~/.configs')
            ```bash
            cp -rv tmux $HOME/.configs
            ```
        - Startup tmux
            ```bash
            tmux new -s [session-name]
            ```
        - Perform initial startup pre-requisite sequence
            - Install plugins
                - Pressing the keybinding '[Prefix] + I'
                    + Prefix = Ctrl+B

## Wiki

## Resources

## References

## Remarks

