arch-luks-suspend
==================

A script for [Arch Linux][] to lock the encrypted root volume on suspend.

When using [dm-crypt with LUKS][] to set up full system encryption, the
encryption key is kept in memory when suspending the system. This drawback
defeats the purpose of encryption if you carry around your suspended laptop
a lot. One can use the `cryptsetup luksSuspend` command to freeze all I/O and
flush the key from memory, but special care must be taken when applying it to
the root device.

The `arch-linux-suspend` script replaces the default suspend mechanism of
systemd. It changes root to initramfs in order to perform the `luksSuspend`,
actual suspend, and `luksResume` operations. It relies on the `shutdown`
initcpio hook to provide access to the initramfs.

[Arch Linux]: https://www.archlinux.org/
[dm-crypt with LUKS]: https://wiki.archlinux.org/index.php/Dm-crypt_with_LUKS


Installation
-------------

1. Install this AUR package: https://aur.archlinux.org/packages/arch-luks-suspend-git/  
   Alternatively, run `make install` as root.
2. Edit `/etc/mkinitcpio.conf` and make sure the following hooks are enabled:
   `encrypt`, `shutdown`, `suspend`.
3. Rebuild the initramfs: `mkinitcpio -p linux`.
4. Reboot.


Author and license
-------------------

Copyright 2013 Vianney le Clément de Saint-Marcq <vleclement@gmail.com>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; version 3 of the License.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with This program.  If not, see <http://www.gnu.org/licenses/>.
