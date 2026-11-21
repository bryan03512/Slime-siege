# Slime Siege

A first-person shooter in the browser. Slimes are invading your backyard garden, and you hold them off with a water blaster, wave after wave, picking an upgrade after each one. Every fifth wave the Slime King shows up.

Play it by opening `index.html` in a browser (it needs an internet connection to load three.js).

## Controls

- Move: WASD or arrow keys
- Look: mouse. ⌘ Command (Ctrl on Windows) turns mouse look on and off; mouse look locks the cursor to the middle of the screen
- Spray: hold the left mouse button
- Jump: Space, or the Jump button. Low, moon-style gravity: a good jump reaches the rooftops
- Minimap (bottom left): the whole garden, every slime, and you as a yellow arrow
- Parry: F. Bats goo back at whoever spat it, or shoves a slime away
- Dash: Shift, or the Dash button. Two charges; both come back when the cooldown ends
- Pause: Esc or P

On a phone: drag the left half of the screen to move, the right half to look, and use the round buttons to spray, jump and dash.

## Adding content

Everything you'd want to add lives in tables near the top of the script in `index.html`:

- `ENEMIES`: each slime type (health, speed, size, damage, score, which wave it first appears, color, and special moves like shooting).
- `UPGRADES`: the upgrade cards offered between waves (`apply` changes the player, `when` hides it when it wouldn't help).
- `OBSTACLES`: the hedges, crates, planters and fountain in the garden.

Built with [three.js](https://threejs.org/) r128.
