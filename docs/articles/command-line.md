---
uid: articles.command_line
---

# The Command Line

BSIPA has 2 command lines: the installer, and the game.

Their documentation is below.

## [The Installer (`IPA.exe`)](#tab/installer)

The installer has quite a few options, which are documented inline with the `-h` or `--help` flag.

This is what it currently looks like:

[!code[IPA command line](_ipa_command_line.txt "the result of IPA.exe -h")]

## [The Game](#tab/game)

The game *also* gets quite a few command line options, though there isn't anything as convenient as a help page for them.

Here's a quick list of what they are and what they do.

- `--verbose`

  > Makes a console appear with log information at startup.
  >
  > Optionally, to start Beat Saber with an external console, an explicit `-pid` can be specified. This allows the game to be launched without being interrupted by Steam's "Allow game launch?" popup when directly launching `Beat Saber.exe` with arguments.
  > - Using PowerShell: 
  >   ```powershell
  >   .\steam -applaunch 620980 --verbose -pid $PID
  >   ```
  > - Using Command Prompt:
  >   ```powershell
  >   powershell -c ".\steam -applaunch 620980 --verbose -pid (Get-CimInstance Win32_Process -Filter ProcessId=$PID).ParentProcessId"
  >   ```
  >

- `--debug`

  > Enables the loading of debug information in Mono. The debugging information must be in the portable PDB format,
  > in the same location as the DLL that it's for.
  >
  > This option also forces BSIPA to show all debug messages in the console, as well as where they were called.
  >
  > This overrides the config settings `Debug.ShowDebug` and `Debug.ShowCallSource`.
  >

- `--trace`
  
  > Enables trace level messages. By default, they do not ever enter the message queue, and thus cost almost nothing.
  > When this or the config option is used, they are added and logged with the same rules as Debug messages.
  >
  > This overrides the config setting `Debug.ShowTrace`.
  >

- `--mono-debug`

  > Enables the built-in Mono soft debugger engine.
  >
  > By default, it acts as a client, and requires that there be a soft
  > debugger server running on port 10000 on `localhost`.
  >
  > Implies `--debug`.
  >

- `--server`

  > Does nothing on its own.
  >
  > When paired with `--mono-debug`, this option makes the Mono soft debugger act in server mode. It begins listening on
  > port 10000 on any address, and will pause startup (with no window) until a debugger is connected. I recommend using
  > SDB, but that is a command line debugger and a lot of people don't care for those.
  >

- `--no-yeet`

  > Disables mod yeeting.
  >
  > By default, whenever BSIPA detects that the game is now running a newer version than previous runs, it will move all
  > mods to another folder and not load them. (They still get checked for updates though.) When this is enabled, that
  > behaviour is disabled.
  >
  > Overrides the config setting `YeetMods`.
  >

- `--condense-logs`

  > Reduces the number of log files BSIPA will output for a given session.
  >
  > By default, BSIPA will create a subfolder in the `Logs` folder for each mod sublog, as well as each mod. This disables
  > that behaviour, and restricts it to only create a global log and mod logs.
  >
  > Overrides the config setting `Debug.CondenseModLogs`.

- `--plugin-logs`
  
  > Causes each plugins' log messages to be written to files in their own folder for ease of debugging.
  >
  > This was the default through 4.1.6, however is now disabled by default.
  >
  > Overrides the config setting `Debug.CreateModLogs`.
  
***
