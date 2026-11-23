# Slime Siege

A first-person shooter in the browser. Security robots are overrunning a dark city block at night, and you hold them off mostly with your blade (guns are a backup), wave after wave, picking an upgrade after each one. Every fifth wave the Warden shows up. Every robot you take down earns coins, which are saved between runs and spent in the shop on new guns.

Play it by opening `index.html` in a browser (it needs an internet connection to load three.js).

## Controls

- Move: WASD or arrow keys
- Look: mouse. ⌘ Command (Ctrl on Windows) turns mouse look on and off; mouse look locks the cursor to the middle of the screen
- Shoot: left mouse button. The starting rifle fires 3-round bursts; hold to keep bursting
- Reload: R, or the Reload button. It also reloads by itself when the magazine runs dry
- Jump: Space, or the Jump button. Low, moon-style gravity: a good jump reaches the rooftops
- Dash: Shift, or the Dash button. Flings you the way you're moving and the speed carries on; look up (or hold Space) to dash upwards, look down to dash downwards. Dashing cancels a grapple fling, and holding the opposite direction brakes any fling. Two charges; both come back when the 2-second cooldown ends
- Focus: C (if bought). Slows time for 3 seconds; recharges in 4
- Swap weapon: Q, or the Swap button. You carry every gun you own plus a long sword; each swing cuts everything in front of you for half a second, hits harder the faster you're going (up to 6x), and you can't be hurt while it swings
- Grapple: hold the right mouse button (or E) to reel yourself to wherever you're aiming (up to 70m), or onto a robot at any distance. The speed you build up carries on after you let go, and grappling something above you flings you up past it
- Parry: F. Knocks energy bolts back at whoever fired them, or shoves a robot away
- Pause: Esc or P

On a phone: drag the left half of the screen to move, the right half to look, and use the round buttons to fire, reload, grapple, jump, dash and parry.

The HUD shows health (bottom centre, 100 to start), ammo (bottom right), a height gauge (left edge: metres up, vertical speed, and with the war hammer in the air an estimate of the slam damage), and a radar (bottom left) centred on you that turns with you, so behind you is the bottom of the circle. Robots off-screen get glowing arrows around the edge of the screen pointing the way to turn.

## Shop

Coins buy:
- **Weapons**: machine gun, sniper, railgun (hold to charge a beam that goes through everything), war hammer (melee; click in the air to dive and slam, bigger shockwave from higher up). Each weapon can be levelled up to 5 (+12% damage, +15% magazine, faster reloads per level).
- **Loadout**: you take one gun and one melee weapon into a run, chosen in the shop. Q swaps between them.
- **Gear**: third dash, armour vest (125 health), coin booster (+25% coins), med-kit finder, Focus (4s recharge), and Second chance tokens (revive once per run; hold up to 3).
- **Style**: accent colours and crosshair shapes.

Every weapon hits harder the faster you're moving: guns up to 2x at about 28 m/s, the sword up to 6x, the hammer much more; the readout beside the crosshair shows your current bonus. Gravity builds the longer you fall. The long sword only protects you mid-swing while you're moving fast (dashing, grappling or dropping).

## Adding content

Everything you'd want to add lives in tables near the top of the script in `index.html`:

