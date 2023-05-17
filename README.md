# README for pdfsizeopt

pdfsizeopt is a program for converting large PDF files to small ones,
without decreasing visual quality or removing interactive features (such as
hyperlinks). More specifically, pdfsizeopt is a free, cross-platform
command-line application (for Linux, Windows, macOS and Unix) and a
collection of best practices to optimize the size of PDF files, with focus
on PDFs created from TeX and LaTeX documents. pdfsizeopt is written in
Python, so it is a bit slow, but it offloads some of the heavy work to its
faster (C, C++ and Java) dependencies.

Doesn't pdfsizeopt work with your PDF?
Report the issue here: https://github.com/pts/pdfsizeopt/issues

Send donations to the author of pdfsizeopt:
https://flattr.com/submit/auto?user_id=pts&url=https://github.com/pts/pdfsizeopt

## Getting started: how to run pdfsizeopt

If it is your first time trying pdfizeopt, follow these instructions.
(This section was updated on 2023-02-15.)

It's easy to install and run pdfsizeopt on modern Linux and Windows systems
with an x86 processor. If you have such a system, jump directly to one of
the following sections (*Installation instructions and usage on Linux* or
*Installation instructions and usage on Windows*). It will take less than
5 minutes.

It's easy to install and run pdfsizeopt on a Mac (both Intel x86 processors
and ARM processors with Apple Silicon are supported). If you have such a
system, jump directly to the section *Installation instructions and usage
on macOS* (*not* using Docker). It will take less than 5 minutes.

Alternatively (but not recommended because it's slower), it's possible to
run pdfsizeopt within Docker on the following systems: Linux amd64, macOS
64-bit Intel x86 (amd64, x86_64), macOS 64-bit ARM (Apple Silicon, e.g. M1
or M2 chip). After that, jump directly to the section *Installation
instructions and usage with Docker on Linux and macOS*. That last step will
take less than 5 minutes.

If you are using an operating system other than Linux, Windows or macOS (on
a computer with Intel processor), the easiest way to try pdfsizeopt is
borrowing a friend's computer with Linux, Windows or macOS, or renting a
Linux VM in the cloud. The reason why it's difficult to run pdfsizeopt on
other kinds of systems is because pdfsizeopt has some required dependencies,
some of them are old versions (e.g. Python 2.4--2.7, Ghostscript 9.05), so
you'll have to compile the right versions of the dependencies first, which
may take several hours and lots of frustrating trial-and-error even for
experienced hackers.

It's technically possible to port pdfsizeopt to other systems (and make it
easy to install), but the author of pdfsizeopt doesn't have the free time to
create and maintain such a port. As an FYI, see
https://github.com/pts/pdfsizeopt/issues/154 about porting to Apple Silicon.

## Running on GitHub Codespaces

Codespaces is free on GitHub thus you can use pdfsizeopt without installing anything.

1) Click on the green Code button and select Codespaces. You can go with the default Codespace.
2) When the Codespace opens, click on Terminal and paste this in. Alternatively if you fork, the pdfsizeopt repo, you can save the below as `setup.sh` and run `sh setup.sh`.
```
mkdir ~/pdfsizeopt
cd ~/pdfsizeopt
wget -O pdfsizeopt_libexec_linux.tar.gz https://github.com/pts/pdfsizeopt/releases/download/2023-04-18/pdfsizeopt_libexec_linux-v9.tar.gz
tar xzvf pdfsizeopt_libexec_linux.tar.gz
rm -f    pdfsizeopt_libexec_linux.tar.gz
wget -O pdfsizeopt.single https://raw.githubusercontent.com/pts/pdfsizeopt/master/pdfsizeopt.single
chmod +x pdfsizeopt.single
ln -s pdfsizeopt.single pdfsizeopt
```
3) The right-click and upload your PDF file.
4) Now you can run 
```
  ~/pdfsizeopt/pdfsizeopt input.pdf output.pdf
```
5) Download your file by right-clicking on the file.

## Installation instructions and usage on Linux

There is no installer, you need to run some commands in the command line to
download and install. pdfsizeopt is a command-line only application, there
is no GUI.

To install pdfsizeopt on a Linux system (with architecture i386 or amd64),
open a terminal window and run these commands (without the leading `$`):

