# Ansible Role: System Config

This role can be used to make some system configurations (placing system
configuration files into /etc/. It might be pretty specific for my personal
computer/laptop setup, but maybe someone else has a use for it as well, or
takes it as a starting point to configure their own system.


## Requirements

I use the monitor hotplug setup in order to configure my system in such a way
that attaching/detaching HDMI monitors is automatically detected and my screen
setup is automatically adjusted. This includes a systemd service, a udev rule,
and some additional scripts. I wrote a more detailed explanation about my
monitor hotplug setup that can be found
[here](https://schuam.de/en/posts/82276148b1.html).

If you want to use my setup. You will have to do the following:

- Adjust the path to the monitor_connection_change.sh script in
  files/etc/systemd/system/monitor-hotplug.service.
- Get the following scrtips from my
  [dotfiles](https://github.com/schuam/.dotfiles/):
  - .config/startup/monitor_connection_change.sh
  - .config/startup/startup_screen_setup.sh
- Adjust some lines in these two scripts that contain paths.
- Write **xrandr** scripts to actually adjust your screen setup. These scripts
  are called from within startup_screen_setup.sh. You can also generate these
  scripts with the program **arandr**.

Sorry, that this might be a little complicated, but I set this up a while back
for myself and haven't found the time to think about how to make it more
convenient for others.

Other than that the rest of the system config role should work out of the box.


## Role Variables

The following variables can be found in vars/main.yml:

- monitor_hotplug_dirs: List of directories under /etc/ that are needed.
- monitor_hotplug_files: List of files for my monitor hotplug configuration.
- x11_dirs: List of X11 directories that are needed under /etc/.
- x11_files: List of files for my X11 configuration.
- ruby_gem_files: List of files for ruby gem configuration.
- locale_files: List of files for the locale configuration.
- vconsole_files: List of files for the vconsole configuration.


The following variables can be found in defaults/main.yml. The first ones
starting with "configure" can be set to true or false, depending on if you want
to configure the respective part. The second to last one is the preferred
vconsole keymap. The last one indicates the kind of graphics card that is
installed.

- configure_monitor_hotplug
- configure_x11
- configure_ruby_gem
- configure_locale
- configure_vconsole
- configure_sshd
- vconsole_keymap
- x11_graphics_card


## Dependencies

None


## Example Playbook

    - hosts: localhost
      roles:
         - { role: schuam.system_config }

## License

MIT


## Author Information

This role was created in 2022 by [Andreas Schuster](https://www.schuam.de/).

