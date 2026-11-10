# plasma6-debian-polkit-automount-internal-drive-no-passwd

```sh
sudo vi /etc/polkit-1/rules.d/10-udisks2-no-password.rules
```
```qml
// Allow udisks2 to mount devices without authentication
// for users in the "sudo" group (debian doesnt have 'wheel').
// https://forum.endeavouros.com/t/password-authentication-when-mounting-drives-in-thunar/17812/5
polkit.addRule(function(action, subject) {
    if ((action.id == "org.freedesktop.udisks2.filesystem-mount-system" ||
         action.id == "org.freedesktop.udisks2.filesystem-mount") &&
        subject.isInGroup("sudo")) {
        return polkit.Result.YES;
    }
});
```
```sh
sudo systemctl restart polkit
```
```sh
sudo reboot
```
