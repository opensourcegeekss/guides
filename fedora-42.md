# Fedora 42 Setup Guide -

## DNF -

Increase DNF download speed.

```bash
echo 'max_parallel_downloads=10' | sudo tee -a /etc/dnf/dnf.conf
echo 'deltarpm=true' | sudo tee -a /etc/dnf/dnf.conf
```

Open terminal and type following commands and reboot after installing updates.

```bash
# Update system and reboot
sudo dnf -y clean all
sudo dnf -y update
sudo reboot
```

## Enable RPM Fusion repositories -

```bash
sudo dnf install -y https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm

sudo dnf install -y https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

## Enable flatpak support -

```bash
# Add flatpak remote
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Update flatpak metadata
flatpak update --appstream
```

## AppImage support -

```bash
sudo dnf install -y fuse
```

## Multimedia codecs -

```bash
sudo dnf -y swap 'ffmpeg-free' 'ffmpeg' --allowerasing
```

## OpenH264 for Firefox -

```bash
sudo dnf install -y openh264 gstreamer1-plugin-openh264 mozilla-openh264
sudo dnf config-manager setopt fedora-cisco-openh264.enabled=1
```

## AMD & Intel GPU Drivers -

```bash
# Basic drivers and Vulkan support
sudo dnf install -y mesa-dri-drivers mesa-vulkan-drivers vulkan-loader mesa-libGLU
```

### AMD -

```bash
# AMD video acceleration (makes videos smoother)
sudo dnf install -y mesa-va-drivers-freeworld mesa-vdpau-drivers-freeworld
```

### Newer Intel GPUs -

```bash
# Intel video acceleration (for newer Intel GPUs)
sudo dnf install -y intel-media-driver
```

### Older Intel GPUs -

```bash
# Intel video acceleration (for Grandfather Intel GPUs)
sudo dnf install -y libva-intel-driver
```

## Hardware Acceleration -

```bash
# Install VA-API stuff
sudo dnf install -y ffmpeg-libs libva libva-utils
```

## Firefox Video Fix -

Firefox needs a little help with H.264 videos.

```bash
# Install the Cisco codec
sudo dnf install -y openh264 gstreamer1-plugin-openh264 mozilla-openh264

# Enable the Cisco repo
sudo dnf config-manager setopt fedora-cisco-openh264.enabled=1
sudo dnf update -y
```

### Dual Boot Time Fix

If you dual boot with Windows, this fixes the clock being wrong.

```bash
# Tell Fedora to use UTC for hardware clock
sudo timedatectl set-local-rtc 0 --adjust-system-clock
```

## Set hostname -

Replace `hostname` with your one.

```bash
hostnamectl set-hostname YOUR_HOSTNAME

# Example -
hostnamectl set-hostname osg
```
## System Cleanup -

Do this occasionally to free up space.

```bash
# Clean package cache
sudo dnf clean all

# Remove orphaned packages
sudo dnf autoremove -y
```