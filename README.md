# Kinesis Advantage 360 Pro - Personal Config

Personal fork for custom keymaps on the Kinesis Advantage 360 Pro.

## Workflow

### Repository Structure

```
V3.0                    ← Keep synced with upstream (don't edit)
  │
  └── my-keymap         ← Your customizations go here
```

### Initial Setup (One-time)

1. Add the upstream remote:
   ```bash
   git remote add upstream https://github.com/KinesisCorporation/Adv360-Pro-ZMK.git
   ```
2. Create your keymap branch:
   ```bash
   git checkout -b my-keymap
   ```

### Making Keymap Changes

1. Make sure you're on your keymap branch:
   ```bash
   git checkout my-keymap
   ```
2. Edit your config files:
   - `config/adv360.keymap` (key bindings)
   - `config/macros.dtsi` (custom macros)
3. Commit and push your changes:
   ```bash
   git add -A && git commit -m "updated keymap"
   git push origin my-keymap
   ```

### Syncing with Upstream

1. Fetch and update the V3.0 branch:
   ```bash
   git fetch upstream
   git checkout V3.0
   git merge upstream/V3.0 --ff-only
   ```
2. Rebase your keymap onto V3.0:
   ```bash
   git checkout my-keymap
   git rebase V3.0
   ```
3. Resolve any conflicts if they occur.
4. Push the updated branch:
   ```bash
   git push origin my-keymap --force-with-lease
   ```

## Building the Firmware

### GitHub Actions (Simple)

1. Push a commit to your `my-keymap` branch on GitHub to trigger the build.
2. Go to the **Actions** tab in your repository.
3. Select the latest run and download the **firmware** artifact.

### Locally (macOS)

Requires `docker` and `colima`:
```bash
brew install docker colima
colima start
# On Apple Silicon: colima start --arch x86_64
```

1. Build for both halves:
   ```bash
   make
   ```
2. Find the results in the `firmware/` directory.
3. Cleanup:
   ```bash
   make clean
   ```

## Flashing firmware

1. Extract the firmwares from the archive.
2. Connect the **left** side keyboard to USB.
3. Press **Mod + macro1** to enter bootloader mode; it will mount as a USB drive.
4. Copy `left.uf2` to the drive. It will automatically disconnect.
5. Power off both keyboards (unplug and switch off).
6. Turn on the **left** side keyboard with the switch.
7. Connect the **right** side keyboard to USB.
8. Press **Mod + macro3** to enter bootloader mode.
9. Copy `right.uf2` to the mounted drive.
10. Unplug the right side and turn it back on.
11. Enjoy!

> **Note**: There are also physical reset buttons on both keyboards (near the RJ11 port) which can be used to enter bootloader mode.

## Resources

- [ZMK Documentation](https://zmk.dev/docs)
- [Key Positions Matrix](assets/key-positions.md)
- [Kinesis Support](https://kinesis-ergo.com/support/kb360pro/)
