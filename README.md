
About Us ZlotyCoin[zl]
==========================

Zlotycoin is a PoS-based cryptocurrency.

We are introducing New Crypto coin, which based in Poland.Yes you read right, we are from POLAND. Our currency name is Zloty, so we developed a crypto currency to participate with rest of world and share our Polish community with the rest of world.Złoty which literally means "golden".Total Zloty supply will be: 40000000zl. Premine is 5%, Total Premine amount 2210526 zl coins. 1700000zl will be on ICO from this premine.Amount from ICO sell will go to Zloty Foundation to develop it on next level. Rest of 5210526zl will be for BOUNTY, Giveaway, External Developer.

Specification
===========================
Algo:Scrypt(PoW/PoS)
Coin Name: Zlotycoin
Symbol: zł
Ticker: ZLC
Initial Letter: Z
Block reward:100 coins
Total coin supply:40000000
Last PoW block:420000
Transaction confirmations:6 blocks
Maturity:20 blocks
Spacing:64 seconds
Timespan:1 block
PREMINE INFO:
Premine %:5%
Premine Total Amount:2210526 coins
POS INTEREST INFO
PoS %:5% per year
RPC port:8316
P2P port:8315

Development process
===========================

Developers work in their own trees, then submit pull requests when
they think their feature or bug fix is ready.

The patch will be accepted if there is broad consensus that it is a
good thing.  Developers should expect to rework and resubmit patches
if they don't match the project's coding conventions (see coding.txt)
or are controversial.

The master branch is regularly built and tested, but is not guaranteed
to be completely stable. Tags are regularly created to indicate new
stable release versions of Zlotycoin.

Feature branches are created when there are major new features being
worked on by several people.

From time to time a pull request will become outdated. If this occurs, and
the pull is no longer automatically mergeable; a comment on the pull will
be used to issue a warning of closure. The pull will be closed 15 days
after the warning if action is not taken by the author. Pull requests closed
in this manner will have their corresponding issue labeled 'stagnant'.

Issues with no commits will be given a similar warning, and closed after
15 days from their last activity. Issues closed in this manner will be 
labeled 'stale'.

Build IN Linux:
==========================
UNIX BUILD NOTES
================

To Build
--------

cd src/
make -f makefile.unix            # Headless zlotycoin

See readme-qt.rst for instructions on building Zlotycoin QT,
the graphical zlotycoin.

Dependencies
------------

 Library     Purpose           Description
 -------     -------           -----------
 libssl      SSL Support       Secure communications
 libdb       Berkeley DB       Blockchain & wallet storage
 libboost    Boost             C++ Library
 miniupnpc   UPnP Support      Optional firewall-jumping support
 libqrencode QRCode generation Optional QRCode generation

Note that libexecinfo should be installed, if you building under *BSD systems. 
This library provides backtrace facility.

miniupnpc may be used for UPnP port mapping.  It can be downloaded from
http://miniupnp.tuxfamily.org/files/.  UPnP support is compiled in and
turned off by default.  Set USE_UPNP to a different value to control this:
 USE_UPNP=-    No UPnP support - miniupnp not required
 USE_UPNP=0    (the default) UPnP support turned off by default at runtime
 USE_UPNP=1    UPnP support turned on by default at runtime

libqrencode may be used for QRCode image generation. It can be downloaded
from http://fukuchi.org/works/qrencode/index.html.en, or installed via
your package manager. Set USE_QRCODE to control this:
 USE_QRCODE=0   (the default) No QRCode support - libqrcode not required
 USE_QRCODE=1   QRCode support enabled

Licenses of statically linked libraries:
 Berkeley DB   New BSD license with additional requirement that linked
               software must be free open source
 Boost         MIT-like license
 miniupnpc     New (3-clause) BSD license

Versions used in this release:
 GCC           4.9.0
 OpenSSL       1.0.1g
 Berkeley DB   5.3.28.NC
 Boost         1.55.0
 miniupnpc     1.9.20140401

Dependency Build Instructions: Ubuntu & Debian
----------------------------------------------
sudo apt-get install build-essential
sudo apt-get install libssl-dev
sudo apt-get install libdb++-dev
sudo apt-get install libboost-all-dev
sudo apt-get install libqrencode-dev

If using Boost 1.37, append -mt to the boost libraries in the makefile.


Dependency Build Instructions: Gentoo
-------------------------------------

emerge -av1 --noreplace boost openssl sys-libs/db

Take the following steps to build (no UPnP support):
 cd ${ZLOTYCOIN_DIR}/src
 make -f makefile.unix USE_UPNP=
 strip zlotycoind


Notes
-----
The release is built with GCC and then "strip zlotycoind" to strip the debug
symbols, which reduces the executable size by about 90%.


miniupnpc
---------
tar -xzvf miniupnpc-1.6.tar.gz
cd miniupnpc-1.6
make
sudo su
make install


Berkeley DB
-----------
You need Berkeley DB. If you have to build Berkeley DB yourself:
../dist/configure --enable-cxx
make


Boost
-----
If you need to build Boost yourself:
sudo su
./bootstrap.sh
./bjam install


Security
--------
To help make your zlotycoin installation more secure by making certain attacks impossible to
exploit even if a vulnerability is found, you can take the following measures:

* Position Independent Executable
    Build position independent code to take advantage of Address Space Layout Randomization
    offered by some kernels. An attacker who is able to cause execution of code at an arbitrary
    memory location is thwarted if he doesn't know where anything useful is located.
    The stack and heap are randomly located by default but this allows the code section to be
    randomly located as well.

    On an Amd64 processor where a library was not compiled with -fPIC, this will cause an error
    such as: "relocation R_X86_64_32 against `......' can not be used when making a shared object;"

    To build with PIE, use:
    make -f makefile.unix ... -e PIE=1

    To test that you have built PIE executable, install scanelf, part of paxutils, and use:
    scanelf -e ./zlotycoin

    The output should contain:
     TYPE
    ET_DYN

* Non-executable Stack
    If the stack is executable then trivial stack based buffer overflow exploits are possible if
    vulnerable buffers are found. By default, zlotycoin should be built with a non-executable stack
    but if one of the libraries it uses asks for an executable stack or someone makes a mistake
    and uses a compiler extension which requires an executable stack, it will silently build an
    executable without the non-executable stack protection.

    To verify that the stack is non-executable after compiling use:
    scanelf -e ./zlotycoin

    the output should contain:
    STK/REL/PTL
    RW- R-- RW-

The STK RW- means that the stack is readable and writeable but not executable.
