# File: Dockerfile
# Base: ROS 2 Humble + Ubuntu desktop + noVNC (HTML5 VNC) 
# Docs for this base (port 6080, seccomp note): https://github.com/Tiryoh/docker-ros2-desktop-vnc
FROM ghcr.io/tiryoh/ros2-desktop-vnc:humble

USER root
ENV DEBIAN_FRONTEND=noninteractive

# Core tooling
RUN apt-get update && apt-get install -y \
    lsb-release wget curl gnupg git nano \
    python3-colcon-common-extensions \
    xclip parcellite \
    && rm -rf /var/lib/apt/lists/*

# Add Gazebo (OSRF) apt repo & key, then install Gazebo Fortress + ROS <-> Gazebo bridge + teleop
# Fortress is the recommended pairing with ROS 2 Humble. :contentReference[oaicite:1]{index=1}
RUN set -eux; \
    apt-get update && apt-get install -y lsb-release wget gnupg; \
    wget -O /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg https://packages.osrfoundation.org/gazebo.gpg; \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" \
      > /etc/apt/sources.list.d/gazebo-stable.list; \
    apt-get update; \
    apt-get install -y ros-humble-ros-gz \
                       ros-humble-teleop-twist-keyboard; \
    # Classic Gazebo ROS wrappers are amd64-only on Jammy; install them only on Intel. :contentReference[oaicite:2]{index=2}
    if [ "$(dpkg --print-architecture)" = "amd64" ]; then \
        apt-get install -y ros-humble-gazebo-ros-pkgs; \
    fi; \
    rm -rf /var/lib/apt/lists/*

# Make a default workspace and source ROS for all shells
RUN mkdir -p /workspaces/ros2_ws/src \
 && echo "source /opt/ros/humble/setup.bash" >> /etc/bash.bashrc

# Autostart a tiny clipboard manager inside the desktop (helps with selections in VNC)
RUN printf "[Desktop Entry]\nType=Application\nName=Parcellite\nExec=parcellite\nX-GNOME-Autostart-enabled=true\n" \
    > /etc/xdg/autostart/parcellite.desktop

# Helpful defaults for graphics over VNC
ENV LIBGL_ALWAYS_SOFTWARE=1 \
    QT_X11_NO_MITSHM=1 \
    RESOLUTION=1920x1080

WORKDIR /workspaces/ros2_ws
