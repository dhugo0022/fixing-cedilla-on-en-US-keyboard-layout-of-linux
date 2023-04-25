# fixing-cedilla-on-en-US-keyboard-layout-of-linux
An easy and fast fix to get cedilla working properly on en-US((intl, with dead keys) with ' + c

This repo serves merely as a reminder for me on how to get the cedilla working properly in linux.

Tested only on Linux Mint 21.1 Cinnamon (Ubuntu 22.04), but the original tutorial was using versions
as old as 11.04.

**Reference: https://askubuntu.com/questions/39837/how-do-i-make-cedilla-%c3%a7-character-available-in-english-usa/39863#39863**

## The fix

### First step:

**For 64-bit systems:**

```
sudo nano /usr/lib/x86_64-linux-gnu/gtk-3.0/3.0.0/immodules.cache
sudo nano /usr/lib/x86_64-linux-gnu/gtk-2.0/2.10.0/immodules.cache
```

**For 32-bit systems:**

```
sudo nano /usr/lib/i386-linux-gnu/gtk-2.0/2.10.0/immodules.cache
```

**Before changing the line, be careful, your version of gtk can be different depending on
your version of ubuntu, like mine was(gtk30). And you don´t wanna change that, the following 
lines are only examples...**

Change the line:

```
"cedilla" "Cedilla" "gtk20" "/usr/share/locale" "az:ca:co:fr:gv:oc:pt:sq:tr:wa
```

to (you will only add ":en" at the end):

```
"cedilla" "Cedilla" "gtk20" "/usr/share/locale" "az:ca:co:fr:gv:oc:pt:sq:tr:wa:en"
```

### Second step:

Replace "ć" with "ç" and "Ć" with "Ç" in /usr/share/X11/locale/en_US.UTF-8/Compose

```
sudo cp /usr/share/X11/locale/en_US.UTF-8/Compose /usr/share/X11/locale/en_US.UTF-8/Compose.bak
sed 's/ć/ç/g' < /usr/share/X11/locale/en_US.UTF-8/Compose | sed 's/Ć/Ç/g' > Compose
sudo mv Compose /usr/share/X11/locale/en_US.UTF-8/Compose
```

### Third step:

Add two lines in /etc/environment

```
GTK_IM_MODULE=cedilla
QT_IM_MODULE=cedilla
```

### Final step:

**Restart your computer.**
