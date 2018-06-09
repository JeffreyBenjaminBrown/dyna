To build [the Dockerfile](Dockerfile) I did this (from `dyna/docker/`):
```
sudo docker build -f Dockerfile -t	                        \
  jeffreybbrown/dyna:new .
```

Then to run the docker image, I did this:
```
sudo docker run --name dyna -it -v /home/jeff/code/dyna:/mnt    \
  -p 9090:8888 -d -h 127.0.0.1                                  \
  jeffreybbrown/dyna:new
```

To run that yourself you'll need to change /home/jeff/code/dyna to the name of the folder in which your clone of Dyna resides.

Once that's running, I did this to get into a shell in the container:
```
sudo docker exec -it dyna bash
```

In the shell I ran `alias python=python2` to change the default python from 3 to 2.

Then I ran `cd /mnt` to go to where the Dyna code is located.

Then I ran `make`. The result was lots of stuff printing to the screen, ending with this:
```
Preprocessing executable 'dyna' for dyna-0.4...
[25 of 37] Compiling Dyna.XXX.Automata.NamedAut ( src/Dyna/XXX/Automata/NamedAut.hs, dist/build/dyna/dyna-tmp/Dyna/XXX/Automata/NamedAut.o )

src/Dyna/XXX/Automata/NamedAut.hs:24:1: error:
    Failed to load interface for ‘Control.Monad.Trans.Either’
    Perhaps you meant
      Control.Monad.Trans.Iter (needs flag -package-key free-5.0.2)
      Control.Monad.Trans.Writer (from transformers-0.5.2.0)
      Control.Monad.Trans.Error (from transformers-0.5.2.0)
    Use -v to see a list of the files searched for.
Makefile:30: recipe for target 'build' failed
make: *** [build] Error 1
```