```
  $ mkdir ~/pdfsizeopt
  $ cd ~/pdfsizeopt
  $ wget -O pdfsizeopt_libexec_linux.tar.gz https://github.com/pts/pdfsizeopt/releases/download/2023-04-18/pdfsizeopt_libexec_linux-v9.tar.gz
  $ tar xzvf pdfsizeopt_libexec_linux.tar.gz
  $ rm -f    pdfsizeopt_libexec_linux.tar.gz
  $ wget -O pdfsizeopt.single https://raw.githubusercontent.com/pts/pdfsizeopt/master/pdfsizeopt.single
  $ chmod +x pdfsizeopt.single
  $ ln -s pdfsizeopt.single pdfsizeopt
```

To optimize a PDF, run the following command:

```
  ~/pdfsizeopt/pdfsizeopt input.pdf output.pdf
```

If the input PDF has many images or large images, pdfsizeopt can be very
slow. You can speed it up by disabling pngout, the slowest image optimization
method, like this:

```
  ~/pdfsizeopt/pdfsizeopt --use-pngout=no input.pdf output.pdf
```

pdfsizeopt creates lots of temporary files (psotmp.*) in the output
directory, but it also cleans up after itself.

It's possible to optimize a PDF outside the current directory. To do that,
specify the pathname (including the directory name) in the command-line.

Please note that the commands above download all dependencies (including
Python and Ghostscript) as well. It's possible to install some of the
dependencies with your package manager, but these steps are considered
alternative and more complicated, and thus are not covered here.

