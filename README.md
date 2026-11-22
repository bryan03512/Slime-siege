# Slime Siege

A first-person shooter in the browser. Security robots are overrunning a dark city block at night, and you hold them off with a burst rifle, wave after wave, picking an upgrade after each one. Every fifth wave the Warden shows up. Every robot you take down earns coins, which are saved between runs and spent in the shop on new guns.

Play it by opening `index.html` in a browser (it needs an internet connection to load three.js).

## Controls

- Move: WASD or arrow keys
- Look: mouse. ⌘ Command (Ctrl on Windows) turns mouse look on and off; mouse look locks the cursor to the middle of the screen
- Shoot: left mouse button. The starting rifle fires 3-round bursts; hold to keep bursting
- Reload: R, or the Reload button. It also reloads by itself when the magazine runs dry
- Jump: Space, or the Jump button; press again in the air to double jump. Low, moon-style gravity: a good jump reaches the rooftops
- Dash: Shift, or the Dash button. Flings you the way you're moving and the speed carries on. Two charges; both come back when the cooldown ends
- Swap weapon: Q, or the Swap button. You carry every gun you own plus a knife; the knife makes you untouchable while it swings
- Grapple: hold the right mouse button (or E) to reel yourself to wherever you're aiming. The speed you build up carries on after you let go, and grappling something above you flings you up past it
- Parry: F. Knocks energy bolts back at whoever fired them, or shoves a robot away
- Pause: Esc or P

On a phone: drag the left half of the screen to move, the right half to look, and use the round buttons to fire, reload, grapple, jump, dash and parry.

The HUD shows health (bottom centre, 100 to start), ammo (bottom right), and a radar (bottom left) centred on you that turns with you, so behind you is the bottom of the circle. Robots off-screen get glowing arrows around the edge of the screen pointing the way to turn.

## Adding content

Everything you'd want to add lives in tables near the top of the script in `index.html`:

- `ENEMIES`: each robot type (health, speed, size, damage, score, coins, which wave it first appears, colours, and special moves like flying and shooting).
- `UPGRADES`: the upgrade cards offered between waves (`apply` changes the player, `when` hides it when it wouldn't help).
- `OBSTACLES`: the buildings, cars, walls, crates and barriers in the city.
- `GUNS`: the guns and their shop prices. The burst rifle is free; the machine gun (full auto, small spread, near misses still count) and the sniper (one huge round per magazine; in the air it slows time, zooms in and shows every robot's hitbox in cyan) are bought with coins.

Coins, owned guns and the equipped gun are stored in the browser under `ss-coins`, `ss-guns` and `ss-gun`.

Built with [three.js](https://threejs.org/) r128.
