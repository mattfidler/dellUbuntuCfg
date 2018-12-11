
# Installing Ubuntu on the Dell XPS 9570
Use the standard install, then add the following hacks

```sh
bash -c "$(curl -fsSL https://raw.githubusercontent.com/JackHack96/dell-xps-9570-ubuntu-respin/master/xps-tweaks.sh)"
```

See https://github.com/JackHack96/dell-xps-9570-ubuntu-respin

# Setting up git for github

Fist generate a ssh key
```sh
# In Ubuntu, the keychain will be saved if you are using gnome.
ssh-keygen -t rsa -b 4096 -C "514778+mattfidler@users.noreply.github.com"
# Add to ssh agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
sudo apt-get install xclip
xclip -sel clip < ~/.ssh/id_rsa.pub
```

Add it to github

https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

Generate a gpg key

https://help.github.com/articles/generating-a-new-gpg-key/


```sh
# From https://gist.github.com/mort3za/ad545d47dd2b54970c102fe39912f305
$ gpg --list-keys
/home/matt/.gnupg/pubring.kbx
-----------------------------
pub   rsa4096 2018-12-11 [SC]
      AE8C937A8B321566E59B442F50DBB34725AF75EF
uid           [ultimate] Matthew Fidler <514778+mattfidler@users.noreply.github.com>
sub   rsa4096 2018-12-11 [E]
And export key like this:

git config --global user.signingkey 50DBB34725AF75EF
git config --global user.name "Matthew Fidler"
git config --global user.email "514778+mattfidler@users.noreply.github.com"
```



# Installing nlmixr R

```sh
sudo apt-get install libopenblas-base r-base
## Now install Rstudio
sudo apt-get install gdebi
cd ~/Downloads
wget https://download1.rstudio.org/rstudio-xenial-1.1.419-amd64.deb
sudo gdebi rstudio-xenial-1.1.379-amd64.deb
```

The `gdebi` command changes based on what `deb` file is actually downloded.  For me this was different than what was downloaded.



Install the needed ubuntu packages

```sh
sudo apt-get install libudunits2-dev python-sympy gfortran libssl-dev libgit2-dev valgrind
```

```R
install.packages(c("tidyverse", "data.table",
                   "devtools", "Rcpp", "brew",
                   "lattice","lbfgs",
                   "inline","dparser","ggplot2",
                   "rex","minqa","Matrix",
                   "numDeriv","R.utils","mvtnorm","n1qn1",
                   "PreciseSums","fastGHQuad","crayon",
                   "cli", "RcppArmadillo","dplyr","ggforce",
                   "purrr","readr","rlang","stringr",
                   "tibble","tidyr","gridExtra","rmarkdown","knitr",
                   "testthat","plotly","webshot","mvtnorm",
                   "shiny",
                   "rmarkdown",
                   "tidyr",
                   "tibble",
                   "curl",
                   "ggplot2",
                   "gridExtra",
                   "microbenchmark",
                   "scales",
                   "stringi", "lbfgsb3c",
                   "lbfgsb3c", "madness", "expm", "matrixcalc", "bookdown", "roxygen2", "xpose",
                   "reticulate", # Works well in Linux.
                   "nloptr", "ucminf"))


devtools::install_github("nlmixrdevelopment/RxODE")
devtools::install_github("richardhooijmaijers/R3port")
devtools::install_github("nlmixrdevelopment/xpose.nlmixr")
devtools::install_github("nlmixrdevelopment/nlmixr")
```

# Rstudio and other non-retina aware apps

```
# http://jumptuck.com/2017/05/09/custom-resolutions-dell-xps-13-running-ubuntu-1604/

#!/bin/sh
xrandr --newmode "1792x1008_60.00" 149.50 1792 1904 2088 2384 1008 1011 1016 1046 -hsync +vsync
xrandr --addmode eDP-1 1792x1008_60.00
xrandr --newmode "1664x936_60.00" 128.50 1664 1768 1936 2208 936 939 944 972 -hsync +vsync
xrandr --addmode eDP-1 1664x936_60.00
```

# Grub (make it readable)

Follow this http://blog.wxm.be/2014/08/29/increase-font-in-grub-for-high-dpi.html, but use 48 size

```
sudo grub-mkfont --output=/boot/grub/fonts/DejaVuSansMono24.pf2 \
  --size=48 /usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf
```

# Ergoemacs things
See https://askubuntu.com/questions/24916/how-do-i-remap-certain-keys-or-devices

Mapping Alt to menu

```sh
#!bin/sh
# This is in ~/.bin/alt-mod-map.sh
# It is can be run in gnome's startup settings;  .xinitrc doens't seem to work:
# https://unix.stackexchange.com/questions/107434/remap-keys-on-gnome3-8-using-xmodmap
# Changing right alt to menu
xmodmap -e "keycode 108 = Menu"
```

