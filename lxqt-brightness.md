## setting brightness control by hotkeys on LXQt

### Create the script file

    touch ~/brightness

### Paste the following content into the <code>brightness</code> file

```shell
#!/usr/bin/env bash
# output device value: eDP-1
output_device=$( /usr/bin/xrandr | awk '{i++}i==2{print;exit}' | awk '{print $1}' ) 
# brightness is converted from decimal to integer bellow
brightness=$( /usr/bin/xrandr --verbose | grep -i brightness | awk '{print $2 * 10}' ) 
# check the args and apply the respective action
check_value() {
    if [ $1 == '-i' ]; then
        increase
    elif [ $1 == '-d' ]; then
        decrease
    else
        display_error
    fi

    reset_scale  ##converts brightness level back to decimal
    /usr/bin/xrandr --output $output_device --brightness $brightness --gamma 0.7:0.7:0.7
}

increase() {
    if (( $brightness < 10 )); then
        brightness=$( echo $brightness | awk '{print $1 + 1 }' )
    else
        echo 'Brightness level cannot be higher than 1'
    fi
}

decrease(){
    if (( $brightness > 3 )); then
        brightness=$( echo $brightness | awk '{print $1 - 1 }' )
    else
        echo 'Brightness level cannot be lower than 0.3'
    fi
}

reset_scale() {
    if [ $brightness -eq 10 ]; then
        brightness=1
    else
        brightness=$( echo '0.'$brightness )
    fi
}

display_error() {
    echo -e 'Error: Argumment expected \n -i to incremment\n -d to decrement \n'
}

if ! [ -z $1 ]; then
    check_value $1
else
    display_error
fi
```
### Set the script permissions

    chmod 755 brightness

### Create the new script location

    sudo mkdir /opt/bin

### Move the script to the following location

    sudo mv ~/brightness /opt/bin/

### Create a symbolic link in order to make it system visible

    sudo ln -s /opt/bin/brightness /usr/local/bin/brightness


[Return to installation steps](debian-install.md#hardware-clock-settings-for-dualboot)
