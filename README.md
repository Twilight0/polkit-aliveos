# 🛡️ polkit-aliveos — Modern, Transparent PolicyKit Authentication Agent for AliveOS

A lightweight, security-first **Polkit Authentication Agent** with a native **Zenity-GTK3** look and feel, built specifically for AliveOS (Wayland / Qtile / Saffron).

Unlike legacy agents (`polkit-gnome`) that hide the caller behind generic text and collapsed accordions, `polkit-aliveos` prominently exposes the **calling application executable**, **full binary path**, **arguments**, and **action ID** right in the main prompt.

---

## 🚀 Features (Core)

1. **Immediate Executable & Path Disclosure**:
   - Parses the calling process `/proc/<pid>/exe`, `/proc/<pid>/cmdline`, and Polkit `command_line` / `program` details.
   - Distinct, formatted caller box:
     - **Program**: `/usr/bin/foo`
     - **Arguments**: `--some-flag --option`
     - **Action ID**: `org.freedesktop.policykit.exec`
2. **Native Zenity-GTK3 Look & Feel**:
   - Styled to match Zenity dialogs (`Gtk.MessageDialog` / `Gtk.Dialog` standard GTK3 styling).
   - Dialog title, lock/shield icon, prominent primary text, clear secondary description.
   - Clean keyboard navigation: `Enter` to submit, `Esc` or `Backspace` to cancel.
3. **Password Reveal Toggle**:
   - Integrated eye icon button inside the password entry field (or hold `Tab`) to peek at the typed password.
4. **Desktop Environment Independence**:
   - Pure Python 3 + PyGObject (`GTK3`, `PolkitAgent 1.0`, `Polkit 1.0`).
   - Zero GTK4 / libadwaita dependencies (strictly conforms to AliveOS GTK3 policy).
   - Native Wayland & X11 compatibility.

---

## 🎛️ Companion Configuration Utility (`polkit-aliveos-config`)

A companion GUI settings utility allows customizing authentication behavior:

| Setting | Description | Default |
| :--- | :--- | :--- |
| **`reveal_password_toggle`** | Show/hide eye icon inside password entry field | `True` |
| **`screen_dimming`** | Dim desktop background (Windows UAC style) during prompt | `False` |
| **`auth_sound`** | Play notification chime when elevation is requested | `True` |
| **`sound_theme_event`** | Audio event for prompt chime (`dialog-warning` / `security-high`) | `dialog-warning` |
| **`auto_expand_details`** | Expand deep technical security tokens by default | `False` |
| **`timeout_seconds`** | Auto-cancel prompt if left unattended | `60` |

---

## 🗺️ Roadmap & Integration with AliveOS TODO

From [`aliveos/TODO.md`](../aliveos/TODO.md):

- [x] **Section 6: GTK3 Policy Compliance**: Zero GTK4/libadwaita dependencies; uses standard GTK3 widgets and theme styling.
- [ ] **Section 8 (Phase 4): Screen Lock / Auth Integration**:
  - Unified credential caching / PAM integration with Saffron lock screen.
  - Optional PIN authentication support (`pam_pwdfile.so`) for fast privilege elevation.
  - Multi-factor authentication prompt support (YubiKey / FIDO2 / TOTP).
- [ ] **Windows UAC-Style Screen Dimming**:
  - Under Wayland: Layer-shell semi-transparent dark overlay (`gtk-layer-shell` or wlr protocol).
  - Under X11 / Qtile: Full-screen translucent backdrop window.
- [ ] **Packaging (`aliveos-repo`)**:
  - Create `PKGBUILD` for `polkit-aliveos` in `aliveos-repo/packages/`.
  - Default autostart entry for Saffron and Qtile sessions.
