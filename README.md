# Management of my dotFiles

I'm using chezmoi for this, so to get up and running, perform the following:

`winget install twpayne.chezmoi`

Then restart your shell and run

`chezmoi init --apply JohnyWS`

Next, configure new SSH Keys in 1Password, where details are then needed for the config:

`chezmoi edit-config`

Lastly, apply the config changes:

`chezmoi apply -v`

Your new computer is now setup.

Note: If you've created new SSH Key for this (recommended per PC), then make sure to add the public signature to GitHub.
