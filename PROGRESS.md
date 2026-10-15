# Progress

## Completed milestones

_None yet._

## Current milestone

**Milestone 1 — Setup and first ROS demonstration**

- [x] A. Verify the system (2026-10-14)
  - Ubuntu 24.04.5 LTS, arm64, QEMU/UTM VM, kernel 6.8.0-147-generic
  - 4 CPU cores, 7.7 GiB RAM (~5.1 GiB available at idle with VS Code open), 4 GiB swap
  - 62 GB disk, 48 GB free
  - Internet and DNS working (packages.ros.org reachable, ~220 ms latency)
  - apt healthy, no errors; 18 packages upgradable
  - VS Code 1.141.1, native arm64 build, installed via Microsoft apt repo
  - Installed: git 2.43.0, python3 3.12.3, curl 8.5.0, wget 1.21.4
  - Missing: python3-pip, python3-venv, build-essential
- [ ] B. Configure development tools
  - [x] Installed python3-pip, python3-venv, build-essential (2026-10-14; NetworkManager restart deferred until next reboot, harmless)
  - [x] ~/.bashrc sources /opt/ros/jazzy/setup.bash (2026-10-15)
  - [x] Git identity: Abu Bakar / GitHub noreply email; init.defaultBranch=main
  - [x] GitHub SSH auth: ed25519 key added, `ssh -T git@github.com` succeeds (host fingerprint verified)
  - [x] Created empty public repo abn-13/turtlebot3-port-patrol (local folder is named turtlebot-3-port-patrol; harmless, README should use repo name)
  - [x] .gitignore created (colcon outputs, Python cache, venvs, editor files; CLAUDE.md kept private)
  - [x] git init, remote origin = git@github.com:abn-13/turtlebot3-port-patrol.git
  - [-] VS Code extensions: skipped (fast-track)
  - [x] colcon, rosdep, vcstool (installed in step C5)
- [x] C. Install ROS 2 Jazzy and run talker/listener (completed 2026-10-14)
  - Order changed (agreed 2026-10-14): C before the rest of B, since ROS tools need the ROS apt repo and Git/VS Code setup fits better once there is code.
  - Official guide read from github.com/ros2/ros2_documentation (jazzy branch); docs.ros.org blocks automated fetches.
  - [x] Locale already en_US.UTF-8; universe, noble-updates, noble-backports already enabled
  - [x] C1: downloaded ros2-apt-source 1.3.0 (inspected: only key + sources file, no install scripts)
  - [x] C2: installed ros2-apt-source 1.3.0~noble; apt update reaches packages.ros.org (arm64) with valid signature
  - [x] C3: sudo apt upgrade (18 packages incl. systemd). Reboot needed for deferred service restarts (lightdm, logind, dbus, NetworkManager)
  - [x] Rebooted (2026-10-14 08:55). Only 3 phased updates pending (apparmor, libapparmor1, open-vm-tools), held back by Ubuntu on purpose, harmless
  - [x] C4: ros-jazzy-desktop 0.11.0 installed (294 ros-jazzy-* pkgs, /opt/ros/jazzy 268 MB, dpkg --audit clean)
  - [x] C5: ros-dev-tools 1.0.3 installed (colcon, rosdep 0.27.0, vcstool 0.3.0). Harmless Python SyntaxWarning from python3-vcstools during install. `sudo rosdep init` + `rosdep update` still to do before Milestone 2 builds
  - [x] C6: user sourced setup.bash; ROS_DISTRO=jazzy, ros2 --help works (and fails before sourcing, as expected)
  - [x] C7: user ran talker (C++) + listener (Python); stop/restart experiments; ros2 node list / topic list / topic info / topic echo; remapping topic (chatter:=port_alerts) and node name (__node:=gate_sensor)
  - [x] Node/topic understanding check passed: user explained in own words that subscribers wait without a publisher and publishers don't depend on subscribers; correctly explained why echo made subscription count 2
  - Debugged by user: remap error from `__node:gate_sensor` (missing `=`); read the rcl parse error to find it
- [ ] D. Gazebo check: merged into fast-track step 1 (launch TurtleBot3 world)
- [x] Set up GitHub repository
- [ ] First commit (fast-track step 0)

## Remaining tasks

Fast-track mode adopted 2026-10-15 (see CLAUDE.md "Fast-track mode"). Patrol node: user writes it with hints.
ARM64 availability checked 2026-10-15: turtlebot3 2.3.6, turtlebot3-gazebo 2.3.7, ros-gz 1.0.24, slam-toolbox 2.8.5, navigation2/nav2-bringup/nav2-simple-commander 1.3.13 all available.

- [ ] 0. First commit
- [ ] 1. Install TurtleBot3 sim + Gazebo + SLAM + Nav2; launch robot world (Gazebo-in-UTM check)
- [ ] 2. SLAM map, saved
- [ ] 3. Nav2 goal via RViz
- [ ] 4. Patrol node (user writes)
- [ ] 5. Two tests, README, GIF
- [ ] 6. OPTIONAL: simple container-yard world (boxes), re-run SLAM, new waypoints, re-record demo

## Known issues

- RAM may be tight later with Gazebo + Nav2 + RViz + VS Code running together. Watch swap usage.
- Download speed is slow (~190 kB/s on apt update, ~220 ms latency to packages.ros.org).
- UTM GPU acceleration is unverified; Gazebo rendering must be tested early (step D).

## Next action

Fast-track step 0: user makes first commit and pushes. Then step 1 install.