Please note that pdfsizeopt works perfectly on any x86 and amd64 Linux
system. There is no restriction on the libc, Linux distribution etc. because
pdfsizeopt uses only its statically linked x86 executables, and it doesn't
use any external commands (other than pdfsizeopt, pdfsizeopt.single and
pdfsizeopt_libexec/*) on the system. pdfsizeopt also works perfectly on x86
FreeBSD systems with the Linux emulation layer enabled.

To avoid typing ~/pdfsizeopt/pdfsizeopt, add "$HOME/pdfsizeopt" to your PATH
(probably in your ~/.bashrc), open a new terminal window, and the
command pdfsizeopt will work from any directory.

You can also put pdfsizeopt to a directory other than ~/pdfsizeopt , as you
like.

Additionally, you can install some extra image imptimizers (see more in the
*Image optimizers* section below):

```
  $ cd ~/pdfsizeopt
  $ wget -O pdfsizeopt_libexec_extraimgopt_linux-v3.tar.gz https://github.com/pts/pdfsizeopt/releases/download/2017-01-24/pdfsizeopt_libexec_extraimgopt_linux-v3.tar.gz
  $ tar xzvf pdfsizeopt_libexec_extraimgopt_linux-v3.tar.gz
  $ rm -f    pdfsizeopt_libexec_extraimgopt_linux-v3.tar.gz
```

## Installation instructions and usage on Windows

There is no installer, you need to run some commands in the command line
(black Command Prompt window) to download and install. pdfsizeopt is a
command-line only application, there is no GUI.

Create folder C:\pdfsizeopt, download
https://github.com/pts/pdfsizeopt/releases/download/2023-04-18/pdfsizeopt_win32exec-v9.zip
, and extract its contents to the folder C:\pdfsizeopt, so that the file
C:\pdfsizeopt\pdfsizeopt.exe exists.

Download
https://raw.githubusercontent.com/pts/pdfsizeopt/master/pdfsizeopt.single
and save it to C:\pdfsizeopt, as C:\pdfsizeopt\pdfsizeopt.single .

To optimize a PDF, run the following command:

```
  C:\pdfsizeopt\pdfsizeopt input.pdf output.pdf
```

in the command line, which is a black Command Prompt window, you can start
it by Start menu / Run / cmd.exe, or finding Command Prompt in the start
menu.

(Press Tab to get filename completion while typing.)

Since you have to type the input filename as a full pathname, it's
recommended to create a directory with a short name (e.g. C:\pdfs), and copy
the input PDF there first.

If the input PDF has many images or large images, pdfsizeopt can be very
slow. You can speed it up by disabling pngout, the slowest image optimization
method, like this:

```
  C:\pdfsizeopt\pdfsizeopt --use-pngout=no input.pdf output.pdf
```

To avoid typing C:\pdfsizeopt\pdfsizeopt, add C:\pdfsizeopt to (the end of)
the system PATH, open a new Command Prompt window, and the command
`pdfsizeopt` will work from any directory.

Depending on your environment, filenames with
accented characters may not work in the Windows version of pdfsizeopt. To
play it safe, make sure your input and output files have names with letters,
numbers, underscore (_), dash (-), dot (.) and plus (+). The backslash (\)
and the slash (/) are both OK as the directory separator.

Spaces in filenames and pathnames should work, but you need to put double
quotes (") around the name.

Filenames with some punctuation characters (such as double quote ("),
question mark (?) and asterisk (*)) and nonprintable characters (such as
newline) will not work on Windows. This is because Windows doesn't support
these characters ([\x00..\x1f\"*:<>?|\x7f] in filenames at all, and it uses
/ and \\ as directory separator.

You can also put pdfsizeopt to a directory other than C:\pdfsizeopt , but it
won't work if there is whitespace or there are accented characters in any of
the folder names.

Please note that pdfsizeopt works perfectly in Wine (tested with wine-1.2 on
Ubuntu Lucid and wine-1.6.2 on Ubuntu Trusty), but it's a bit slower than
running it natively (as a Linux or Unix program).

## Installation instructions and usage with Docker on Linux and macOS

These instructions work on the following systems: Linux amd64, macOS 64-bit
Intel x86 (amd64, x86_64), macOS 64-bit ARM (Apple Silicon, e.g. M1 or M2
chip). The version of Linux or macOS doesn't matter (old systems such as
macOS Leopard 10.5 also work), as long as it has Docker installed and
working.

The programs in the Docker image ptspts/pdfsizeopt are compiled for Linux
i386 (32-bit Intel x86), and these binaries happen to work in all platforms
mentioned above, even with Apple Silicon. (Tested on 2023-02-21.)

There is no installer, you need to run some commands in the command line to
download and install. pdfsizeopt is a command-line only application, there
is no GUI.

First, check that you have Docker installed properly by running this
command and checking for the OK at the end:

```
  docker version && echo OK
```

If you don't get OK, because the `docker' command was not found, then Docker
is not installed to your computer. Installation instructions (on 2023-02-22):

* To install Docker on Linux, you have two options: Docker Engine
  (https://docs.docker.com/engine/install/ , within the Server section) or
  Docker Desktop (https://docs.docker.com/desktop/install/linux-install/). Any
  of them would work.

* To install Docker on macOS, install Docker Desktop
  (https://docs.docker.com/desktop/install/mac-install/).

  Then (on macOS), add the `docker` command to your PATH by running the
  following command (copy-paste it, don't type, to avoid typos):

  ```
    (echo; echo 'export PATH="/Applications/Docker.app/Contents/Resources/bin:$PATH"') >>~/.profile
  ```

  Then (on macOS), close the Terminal app, and open it again (so that
  changes to ~/.profile take effect).

* After the installation, retry the `docker version` command above.

Remove any previous Docker images of pdfsizeopt:

```
  docker image rm ptspts/pdfsizeopt
```

Do a test optimization run, which exercises all dependencies of pdfsizeopt:

```
  curl -L -o deptest.pdf https://github.com/pts/pdfsizeopt/raw/master/deptest/deptest.pdf
  docker run -v "$PWD:/workdir" -u "$(id -u):$(id -g)" --rm -it ptspts/pdfsizeopt pdfsizeopt deptest.pdf
```

If you get a (harmless) warning message like

```
  WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
```

, and you don't want to get it again, then add `--platform linux/amd64` after the `-it`:

```
  docker run -v "$PWD:/workdir" -u "$(id -u):$(id -g)" --rm -it --platform linux/amd64 ptspts/pdfsizeopt pdfsizeopt deptest.pdf
```

To optimize a PDF, run this command:

```
  docker run -v "$PWD:/workdir" -u "$(id -u):$(id -g)" --rm -it ptspts/pdfsizeopt pdfsizeopt input.pdf output.pdf
```

If the input PDF has many images or large images, pdfsizeopt can be very
slow. You can speed it up by disabling pngout, the slowest image optimization
method, like this:

```
  docker run -v "$PWD:/workdir" -u "$(id -u):$(id -g)" --rm -it ptspts/pdfsizeopt pdfsizeopt --use-pngout=no input.pdf output.pdf
```

pdfsizeopt creates lots of temporary files (psotmp.*) in the output
directory, but it also cleans up after itself.

It's possible to optimize a PDF outside the current directory. To do that,
specify the pathname (including the directory name) in the command-line.

To avoid typing a long command, run

```
  (echo '#! /bin/sh'; echo 'exec docker run -v "$PWD:/workdir" -u "$(id -u):$(id -g)" --rm -it ptspts/pdfsizeopt pdfsizeopt "$@"') >pdfsizeopt && chmod 755 pdfsizeopt
```

, and then copy the pdfsizeopt script to your PATH, then open a new terminal
window, and now this command will also work to optimize a PDF:

```
  pdfsizeopt input.pdf output.pdf
```

Please note that the ptspts/pdfsizeopt Docker image is updated very rarely.
To use a more up-to-date version of pdfsizeopt, run these commands to download:

```
  curl -L -o pdfsizeopt.single https://raw.githubusercontent.com/pts/pdfsizeopt/master/pdfsizeopt.single
  chmod +x pdfsizeopt.single
```

Then run this command to optimize a PDF:

```
  docker run -v "$PWD:/workdir" -u "$(id -u):$(id -g)" --rm -it ptspts/pdfsizeopt ./pdfsizeopt.single --use-pngout=no input.pdf output.pdf
```

If you want to have extra image optimizers included on Linux, use
ptspts/pdfsizeopt-with-extraimgopt instead of ptspts/pdfsizeopt in the
commands above. Example:

```
  docker run -v "$PWD:/workdir" -u "$(id -u):$(id -g)" --rm -it ptspts/pdfsizeopt-with-extraimgopt pdfsizeopt --use-image-optimizer=sam2p,jbig2,pngout,zopflipng,optipng,advpng,ECT input.pdf output.pdf
```

## Installation instructions and usage on macOS

These instructions work on Macs with macOS Catalina 10.15 (and even
older, maybe macOS Snow Leopard 10.6) -- macOS Ventura 13 (and even newer),
having a 64-bit ARM processor (Apple Silicon) or a 64-bit Intel x86
(x86_64, amd64) processor. The programs are compiled for 64-bit Intel x86
processors, and they work on 64-bit ARM processors as well, using the
Rosetta 2 emulation in macOS. These instructions were tested and known to
work on macOS Ventura 13.3, both with 64-bit Intel x86 (x86_64, amd64)
processor and Apple Silicon (ARM processor).

If you have an older Mac running Mac OS X Leopard 10.5 -- macOS Mojave
10.14, follow the section *Installation instructions and usage on older
macOS* instead.

These instructions are not tested yet. See
https://github.com/pts/pdfsizeopt/issues/154 for progress updates.

There is no installer, you need to run some commands in the command line to
download and install. pdfsizeopt is a command-line only application, there
is no GUI.

To install pdfsizeopt on a macOS system, open a terminal window and run
these commands (without the leading `$`):

```
  $ mkdir ~/pdfsizeopt
  $ cd ~/pdfsizeopt
  $ curl -L -o pdfsizeopt_libexec_darwin.tar.gz https://github.com/pts/pdfsizeopt/releases/download/2023-04-18/pdfsizeopt_libexec_darwinc64-v9.tar.gz
  $ tar xzvf pdfsizeopt_libexec_darwin.tar.gz
  $ rm -f    pdfsizeopt_libexec_darwin.tar.gz
  $ curl -L -o pdfsizeopt.single https://raw.githubusercontent.com/pts/pdfsizeopt/master/pdfsizeopt.single
  $ chmod +x pdfsizeopt.single
  $ ln -s pdfsizeopt.single pdfsizeopt
```

Do a test optimization run, which exercises all dependencies of pdfsizeopt:

```
  $ curl -L -o deptest.pdf https://github.com/pts/pdfsizeopt/raw/master/deptest/deptest.pdf
  $ ~/pdfsizeopt/pdfsizeopt deptest.pdf
```

... and open (view) deptest.pdf and the corresponding optimized
deptest.pso.pdf .

To optimize a PDF, run the following command:

```
  ~/pdfsizeopt/pdfsizeopt input.pdf output.pdf
```

If the input PDF has many images or large images, pdfsizeopt can be very
slow. You can speed it up by disabling pngout, the slowest image optimization
method, like this:

```
  ~/pdfsizeopt/pdfsizeopt --use-pngout=no input.pdf output.pdf
```

Also, if you have an 32-bit Mac, then the pngout bundled with pdfsizeopt
won't work (because it needs a 64-bit Mac), so you have to force
--use-pngout=no . See the section *Image optimizers* for alternatives of
pngout.

pdfsizeopt creates lots of temporary files (psotmp.*) in the output
directory, but it also cleans up after itself.

It's possible to optimize a PDF outside the current directory. To do that,
specify the pathname (including the directory name) in the command-line.

Please note that the commands above download most dependencies (including
Ghostscript, but excluding Python) as well. Everything should work as
instructed above, out of the box. If you are experiencing problems, please
report an issue on https://github.com/pts/pdfsizeopt/issues .

To avoid typing ~/pdfsizeopt/pdfsizeopt, add "$HOME/pdfsizeopt" to your PATH
(probably in your ~/.bashrc), open a new terminal window, and the
command pdfsizeopt will work from any directory.

You can also put pdfsizeopt to a directory other than ~/pdfsizeopt , as you
like.

## Installation instructions and usage on older macOS

These instructions should work on older Macs running Mac OS X Leopard 10.5
-- macOS Mojave 10.14, and having a 32-bit or 64-bit Intel x86 processor. The
programs are compiled for 32-bit Intel x86 (i386) processor (and also work
on a 64-bit Intel processor with macOS Mojave 10.14 or earlier), except for
the pngout tool, which needs at least Mac OS X Snow Leopard 10.6 and a
64-bit Intel processor.

There is no installer, you need to run some commands in the command line to
download and install. pdfsizeopt is a command-line only application, there
is no GUI.

To install pdfsizeopt on an older macOS system, open a terminal window and
run these commands (without the leading `$`):

```
  $ mkdir ~/pdfsizeopt
  $ cd ~/pdfsizeopt
  $ curl -L -o pdfsizeopt_libexec_darwin.tar.gz https://github.com/pts/pdfsizeopt/releases/download/2023-04-18/pdfsizeopt_libexec_darwin-v9.tar.gz
  $ tar xzvf pdfsizeopt_libexec_darwin.tar.gz
  $ rm -f    pdfsizeopt_libexec_darwin.tar.gz
  $ curl -L -o pdfsizeopt.single https://raw.githubusercontent.com/pts/pdfsizeopt/master/pdfsizeopt.single
  $ chmod +x pdfsizeopt.single
  $ ln -s pdfsizeopt.single pdfsizeopt
```

Do a test optimization run, which exercises all dependencies of pdfsizeopt:

```
  $ curl -L -o deptest.pdf https://github.com/pts/pdfsizeopt/raw/master/deptest/deptest.pdf
  $ ~/pdfsizeopt/pdfsizeopt deptest.pdf
```

... and open (view) deptest.pdf and the corresponding optimized
deptest.pso.pdf .

To optimize a PDF, run the following command:

```
  ~/pdfsizeopt/pdfsizeopt input.pdf output.pdf
```

If the input PDF has many images or large images, pdfsizeopt can be very
slow. You can speed it up by disabling pngout, the slowest image optimization
method, like this:

```
  ~/pdfsizeopt/pdfsizeopt --use-pngout=no input.pdf output.pdf
```

Also, if you have a Mac with a 32-bit Intel x86 processor, then the pngout
bundled with pdfsizeopt won't work (because it needs a 64-bit processor), so
you have to force --use-pngout=no . See the section *Image optimizers* for
alternatives of pngout.

pdfsizeopt creates lots of temporary files (psotmp.*) in the output
directory, but it also cleans up after itself.

It's possible to optimize a PDF outside the current directory. To do that,
specify the pathname (including the directory name) in the command-line.

Please note that the commands above download most dependencies (including
Ghostscript, but excluding Python) as well. Everything should work as
instructed above, out of the box. If you are experiencing problems, please
report an issue on https://github.com/pts/pdfsizeopt/issues .

To avoid typing ~/pdfsizeopt/pdfsizeopt, add "$HOME/pdfsizeopt" to your PATH
(probably in your ~/.bashrc), open a new terminal window, and the
command pdfsizeopt will work from any directory.

You can also put pdfsizeopt to a directory other than ~/pdfsizeopt , as you
like.

## Installation instructions and usage on FreeBSD

There is no installer, you need to run some commands in the command line to
download and install. pdfsizeopt is a command-line only application, there
is no GUI.

pdfsizeopt works perfectly on x86 FreeBSD systems with the Linux
emulation layer enabled. So, enable the Linux emulation layer on your
FreeBSD system, and then follow the
*Installation instructions and usage on Linux*.

Alterantively, you can follow the
*Installation instructions and usage on generic Unix*, but that needs much
more work on your part (and it's inconvenient and error-prone), because you
need to install many dependencies separately, possibly compiling some of
them from source.

## Installation instructions and usage on generic Unix

Doing this is increasingly hard in 2023, because pdfsizeopt needs Python
2.4--2.7 and Ghostscript 9.05, both very old, and thus hard to install to a
modern system.

There is no installer, you need to run some commands in the command line
(black Command Prompt window) to download and install. pdfsizeopt is a
command-line only application, there is no GUI.

pdfizeopt is a Python script. It works with Python 2.4, 2.5, 2.6 and 2.7
(but it doesn't work with Python 3.x). So please install Python first.

Create a new directory named pdfsizeopt, and download this link there:
https://raw.githubusercontent.com/pts/pdfsizeopt/master/pdfsizeopt.single

Rename it to pdfsizeopt and make it executable by running the following
commands (without the leading `$`):

```
  $ cd pdfsizeopt
  $ mv pdfsizeopt.single pdfsizeopt
  $ chmod +x pdfsizeopt
```

If your Python executable is not /usr/bin/python, then edit the first line
(starting with `#!`) in the pdfsizeopt script accordingly.

Try it with:

```
  $ ./pdfsizeopt --version
  info: This is pdfsizeopt ZIP rUNKNOWN size=105366.
```

pdfsizeopt has many dependencies. For full functionality, you need all of
them. Install as many as you can, and put them to the PATH.

Dependencies:

* Python (command: python). Version 2.4, 2.5, 2.6 and 2.7 work (3.x doesn't
  work).
* Ghostscript (command: gs): Version 9.05 is recommended, 8.50 should also
  work, and some early 9.x versions such as 9.14.1 also work. The most
  recent versions don't work, especially for font optimization.
* jbig2 (command: jbig2): Install from source:
  https://github.com/pts/pdfsizeopt-jbig2
  If you are unable to install, use pdfsizeopt --use-jbig2=no .
* pngout (command: pngout): Download binaries from here:
  http://www.jonof.id.au/kenutils Source code is not available.
  If you are unable to install, use pdfsizeopt --use-pngout=no .
* imgdataopt (command: imgdataopt): Install from source:
  https://github.com/pts/imgdataopt
  To make pdfsizeopt able to use it, copy the `imgdataopt` program file as `sam2p`
  (e.g. /usr/local/bin/sam2p) to your PATH.
  If you are unable to install it, use pdfsizeopt --do-optimize-images=no .
  Some Linux distributions have sam2p binaries, but they tend to be too old.
  Alternatively, sam2p >=0.49.3 + png22pnm also works instead of imgdataopt,
  but imgdataopt is easier to install.
* The Multivalent PDF compressor (written in Java) is an optional dependency
  of pdfsizeopt, turned off by default. Don't bother installing it.

After installation, use pdfsizeopt as:

```
  $ ./pdfsizeopt input.pdf output.pdf
```

You can add the directory containing pdfsizeopt to the PATH, so the
command `pdfsizeopt` will work from any directory.

## Image optimizers

pdfsizeopt can use the following external tools to make images in embedded
PDF files smaller:

* sam2p (used by default, cannot be disabled)
* jbig2 (used by default, disable with --use-jbgi2=no)
* pngout (used by default, disable with --use-pngout=no)
* zopflipng (not enabled by default)
* optipng (not enabled by default)
* advpng (not enabled by default)
* ECT (not enabled by default)

To enable or disable any image optimizer, specify all image optimizers you
want to be enabled like this: --use-image-optimizer=optipng,jbig2 . This
will also disable the default pngout.

You can also specify custom image optimizer command patterns by specifying
separate, additional --use-image-optimier= flags, like this:

```
  --use-image-optimizer="optipng %(sourcefnq)s -o6 -fix -force %(optipng_gray_flags)s-out %(targetfnq)s"
```

You always have to specify %(targetfnq) in the command pattern.

Specify --do-debug-image-optimizers=yes to see which image optimizers are
enabled (and their full command-line) for the current run.

At startup, pdfsizeopt checks that the requested image optimizers are
available (as program files), and fails if some of them are missing. To
ignore those which are missing, specify --do-require-image-optimizers=no .

It's your (the user's) responsibility to install the image optimizers and
add them to the PATH. If you follow the installation instructions for
Windows and Linux above, the default image optimizers (sam2p, jbig2 and
pngout) will be installed for you. For Linux, there are also installation
instructions above for extra image optimizers (zopflipng, optipng, advpng
and ECT).

## Troubleshooting

### 1. pdfsizeopt fails for some fonts.

Specify --do-unify-fonts=no and --do-regenerate-all-fonts=no .

If it still fails, specify --do-optimize-fonts=no .

In either case, please report it on https://github.com/pts/pdfsizeopt/issues

### 2. pdfsizeopt fails for some images.

Specify --do-optimize-images=no .

Please report it on https://github.com/pts/pdfsizeopt/issues

### 3. pdfsizeopt is too slow processing images.

Specify --use-pngout=no . This disables pngout, which is the slowest
optimization step for images.

### 4. pdfsizeopt fails without creating the output PDF.

Please report it on https://github.com/pts/pdfsizeopt/issues , attaching the
input PDF file and the console output of pdfsizeopt. Your report is very
much appreciated.

If pdfsizeopt exits with an uncaught exception, it may leave some temporary
files (psotmp.*) behind in the current directory. You can remove these files.

Please note that pdfsizeopt is not resilient in processing corrupt PDF
files (i.e. those which are not compliant to the PDF standard). So if
pdfsizeopt fails, then the reason may be a bug in pdfsizeopt or a corrupt
PDF input file. Nevertheless, please report an issue (see above).

### 5. The output PDF of pdfsizeopt doesn't look like the same as the input PDF.

Please report it on https://github.com/pts/pdfsizeopt/issues , attaching the
input PDF file and the output PDF file (.pso.pdf) and the console output of
pdfsizeopt. Your report is very much appreciated.

### 6. pdfsizeopt is unable to find some input files on Windows.

This may happen if the filename or the full pathname contains any character
other than the ASCII letters (a-z and A-Z), digits (0-9), underscore (_),
ASCII dash (-), plus (+), dot (.), backslash (\) or slash (/). Typically
these characters don't work:

* spaces and tabs: This is easy to fix, just wrap the filename in double
  quotes ("), the usual way.
* double quotes ("): This can't happen, filenames on Windows are not allowed
  to contain double quotes. If you need to pass a non-filename argument with
  a double quote in it to pdfsizeopt, do this. Wrap the argument in double
  quotes ("), replace all double quotes (") with \", and (in parallel to the
  previous replacement) replace a sequence
  backslashes (\) and an double quote (") immediately following them by
  duplicating the backslashes and replacing the double quote (") with \".
  This sounds complicated, but this is the usual way for other programs as
  well, see https://stackoverflow.com/a/4094897/97248 .
* newlines and other non-space whitespace: This won't
  work, the Windows Command Prompt (cmd.exe) doesn't allow these characters in
  command-line arguments. Also Windows doesn't allow them in filenames.
* accented characters (such as á and ő). These characters won't work (or it
  may work for only some characters, depending on the active code page) in
  the PDF filename specified in the commandline, or in the full pathname of
  pdfsizeopt (so don't install pdfsizeopt to C:\bőr, it won't work).

  Accented characters (outside the active code page) will not work in the
  full pathname of pdfsizeopt (such as C:\bőr\pdfsizeopt.exe). That's
  because Python is unable to call external programs (os.system, os.popen,
  os.spawnl and subprocess.call) with accented characters in their name,
  because it uses the single-byte API.

* anything which is not ASCII printable (code between 33 and 126,
  inclusive): If not covered above, this may not work. See the description
  of accented characters.

If some filenames still don't work, the workarounds are:

* renaming or copying the file (and folders) in Windows Explorer, and passing
  the renamed file to pdfsizeopt
* using pdfsizeopt on a Unix system (e.g. Linux, FreeBSD, macOS) instead

Accented characters in PDF filename could be made work the following way (as
a future improvement work to pdfsizeopt):

* pdfsizeopt.exe should call the 16-bit API (GetCommandLineW) instead of
  the single-byte API (GetCommandLineA) to get the arguments
* pdfsizeopt.exe should escape the non-ASCII characters in the arguments
  (e.g. as U+12AB)
* pdfsizeopt.exe should run pdfsizeopt.single like this:

    .../pdfsizeopt_win32exec/pdfsizeopt_python.exe .../pdfsizeopt.single --args-u+ ...

* pdfsizeopt Python code should recognize --args-u+, and when finding the
  filename, it should convert it to unicode (by keeping ASCII except for
  U+12AB), and it should pass tha unicode-typed value to open(...). Such an
  open(...) works in Python 2.6 on Windows.
* When displaying filenames, pdfsizeopt Python code should still display the
  ASCII with the U+12AB escaping. Thus the win32console module is not
  needed. Thus filenames will be displayed leglibly but incorrectly (not
  copy-pasteably) in the Command Prompt window.

* No escaping is needed in command lines of helper programs (e.g. gs,
  sam2p), because it's all ASCII, because filenames are autogenerated
  temporary fil names, which are all ASCII, and path to pdfsizeopt itself
  is required to the ASCII.

Accented characters in the pathname of pdfsizeopt.single can be made work
this way (as a future improvement work to pdfsizeopt):

* Do the accented characters in the filename above first.
* pdfsizeopt.exe should use wgetcwd to get the current directory.
* pdfsizeopt.exe should use wchdir to change to the directory of
  pdfsizeopt.single .
* pdfsizeopt.exe should prepend the directories pdfsizeopt_win32exec and
  pdfsizeopt_win32exec/pdfsizeopt_gswin to the PATH, using wputenv.
* pdfsizeopt.exe should run pdfsizeopt.single like this:

  ```
    pdfsizeopt_python.exe pdfsizeopt.single --args-u+ --cwd=... ...
  ```

  , where the value of --cwd= is the escaped (U+12AB) version of the
  result of wgetcwd.

* pdfsizeopt Python code should prepend the value of --cwd=... to the input
  filename if it's relative.
* pdfsizeopt Python code shouldn't modify the PATH if --cwd=... is present.
  (Does this environment variable propagation work in Python 2.6.? Let's try!)
* It's still true that
  no escaping is needed in command lines of external programs (e.g. gs,
  sam2p), because it's all ASCII, because temporary file names are all ASCII,
  and path to pdfsizeopt itself is required to the ASCII. Escaping is needed
  if the pathname of the temporary directory (TEMP variable) needs escaping.

### 7. Error on Windows: The application failed to initialize properly (0xc0000034). Click on OK to terminate the application.

This error has happened on a Windows XP system. The solution: download
msvcr90.dll (or find it somewhere already on your system), and copy it into
pdfsizeopt_win32exec (next to python26.dll). Any version of msvcr90.dll will
work:

* msvcr90.dll 9.0.21022.8 (655872 bytes)
* msvcr90.dll 9.0.30729.6161 (653136 bytes)
* msvcr90.dll 9.0.30729.9247 (653968 bytes)

### 8. Error on Windows: The system cannot execute the specified command.

This error has happened on a Windows XP system when the file
Microsoft.VC90.CRT.manifest was missing from the pdfsizeopt_win32exec
directory. The solution: reinstall pdfsieopt, the directory
pdfsizeopt_win32exec in the newest version has that file.

### 9. Ghostscript errors with Type1CParser and Type1CConverter

Please install pdfsizeopt by following the installation instructions on
https://github.com/pts/pdfsizeopt . By doing so, pdfsizeopt will use
Ghostscript 9.05 bundled with it, and it will work.

## More documentation

* https://github.com/pts/pdfsizeopt/releases/download/docs-v1/pts_pdfsizeopt2009.psom.pdf
  White paper on EuroTex 2009.
* https://github.com/pts/pdfsizeopt/releases/download/docs-v1/pts_pdfsizeopt2009_talk.psom.pdf
  Conference talk slides on EuroTex 2009.

<!-- __END__ -->
