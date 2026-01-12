# Eurion OS (alpha)

Eurion OS è un progetto di sistema operativo desktop “europeo” sicuro-by-design, costruito come immagine immutabile (Fedora Atomic) e derivato in modo riproducibile.

## Obiettivi (alpha)
- UX desktop “Windows-like” ma moderna (KDE)
- Aggiornamenti atomici + rollback
- Telemetria: opt-in e conforme GDPR (design goal)
- App baseline: Office, password manager, media, compatibilità app Windows tramite Bottles (Wine)

## Installazione (per tester)
> Nota: rebasing è una feature sperimentale.

1) Rebase a immagine **non firmata** (installa policy/chiavi):
```bash
sudo rpm-ostree rebase ostree-unverified-registry:ghcr.io/europnproject/eurion-os:latest
sudo systemctl reboot


# eurion-os-image &nbsp; [![bluebuild build badge](https://github.com/hackth3w0rld/eurion-os-image/actions/workflows/build.yml/badge.svg)](https://github.com/hackth3w0rld/eurion-os-image/actions/workflows/build.yml)

See the [BlueBuild docs](https://blue-build.org/how-to/setup/) for quick setup instructions for setting up your own repository based on this template.

After setup, it is recommended you update this README to describe your custom image.

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/hackth3w0rld/eurion-os-image:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/hackth3w0rld/eurion-os-image:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/hackth3w0rld/eurion-os-image
```
