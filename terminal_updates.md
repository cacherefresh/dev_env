# Terminal Updates, adding git Aliases etc. 
Reduce , Reuse, Recycle, and REDUCE BITROT!
the tiny little 1 minute things that you use every day a million times adds up. 
same as holding shift and right clicking to open a terminal at a designated folder rather than CHANGE DIRECTORYing every time.... so here are some helpers. 

## zsh and oh-my-zsh
use it. there is enough documentation out there. but add the current working directory and git branch to show up in your terminal. it will save you headache. 

## adding git alias git prune-gone
this will git fetch --prune, and then delete all the branches locally that are gone upstream that have been merged already as you branches will grow. 

``
git config --global alias.prune-gone '!git fetch --prune && git branch -vv | grep ": gone]" | awk "{print \$1}" | xargs -r git branch -d'
``

##Some Commands to ease navigation: 

### adding up arrow filter
brief description: 
  this will make it so when you type a few letters you can hit the up arrow ( ↑ ) 
  it filters only the previous commands that start with whatever you typed.
#### do this in your terminal
(you'll type the first line and hit enter, it will let you type stuff until you type the letters EOF...)

``
> $ cat >> ~/.inputrc << EOF
> 
> \> "\e[A": history-search-backward
> 
> \> "\e[B": history-search-forward
> EOF
``

#### example
if you ran the commands 
> cd ~#
> 
> fgrep	## Search file(s) for lines that match a fixed string
>
> ls -la
> 
> flutter run ./lib/main.dart
>
> ls -la 
>

then in your terminal hit "f" and then ↑
instead of the usual previous command (ls-la) 
it will instead show you flutter run .lib/main.dart
and if you hit UP again, it wil jump up to fgrep.....

^_~ your welcome... saves you time

how much does god love me? bash and input already have my initals added to the end ... rc .... it's good to enjoy life when you are coding all day trying to bring peace on earth. remember to touch grass ..when it's damp especially with your bare feet. it grounds you and removes negative energy quite literally. Navy seals would do this, or people that were almost overdosing. it can save a life. I do it weekly.   
