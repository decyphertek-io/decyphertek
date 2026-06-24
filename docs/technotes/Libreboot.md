Libreboot — free/open BIOS/UEFI firmware replacement for the Lenovo ThinkPad T480s. This guide covers the **T480s (S model) only**. Do NOT use T480 ROMs — the boards have different wiring and you will brick.

Official docs (diffuse, heavily cross-linked): https://libreboot.org/docs/install/t480.html

Prerequisites:
-------------
* Linux machine (Debian/Ubuntu recommended). You must also read https://libreboot.org/docs/install/ivy_has_common.html before flashing or you WILL brick (vendor file injection).
* External SPI programmer supported by Libreboot. Recommended: **Raspberry Pi Pico** flashed with `pico-serprog`. See the 25XX NOR flashing guide: https://libreboot.org/docs/install/spi.html
* SOIC8 test clip (Pomona 5250 / generic), jumper wires.
* Two SPI flash chips on the T480s motherboard:
  1. **Main system flash** — 16MB / 128Mbit — Libreboot goes here (centrally located, near the RAM).
  2. **Thunderbolt firmware flash** — 1MB — near the board edge. Must be fixed FIRST.
  flashprog will warn about wrong size if you attach the clip to the wrong chip — use that as a sanity check.

Install:
--------
```
# ===========================================================================
# 1) GET LBMK (Libreboot build system) + flashprog
# ===========================================================================
git clone https://libreboot.org/lbmk.git
cd lbmk

# Install build deps (adapt the target to your distro: ubuntu2004/debian11/etc.)
sudo ./mk dependencies debian11

# Build flashprog (output lands in util/flashprog/flashprog)
./mk -b flashprog

# Put it on PATH for convenience
sudo cp util/flashprog/flashprog /usr/local/bin/
which flashprog

# Verify programmer is seen (Pi Pico + serprog shows up as /dev/ttyACM0)
ls -l /dev/ttyACM0

# ===========================================================================
# 2) DOWNLOAD / GENERATE VENDOR FILES  (incl. Thunderbolt firmware tb.bin)
# ===========================================================================
# Pulls Intel ME, deguard blobs, and the Lenovo Thunderbolt .exe (auto-extracted
# via innoextract) and pads tb.bin to 1MB.
# MUST be t480s_vfsp_16mb — NOT t480_vfsp_16mb (different board!)
./mk -d coreboot t480s_vfsp_16mb

# Outputs you'll use later:
#   vendorfiles/t480s/tb.bin   <- Thunderbolt firmware, 1MB, padded

# ===========================================================================
# 3) UPDATE LENOVO UEFI + EC FIRMWARE  (do this BEFORE touching Libreboot)
# ===========================================================================
# T480 (non-S) REQUIRES a specific version: n24ur39w.
# T480s (S model): EC version does not matter for S, but still update to
# the latest Lenovo UEFI/EC from the support page:
#   https://pcsupport.lenovo.com/.../thinkpad-t480s-type-20l7-20l8/downloads
#
# In Lenovo UEFI setup:
#   - Disable Secure Boot
#   - Enable Legacy/CSM boot
#   - Enable "Flash BIOS Updating by End Users"
#   - Disable "Secure Rollback Prevention"
#
# Convert the bootable ISO to an img and write to USB:
geteltorito -o t480s_bios.img /path/to/lenovo_bios_update.iso
sudo dd if=t480s_bios.img of=/dev/sdX bs=4M conv=fsync status=progress
#
# Boot USB in LEGACY mode -> pick option 2 (update BIOS + EC).
# Keep battery charged + charger plugged in.
# FULLY shut down after the update.

# ===========================================================================
# 4) THUNDERBOLT FIRMWARE FIX  (MUST do BEFORE flashing Libreboot)
#    CRITICAL ORDER: dump -> erase -> flash null.bin -> BOOT & confirm
#                    -> shut down -> THEN flash tb.bin
#    Do NOT erase and flash tb.bin in one pass or you risk a non-booting
#    Thunderbolt controller.
# ===========================================================================
# Disassemble T480s:
#   - Remove bottom case screws, pry off lower chassis.
#   - Disconnect/remove the internal battery (T480s battery is large; the
#     connector is built into the battery, so remove the whole battery).
#   - Remove the CR2032 coin cell.
#   - In Lenovo UEFI: disable "ThunderBolt Assist" if present.
#
# Locate the Thunderbolt SPI flash (smaller chip, near the board edge).
# Attach SOIC8 clip to the TB flash.

# 4a) Make TWO backup dumps and confirm they match
flashprog -p serprog:dev=/dev/ttyACM0 -r tb_dump1.bin
flashprog -p serprog:dev=/dev/ttyACM0 -r tb_dump2.bin
sha512sum tb_dump1.bin tb_dump2.bin   # must be identical; keep these safe

# 4b) ERASE the Thunderbolt flash
flashprog -p serprog:dev=/dev/ttyACM0 -E

# 4c) Create a 1MB all-zero file and flash it
dd if=/dev/zero of=null.bin bs=1M count=1
# Verify it really is all-zero and 1MB (hexdump null.bin | head)
flashprog -p serprog:dev=/dev/ttyACM0 -w null.bin

# 4d) REMOVE the clip, reassemble enough to boot, connect battery first
#     then charger. Power on. It SHOULD show the Lenovo boot screen.
#     (This may take a while — be patient.)
#     Once you confirm it boots Lenovo firmware, FULLY shut down and
#     disconnect all batteries/charger again.

# 4e) NOW flash the real Thunderbolt firmware
#     (re-attach clip to the TB flash)
flashprog -p serprog:dev=/dev/ttyACM0 -w vendorfiles/t480s/tb.bin
#
# Remove clip, reassemble, boot. Should again show Lenovo boot screen, and
# USB-C / Thunderbolt / fast charging will work correctly.

# ===========================================================================
# 5) PREPARE THE LIBREBOOT ROM  (vendor file injection + MAC address)
# ===========================================================================
# Option A: build the ROM from source
./mk -b coreboot t480s_vfsp_16mb
#   -> produces bin/t480s_vfsp_16mb/*.rom  (12MB after build)
#
# Option B: use a pre-compiled release ROM from https://libreboot.org/download.html
#   (in either case you MUST inject vendor files next — see step 5b)

# 5b) Inject vendor files into the ROM (DO THIS BEFORE FLASHING or you brick)
#     See: https://libreboot.org/docs/install/ivy_has_common.html
./mk inject bin/t480s_vfsp_16mb/<your_rom>.rom
#   (this pulls Intel ME, deguard blobs, and configures them automatically)

# 5c) Set the MAC address (otherwise you get a generic/default MAC)
#     Libreboot ships nvmutil for the Intel GbE NVM region.
#     IMPORTANT: if using ifdtool, pass --platform sklkbl or the IFD will
#     be handled incorrectly.
#     See: https://libreboot.org/docs/install/nvmutil.html
# Example:
#   ./mk -b nvmutil            # build nvmutil if not already built
#   ./util/nvmutil/nvmutil your_rom.rom setmac <your:mac:here>

# ===========================================================================
# 6) FLASH LIBREBOOT TO THE MAIN 16MB SYSTEM SPI CHIP (hardware/external)
# ===========================================================================
# Internal flashing is NOT possible from Lenovo BIOS — you must flash
# externally. (Internal flash is only available AFTER Libreboot is installed
# and flash protections are off.)
#
# Disassemble again, disconnect all batteries + coin cell.
# Attach the SOIC8 clip to the MAIN system flash (16MB, central, near RAM).

# 6a) Back up the original Lenovo firmware — make two dumps, verify match
flashprog -p serprog:dev=/dev/ttyACM0 -r lenovo_main_dump1.bin
flashprog -p serprog:dev=/dev/ttyACM0 -r lenovo_main_dump2.bin
sha512sum lenovo_main_dump1.bin lenovo_main_dump2.bin   # must match
# KEEP THESE. They are your recovery path back to Lenovo firmware.

# 6b) Write the prepared Libreboot ROM (with vendor files + MAC injected)
flashprog -p serprog:dev=/dev/ttyACM0 -w bin/t480s_vfsp_16mb/<your_rom>.rom

# 6c) Verify the write
flashprog -p serprog:dev=/dev/ttyACM0 -v bin/t480s_vfsp_16mb/<your_rom>.rom

# 6d) Remove clip, reassemble, reconnect battery, power on.
#     Libreboot should boot. If it doesn't, reattach clip and reflash from
#     your lenovo_main_dump1.bin backup.

# ===========================================================================
# 7) POST-INSTALL
# ===========================================================================
# Once Libreboot is running:
#   - Internal flashing works (with /dev/mem protections disabled):
#       https://libreboot.org/docs/install/devmem.html
#   - HyperThreading is DISABLED by default (security). Re-enable via:
#       ./mk -m coreboot t480s_vfsp_16mb   (Chipset -> Enable Hyperthreading)
#   - TPM is disabled by default (SeaBIOS TPM driver bug).
#   - Thunderbolt itself still needs further testing in Libreboot; the TB
#     firmware fix above prevents the brick/log-overflow issue but full
#     TB hotplug under Libreboot is not yet validated.
#   - thinkpad_acpi may not load correctly — see:
#       https://libreboot.org/faq.html#thinkpad-acpi
```

Notes:
-----
* The T480 and T480s are NOT interchangeable. ROM, tb.bin, and flash layout differ.
* If you mess up the Thunderbolt sequence, repeat erase -> null.bin -> boot -> tb.bin; it's recoverable.
* Keep all dump files forever — they're your only way back to Lenovo firmware.
* Full official docs (with photos of the chip locations and battery connectors): https://libreboot.org/docs/install/t480.html
