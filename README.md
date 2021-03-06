# swiggityspeare
[![forthebadge](http://forthebadge.com/images/badges/powered-by-case-western-reserve.svg)](http://forthebadge.com)

Character-based recurrent neural networks wrapped into an IRC chatbot.
Initially designed to be colloquial English with a touch of Shakespeare, the
network can't be open-sourced for privacy reasons: training data came from IRC
users who didn't consent to open-sourcing.

### tl;dr environment setup

Swiggityspeare now comes with an easy setup script to get started! You'll still
need to install CUDA manually, but here's the process:

- install the [CUDA Toolkit][cuda]
- `git clone https://github.com/raidancampbell/swiggityspeare.git --recursive`
- `cd swiggityspeare`
- `./setup.sh`
- `java -jar swiggityspeare.jar -c "#swag #cwru" -n babbyspeare`

`setup.sh` will ask to install [Torch][torch], init+update the git submodule for
[Andrej Karpathy's char-rnn][karpathy_char-rnn], move the neural network into
place, and install the required packages with `luarocks`.

[torch]: http://torch.ch/
[cuda]: https://developer.nvidia.com/cuda-downloads
[karpathy_char-rnn]: https://github.com/karpathy/char-rnn

### dependencies

Swiggity's Java dependencies are all taken care of at compile time with the .jar
files in the `dependencies` directory.

Other than CUDA, all of swiggity's system dependencies are best installed using
`setup.sh`, as explained above. Otherwise, manually install Torch, `git
submodule init` and `git submodule update`, and use `luarocks` (provided with
Toch) to install `cunn` `cutorch` `nngraph` `optim`.

Test the environment with a quick `th train.lua`, whose default settings should
begin training from a Shakespeare dataset included in the char-rnn repository.

It's build-your-own neural network. A sample network is in
dependencies/irc_network.t7: it's a quick Shakespeare-trained network. __This
needs to be moved into the newly cloned `char-rnn` directory to work.__
`setup.sh` manages the initial copying for you.

At this point usage is pretty simple. The project is based on IntelliJ, so just
`build`->`build artifacts`->`swiggityspeare.jar`, or use the prebuilt
`swiggityspeare.jar` provided.

### usage

Execution is a simple `java -jar swiggityspeare.jar`. However, the jar expects
the `dependencies` directory to be alongside it (or the `-d` switch to be set),
so that it knows where the `char-rnn` code is, and can execute it. The
prepackaged .t7 neural network needs to be moved into the cloned `char-rnn`
directory.

When in doubt, `java -jar swiggityspeare.jar --IHaveNoIdeaWhatImDoing` (or any
invalid switch, like --help) will print the usage text. For the lazy: usage:

    swiggityspeare
    -c <arg>   channels to join, including quotes, in the format "#chan1 #chan2" [#cwru]
    -d <arg>   relative path of the char-rnn directory ["dependencies/char-rnn"]
    -n <arg>   nick for the bot to take [swiggityspeare]
    -p <arg>   IRC server port number (SSL is assumed) [6697]
    -s <arg>   IRC server hostname [irc.case.edu]
    -t <arg>   filename of the .t7 holding the neural network within
               char-rnn's root directory [irc_network.t7]

### Contributions
Git-workflow-style fork-commit-pullreqest. You kids are all better at git than
I am, so I'm learning from you here.

### License
MIT