- `ENEMIES`: each robot type (health, speed, size, damage, score, coins, which wave it first appears, colours, and special moves like flying and shooting). Waves are small (3 to about 12 robots); every wave brings at least one tank from the three tank tiers (Bulwark, Titan, Colossus, each bigger and tougher), and every fifth wave the Warden.
- `UPGRADES`: the upgrade cards offered between waves (`apply` changes the player, `when` hides it when it wouldn't help).
- `OBSTACLES`: the buildings, cars, walls, crates and barriers in the city.
- `GUNS`: the weapons and their shop prices (mode: burst, auto, single, charge or melee). `GEAR`, `COLORS`, `CROSSES` and `LEVEL_COST` hold the rest of the shop. The burst rifle is free; the machine gun (full auto, small spread, near misses still count) and the sniper (one huge round per magazine that bursts in a 3.5m blast where it hits the ground or a wall; in the air, a first click scopes in, slows time and shows every robot's hitbox as a cyan box, and a second click fires). Every robot's hitbox is a box (`hitboxOf()`): a shot that enters it hits are bought with coins.

Everything saves in the browser: coins (`ss-coins`, saved the moment you earn them), owned and equipped guns (`ss-guns`, `ss-gun`), best score (`ss3-best`), sound (`ss-muted`), and the run in progress (`ss-run`, saved every 2 seconds and when you leave the page). Continue on the main menu picks a saved run back up.

Built with [three.js](https://threejs.org/) r128.

## Melee first (v47)
- Every run starts with your melee weapon in hand. The long sword hits harder (6), reaches further (5 m) and swings faster.
- Guns do 60% damage and carry limited spare ammo (2 magazines). Melee kills refill spare ammo, heal 4 health and pay 1.5x coins.
- New upgrades: Keen edge (+30% melee damage), Long arms (+20% reach), Leech (melee kills heal more).
- Drones lock a red laser on you for 1.8 s, then fire an instant sniper shot. Parry just before it hits, or up to 0.5 s after, to cancel the damage and fire it back.
- Every fifth wave brings the Duelist instead of the Warden (1400 health): it strafes, dashes in, dodges your swings, winds up big cuts (parry to stagger it), grapples onto rooftops near you, and snipes from range with the drones' red-laser shot.
- New slash, hammer and melee-hit sounds.
- Damage numbers float up over robots when you hit them (white, orange for big hits, pink for the killing blow), and a red number pops over your health bar when you're hit.
- Tanks have double health: Bulwark 90, Titan 220, Colossus 520.
- Spear (140 coins, melee): a long narrow thrust (7 m) that pierces every robot in the line, with no 3-hit cap. Moving faster than about 11 m/s, it hits whatever is in its line on its own (half damage, each robot every 0.3 s). Weak per hit (2 base damage), but its speed bonus has no cap and climbs fast: ×(1 + (speed − 6)/3).
- Spear immunity: every thrust makes you immune for 0.8 s (0.4 s on each auto-hit that lands).
- The grapple has no top speed: it pulls harder the longer it's attached (70 m/s² at first, +28 m/s² every second), and it never slows you down if you came in faster. This also lets the spear's uncapped speed bonus go past 6x.

## Slime look, Goop and touch assists (v56)
- Every weapon is slime-styled: a see-through goo blade on the sword, a slime spear tip, a wobbling ball of slime for the hammer head, slime canisters on the guns, drips that wobble, green bullets and green hit splashes.
- The keyboard button bar at the bottom right is gone (controls are still in the menu). Goop, a little slime helper, sits there instead: he cheers kills and parries, flinches when you're hit, and gives tips (low health, drone lasers, the Duelist, out of ammo). On touch screens he sits on the right edge above the buttons.
- Touch screens only, rounds unchanged: a missed grapple looks within 15 degrees for a robot and within 12 degrees for a wall or roof (30% more range); melee swings turn you toward the nearest robot in front and reach 25% further; every swing gives 0.3 s immunity; getting hit gives 1.3 s immunity instead of 0.8; the parry window is 0.5 s instead of 0.3 and the late-parry buffer for drone shots is 0.8 s; gun near misses count from 1.2 m further.
- Grapple aim assist: of the robots within 6 degrees of your aim (18 on touch screens) that you can see, the grapple goes to the one with the most health; if there are none, it goes where you aim.
- Pause menu has End run (press twice): ends the run like dying, so your coins are kept and best scores count.
- Robot health grows faster with each wave: x(1 + 0.2(w-1)) x 1.04^(w-1), about 2x at wave 5, 4x at wave 10, 10x at wave 20. The Duelist gets 60% more each time it returns. The wave banner shows the current multiplier.
- The Duelist shoots about twice as often (every 2.4 s, 1.2 s lock-on). Above half health it launches into the sky and grapples straight onto you for a 30-damage dive (parry it to stagger it, or dash away). Below 45% health it swings from point to point in the sky around you, shooting every 1.3 s, then drops back down after a few swings.
- Long sword speed bonus: starts at 2.5x and gains 1x for every 12 m/s over 6 m/s (half as fast as before), up to 7.5x.

## The Duelist duel (v68)
- Boss waves are a one-on-one duel: only the Duelist spawns (no ring).
- Phases: at 66% and 33% health it roars (can't be hurt for 1.3 s), then blasts you back with a shockwave (12 damage within 22 m). Phase 2: 25% faster, quicker cuts, more dives, a shot every 1.8 s. Phase 3: swings around the sky shooting every 1.3 s.
- Clash: grapple into it while it's flying on its own grapple. Whoever is moving faster wins: if it's you, it's knocked out of the sky, stunned 2.2 s and loses 6% health; if it's faster, you're slammed down for 25 damage.
- Finisher: below 12% health, parrying its next cut, dive or shot finishes it in slow motion.
- It learns a move each time it returns: level 2 (wave 10) zig-zag triple dash, level 3 spinning slash (longer wind-up, 6.5 m reach), level 4 two one-hit decoy clones at each phase change, level 5 double shots.
- Headshots: gun hits on the top part of a ground robot's hitbox do double damage, with a cyan HEAD damage number.
- War hammer: base damage 2 (was 0.6). Swing bonus grows e^(0.09 per m/s over 6), up to 8x. Slam grows e^(0.12 per m fallen past 4 m), up to 200 (for example 14 from 20 m, 45 from 30 m, 150 from 40 m).
- Harder Duelist: when you grapple onto it, 45% of the time (60% from phase 2, at most every 4 s) it sidesteps and your line breaks. 30% of its cuts are fakes: it pulls back and swings for real 0.3 s later, so an early parry is wasted. Its cuts ignore dashes and immunity windows, except for 1 s after you parry one. From phase 2 its cuts chain: cut, dash in, cut, up to three in a row.
- Revives no longer trigger on their own: if you have one, the game over screen shows a Revive button (one per run) that puts you back into the run with half health and a shockwave. Not offered after End run.
- War hammer slam flings you back up on impact: 6.5 m/s upward plus a bit more for bigger drops (up to 18 m/s), so you can chain slams.

## New guns (v73)
- Slime shotgun (110): 8 pellets in a wide spray, 6 shells. Fired in the air, the kick throws you the opposite way you aim (17 m/s; a quarter of that on the ground): aim down to launch up, behind you to rocket forward.
- Acid SMG (130): fast weak spray (16 rounds/s); every hit sets the robot burning for 2.5 s (2.5 damage per second before boosts), and the burn keeps going while you move on.
- Rail bow (150): hold to draw (0.9 s), let go to loose a bolt. Damage scales from 25% to 100% with the draw (7 at full). A full draw pierces every robot in a line and pins each one in place for 4.5 s (bosses 1.8 s, and it knocks the Duelist off its grapple). No slow motion, unlike the railgun.

## New melee weapons (v74)
The shop's weapons are split into Melee and Ranged tabs. New melee weapons use their own speed bonus: +1x per 8 m/s over 6 m/s, up to 6x (the long sword keeps its 2.5x start).
- Pogo lance (140): stab on the ground; in the air, click to plunge. Landing on a robot bounces you off its head; each bounce in a row does +50% and throws you higher.
- Goo gloves (120): click to grab the robot in front and hold it up, click again to hurl it. It smashes into whatever it hits (3x to itself, 4x to everything within 3.5 m). Tanks and the Duelist are too big: you punch them.
- Drill blade (130): hold to grind the robot in front; damage climbs 1.2x per second of drilling, up to 6x, and you slowly push forward.
- Splitter axe (140): click to throw it into a robot up to 30 m away; click again to yank yourself to it and chop (5x, half that to robots within 4 m).
- Ricochet shield (130): hold to block (80% less damage; raising it counts as a parry). Tap to throw it: it bounces between up to 4 robots and comes back (1.2 s).
- Mirror blade (150): every swing leaves a slime copy that repeats it 0.35 s later from where you stood.
- Grapple blade (140): normal swings, plus grappling onto a robot ends in an automatic slash that grows 12% per metre you flew.
- You can look almost exactly straight up or down (89.7 degrees, was about 77).
- Skip lance (150, melee): like the pogo lance, but clicking in the air dives at an angle along the way you're moving (at least 16 m/s), and hitting a robot bounces you onward in the same direction, 12% faster each bounce (up to 60 m/s). +50% damage per bounce in a row.
