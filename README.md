# Elixir Installation

## Installation

### Windows

Download the installer from [elixir-lang.org](https://elixir-lang.org/install.html#windows) and run it.

You need to add the bin folders of the installation path to the PATH environment variables.

``` environment variables
C:\Program Files\Erlang OTP\bin
C:\Program Files\elixir\bin
%USERPROFILE%\.mix\escripts
```

#### Check installed version

```powershell
elixir -v
Erlang/OTP 25 [erts-13.0.4] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:1] [jit:ns]

Elixir 1.14.2 (compiled with Erlang/OTP 25)

# mix is a build tool that comes with Elixir
mix -v
Erlang/OTP 25 [erts-13.0.4] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:1] [jit:ns]

Mix 1.14.2 (compiled with Erlang/OTP 25)
```

#### Interactive mode

When you run `iex` it will start an interactive shell. However, it will not load correctly from PowerShell.

```powershell
iex
cmdlet Invoke-Expression at command pipeline position 1
Supply values for the following parameters:
Command: 2+3
5
PS C:\Users\nagar\Development\Elixir>
```

You need to fix `iex.bat` works correctly.

```powershell
> Get-Command iex

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           iex -> Invoke-Expression

> Get-Command cmd

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Application     cmd.exe                                            10.0.1904… C:\WINDOWS\system32\cmd.exe

> Get-Command -All iex -Syntax
iex (alias) -> Invoke-Expression

iex [-Command] <string> [<CommonParameters>]

C:\Program Files (x86)\Elixir\bin\iex.bat
C:\Program Files (x86)\Elixir\bin\iex

> Remove-Item alias:\iex -Force
```

[Cannot run elixir application from powershell](https://stackoverflow.com/questions/40011452/cannot-run-elixir-application-from-powershell)

Now you can run `iex.bat` from PowerShell.

```powershell
> iex.bat
Interactive Elixir (1.14.2) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> 2 + 3
5
iex(2)>
```

#### Run a file

```powershell
elixir hello.exs
```

#### Clear iex console screen on Windows

```powershell
iex(23)> clear/0
Cannot clear the screen because ANSI escape codes are not enabled on this shell
** (ArithmeticError) bad argument in arithmetic expression: :"do not show this result in output" / 0
    :erlang./(:"do not show this result in output", 0)
    iex:23: (file)

# iex(23)> :os.cmd('cls')
# :ok

ex(23)> Application.put_env(:elixir, :ansi_enabled, true)
:ok

iex(24)> clear/0
:ok
** (ArithmeticError) bad argument in arithmetic expression: :"do not show this result in output" / 0
    :erlang./(:"do not show this result in output", 0)
    iex:24: (file)
iex(24)>
```

[Clear screen in an iex session?](https://elixirforum.com/t/clear-screen-in-an-iex-session/29014/3)
