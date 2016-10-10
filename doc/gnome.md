# Keep primary display workspace steady when selecting windows on secondary display without workspaces
    gsettings set org.gnome.mutter workspaces-only-on-primary true

    
# Dolphin missing icons workaround

edit file */usr/share/applications/org.kde.dolphin.desktop*

replace 

    Exec=dolphin %u
    
by  

    Exec=env XDG_CURRENT_DESKTOP=gnome dolphin %u
    
# Toggle cairo dock shortcut command:
    
    dbus-send --session --dest=org.cairodock.CairoDock /org/cairodock/CairoDock org.cairodock.CairoDock.ShowDock int32:2 
  
Add this command as the desktop shortcut. 