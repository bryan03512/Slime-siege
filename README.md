# Slime Siege

A first-person shooter in the browser. Security robots are overrunning a dark city block at night, and you hold them off with a burst rifle, wave after wave, picking an upgrade after each one. Every fifth wave the Warden shows up. Every robot you take down earns coins, which are saved between runs for the shop (coming soon).

Play it by opening `index.html` in a browser (it needs an internet connection to load three.js).

## Controls

- Move: WASD or arrow keys
- Look: mouse. ⌘ Command (Ctrl on Windows) turns mouse look on and off; mouse look locks the cursor to the middle of the screen
- Shoot: left mouse button. The starting rifle fires 3-round bursts; hold to keep bursting
- Reload: R, or the Reload button. It also reloads by itself when the magazine runs dry
- Jump: Space, or the Jump button. Low, moon-style gravity: a good jump reaches the rooftops
- Dash: Shift, or the Dash button. Two charges; both come back when the cooldown ends
- Parry: F. Knocks energy bolts back at whoever fired them, or shoves a robot away
- Pause: Esc or P

On a phone: drag the left half of the screen to move, the right half to look, and use the round buttons to fire, reload, jump, dash and parry.

The HUD shows health (bottom centre, 100 to start), ammo (bottom right), and a minimap of the whole block (bottom left).

## Adding content

Everything you'd want to add lives in tables near the top of the script in `index.html`:

- `ENEMIES`: each robot type (health, speed, size, damage, score, coins, which wave it first appears, colours, and special moves like flying and shooting).
- `UPGRADES`: the upgrade cards offered between waves (`apply` changes the player, `when` hides it when it wouldn't help).
- `OBSTACLES`: the buildings, cars, walls, crates and barriers in the city.
- The starting gun's numbers (`burst`, `burstGap`, `burstPause`, `mag`, `reloadTime`) are in `newRun()`; new guns will go alongside it.

Coins are stored in the browser under `ss-coins`.

Built with [three.js](https://threejs.org/) r128.
