# Debian / Ubuntu User Management


| **User Management**     |                                                                      |
| `useradd -m name`       | Add user with the name `name`. `-m` creates a home directory `name`. |
| `passwd name`           | Set the password for user `name`.                                    |
| `userdel name`          | Remove user with the name `name`.                                    |
| `usermod -aG sudo name`| Make `name` a sudoer. |


**User not in sudoers file**

If you are part of the `sudo` group but are getting the error that you are not a sudoer or in the sudoers file, run:

```sh
sudo visudo
```

Then save the file. Your `/etc/sudoers` file should now have the `sudo` group allowed to `sudo`:

```
# Allow members of group sudo to execute any command
%sudo ALL=(ALL:ALL) ALL
```

Remember never to edit the `sudoers` file directly.
