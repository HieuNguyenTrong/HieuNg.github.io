** AIRSIM **

# Go to the folder where you clone GitHub projects

$ git clone -b 4.18 https://github.com/EpicGames/UnrealEngine.git
$ cd UnrealEngine
$ ./Setup.sh
$./GenerateProjectFiles.sh

# When installing Unreal Engine 4.18.3 if there is an error as follows:

**ERROR**

``
	ERROR: Could not determine version of the compiler, not registering Linux toolchain.
``

**To solve that problem**

- Install clang, llvm 5.0

$ sudo add-apt-repsitory "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-5.0 main"
$ wget -O - http://apt.llvm.org/llvm-snapshot.gpg.key|sudo apt-key add -
$ sudo apt update

$ sudo apt install python-lldb-5.0
$ sudo apt install clang-5.0 clang-5.0-doc libclang-common-5.0-dev
libclang-5.0-dev libclang1-5.0 libclang1-5.0-dbg libllvm-5.0-ocaml-dev 
libllvm5.0 libllvm5.0-dbg lldb-5.0 llvm-5.0 llvm-5.0-dev llvm-5.0-doc 
llvm-5.0-examples llvm-5.0-runtime clang-format-5.0 python-clang-5.0 libfuzzer-5.0-dev

$ sudo ln -sf /usr/bin/llvm-symbolizer-5.0 /usr/bin/llvm-symbolizer
$ sudo update-alternatives --install /usr/bin/cc cc /usr/bin/clang-5.0 60
$ sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 50
$ sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++-5.0 60
$  sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 50
$  sudo apt install build-essential cmake valgrind kcachegrind vim cccc

*OPTIONAL: Code::Blocks IDE*
$ sudo apt install codeblocks codeblocks-contrib

- After finishing the above commands, try to install again this command:

$./GenerateProjectFiles.sh

- If there is no error, continue to type:

$ make 

- After all steps, enjoy Unreal Engine!
