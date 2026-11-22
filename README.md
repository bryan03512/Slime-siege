# Slime Siege

A first-person shooter in the browser. Security robots are overrunning a dark city block at night, and you hold them off with a burst rifle, wave after wave, picking an upgrade after each one. Every fifth wave the Warden shows up. Every robot you take down earns coins, which are saved between runs and spent in the shop on new guns.

Play it by opening `index.html` in a browser (it needs an internet connection to load three.js).

## Controls

- Move: WASD or arrow keys
- Look: mouse. ⌘ Command (Ctrl on Windows) turns mouse look on and off; mouse look locks the cursor to the middle of the screen
- Shoot: left mouse button. The starting rifle fires 3-round bursts; hold to keep bursting
- Reload: R, or the Reload button. It also reloads by itself when the magazine runs dry
- Jump: Space, or the Jump button. Low, moon-style gravity: a good jump reaches the rooftops
- Dash: Shift, or the Dash button. Flings you the way you're moving and the speed carries on; look up (or hold Space) to dash upwards, look down to dash downwards. Dashing cancels a grapple fling, and holding the opposite direction brakes any fling. Two charges; both come back when the cooldown ends
- Focus: C (if bought). Slows time for 3 seconds; recharges in 15
- Swap weapon: Q, or the Swap button. You carry every gun you own plus a long sword; each swing cuts everything in front of you for half a second, hits harder the faster you're going (up to 3x), and you can't be hurt while it swings
- Grapple: hold the right mouse button (or E) to reel yourself to wherever you're aiming (up to 70m), or onto a robot at any distance. The speed you build up carries on after you let go, and grappling something above you flings you up past it
- Parry: F. Knocks energy bolts back at whoever fired them, or shoves a robot away
- Pause: Esc or P

On a phone: drag the left half of the screen to move, the right half to look, and use the round buttons to fire, reload, grapple, jump, dash and parry.

The HUD shows health (bottom centre, 100 to start), ammo (bottom right), a height gauge (left edge: metres up, vertical speed, and with the war hammer in the air an estimate of the slam damage), and a radar (bottom left) centred on you that turns with you, so behind you is the bottom of the circle. Robots off-screen get glowing arrows around the edge of the screen pointing the way to turn.

## Shop

Coins buy:
- **Weapons**: machine gun, sniper, railgun (hold to charge a beam that goes through everything), war hammer (melee; click in the air to dive and slam, bigger shockwave from higher up). Each weapon can be levelled up to 5 (+12% damage, +15% magazine, faster reloads per level).
- **Loadout**: you take up to 2 guns and 1 melee weapon into a run, chosen in the shop. Q swaps between them.
- **Gear**: third dash, armour vest (125 health), coin booster (+25% coins), med-kit finder, Focus, and Second chance tokens (revive once per run; hold up to 3).
- **Style**: accent colours and crosshair shapes.

Gravity builds the longer you fall. The long sword only protects you mid-swing while you're moving fast (dashing, grappling or dropping).

## Adding content

Everything you'd want to add lives in tables near the top of the script in `index.html`:

- `ENEMIES`: each robot type (health, speed, size, damage, score, coins, which wave it first appears, colours, and special moves like flying and shooting).
- `UPGRADES`: the upgrade cards offered between waves (`apply` changes the player, `when` hides it when it wouldn't help).
- `OBSTACLES`: the buildings, cars, walls, crates and barriers in the city.
- `GUNS`: the weapons and their shop prices (mode: burst, auto, single, charge or melee). `GEAR`, `COLORS`, `CROSSES` and `LEVEL_COST` hold the rest of the shop. The burst rifle is free; the machine gun (full auto, small spread, near misses still count) and the sniper (one huge round per magazine that bursts in a 3.5m blast where it hits the ground or a wall; in the air, a first click scopes in, slows time and shows every robot's hitbox as a cyan box, and a second click fires). Every robot's hitbox is a box (`hitboxOf()`): a shot that enters it hits are bought with coins.

Everything saves in the browser: coins (`ss-coins`, saved the moment you earn them), owned and equipped guns (`ss-guns`, `ss-gun`), best score (`ss3-best`), sound (`ss-muted`), and the run in progress (`ss-run`, saved every 2 seconds and when you leave the page). Continue on the main menu picks a saved run back up.

Built with [three.js](https://threejs.org/) r128.
