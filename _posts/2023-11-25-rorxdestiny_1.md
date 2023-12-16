---
title: RoRxDestiny 1 - Inception
date: 2023-11-15 18:36:00 +0800
categories: [RoRxDestiny]
tags: [gamedev]     # TAG names should always be lowercase
image:
    path: /assets/images/terminal.jpg
---
<link rel="stylesheet" href="{{ site.baseurl }}/assets/css/adds.css">


## Why did you want to start making this game?

I needed something to do. I also felt like I could pull something like this off for once, after learning so much at UniMelb. Doing side projects in C or Processing didn't feel too fulfilling - anyone could plug these small steps into StackOverflow or ChatGPT and get their answers in moments. Besides, it makes for a good resume or portfolio project. It's going to start small and might grow to be something big.

## Why start devlogging?

It feels like some kind of journaling, which I already do. It'll help keep me motivated and to see overall progress, jot down notes that will last longer than pen on paper, and to keep track of changes I've made.

In fact, I've already done a chunk of the project before I decided to start devlogging, but I'm just going to pretend here that I've devlogged since the beginning.

## What tools/software did you choose and why?

At first I considered using Java to make it. It *is* suitable for a game (Minecraft was made in it), and there are a lot of game engines in Java to make any kind of game. Also, my only experience in gamedev was in Java. I made a simple RPG, built Pac-Man and extended every mechanic (also a level editor!), and banged together Guitar Hero in 6 hours. I loved using IntelliJ and its linter - it tells you *everything* and it basically does the code for you!

But because it would make a resume look better, I chose to use Unity, which uses C#. C# is another OO language, and I already was comfortable with coding in C and Java. C and Java combined - how bad could it be? I decided to learn C# alongside learning how to use Unity. I justified this decision by telling myself that Unity had plenty of documentation and tutorials, so it wouldn't be like when I was trying to make a card game in Prolog - for context, you'd be basically trying to talk in Ancient Greek.

## What kind of game will it be and why?

A roguelike, of course. What else would anyone make for their first big game project? 

I'm kidding, but I did have another idea before choosing the roguelike in the end. I wanted to make some kind of space-themed text based game crossed with FTL, Seedship, Stellaris, and Starfield. You could customize every part of your ship with modular components, pick a point on a 3D map and fly there, provided you had enough fuel and your jump drive could reach it. There was a galaxy map and planets in each system, with dialogues and characters and vendors. There would be an overall story with side quests you could pick up, tying into one another. I planned the story before I realized the scope of the project, and how unreasonable it would be for a first big game. So I had to settle on something else, and I already knew the answer.

Call me old fashioned but I loved Risk of Rain 1 over Risk of Rain 2. The sequel just never felt the same as the first. It felt slow and I did not enjoy that you actually had to think about your build on harder difficulties. To me Risk of Rain was always a "shoot, turn your mind off, have fun" game, even on the hardest difficulty. I liked Vampire Survivors and 20 Minutes Until Dawn, and how you could mix upgrades and weapons together to create synergies become unstoppable. I also liked the buildcrafting and raiding/dungeon aspects of Destiny 2, where you complete multiple "encounters" involving puzzle mechanics and maybe a boss fight, leading up to a final boss encounter. I had also read sci-fi books - Alastair Reynolds, Isaac Asimov, Frank Herbert - and I devoured them. I took these ideas (as well as the space idea because I liked space) and it became the foundation of the game I wanted to create. I hadn't played a lot of other roguelikes, and my idea would not be the first, but I knew where to take it and I thought I would be proud of my end product.

## What are the game mechanics, rules, etc and how will it be fun?

Everything I am about to say is subject to change.

There are scenarios (levels) with some sort of overarching story contained in them. For example, one level would see the player dropped in as an elite soldier in the terminals of a space habitat, clearing hordes of enemies and clearing the way for civilians to a docked ship. The player would have to solve puzzles to power up the terminal boards that shows the map to the correct ship; other pathways would lead to extra loot or collectibles. Hordes of enemies would emerge from side doors that would drop gold that could open chests which contain upgrades/loot. It should be long enough to not feel too repetitive but not too short so that the story feels rushed.

The puzzle aspect is taken from the dungeon/raiding part of Destiny 2. I don't want the puzzles to be too easy to do. The puzzles should be slightly different each time. At the same time I want to balance enemy spawns and damage received and dealt at each point in time. Upgrades are still being worked on, since it also depends on my choice of how many characters can be played. Should it be a small number of characters (upgrades will primarily affect player weapon of choice) or should there be a motley of characters (upgrades will primarily affect player stats)? Or even just one character?

## How much time will you dedicate to this?

I am not going to focus all my time on this. From experience, it will lead to burnout, overthinking, exhaustion, then inevitably put on the ever-growing "list of things to do". I also have other hobbies that I allocate time for: running, cooking, drawing, gaming, and reading. After completing four half marathons, I am training for a full one. I am in the middle of rereading some of my favourite books. I raid with friends every few days. But I do want to make progress in a regular manner.

## Could you summarize parts of the story of the original game you had planned before reality set in?

Why, thank you for asking! Keep in mind I had abandoned planning the story after I realized the scope of the game, but I had written some excerpts/lore and some art on the side as well. So, the lesson here is that first decide on the game mechanics *then* plan out the story.

> The city of Glass lay before me, tens of miles below the transport bringing hundreds of passengers down from the spaceport. 
> 
> The metropolis sprawled across one of the only contiguous landmasses of Cascadia. An ordered tangle of marble-white megalithic complexes stretched from sunrise to sunset, with the occasional spire breaking through the plascrete jungle which thrusted into the stratosphere.

In the near future, gateway technology has paved the way for a new golden age of exploration. It has not been long since the first gateways were built, so humanity has only colonized a number of nearby systems. 

The player is a specialized courier, working for a nondescript company in the biggest terminal hub of the settled systems. This company is a front for the transport of illegal or illicit goods to anyone - pay the steep fee, give an address and time, and it will probably reach its destination. Couriers are trained in social engineering and combat, and have established rapport with many people across the systems. Since space travel is strictly regulated, clients ranging from the highest of classes to the dirt poor turn to these services for business.

> I was born in a house with a million rooms, built on a small, airless world on the edge of an empire of light and commerce.
>
> During the years of my childhood, I only saw a fraction of that vast, rambling, ever-changing mansion. Even as I grew older, I doubt that I ever explored more than a hundredth of it. I was intimidated by the long, forbidding corridors or mirror and glass, the corkscrewing staircases rising from dark cellars and golden vaults where even the adults never went, the rooms and parlours that were alleged to be haunted. The elevators alarmed me when they moved without apparent instruction, obeying some inscrutable whim of the house's governing persona. It was a mansion of ghosts and monsters, with ghouls in the shadows and demons scurrying behind the cupboards.

The player maintains or builds rapport with people across planets while carrying out routine deliveries, doing side quests for underground street rats, mercenaries, local governments, and corporations. 

For example in one of the side questlines, the Company is interested in maintaining a good relationship with Pirandello Group, which is engaged in a corporate cold war with its rival Wanderborn Holdings over gateway disputes. Pirandello was the brain behind reverse engineering the first gateway, and the exact technology has remained a secret since. Wanderborn, however, is close to inventing something similar and is rumoured to be a faster mode of transportation. Whichever mode of travel between star systems is fastest and/or cheapest will control the vast majority of space travel. 

The player is tasked with infiltrating and sabotaging the production of Wanderborn's new invention in various manufacturing plants across the systems. Along the way, Wanderborn Securities gets wind of this and attempts to convince the player to join their side, citing Pirandello's massive but declining influence within the corporate sphere, and a potential overthrow with Pirandello's other rival corporations. Whichever corporation the player sides with will invite them to a gala, where the director is assassinated while giving a speech. If the player chooses to join Wanderborn and the other corporations, all of them unite in a corporate war against Pirandello. Any relations to the Company is severed and Wanderborn and co. pledge their resources to you and the Company. Wanderborn Holdings makes a bid for the Conglomerate Director Chair after their own gateway technology is unveiled. 

If the player chooses to stay with Pirandello, they remove any hope of a power grab by sabotaging the mega-manufactories, and intercepts communications pinpointing the locations of the engineering leads. The veteran company ousts the corporate houses in the next general assembly.

> Cryo-rifle
> 
> NOT a freeze ray. Made to be small and inconspicuous. Fires ice-slugs: bullets of pure water-ice accelerated to supersonic speed by a captive jacket driven down the barrel by a sequenced ripple of magnetic fields.
> 
> Ice slugs do as much damage as metal or ceramic bullets, but when they shatter in the body, their fragments melt away invisibly.
> 
> The main advantage in such a weapon is that it could be charged from any supply of reasonably pure water, although it works best with carefully pre-frozen cache of slugs in the weapon's manufacturer-supplied cryo-clip.
> 
> It is nearly impossible to trace the owner of such a gun if a crime has been committed, making it an ideal assassination tool. The slugs have no autonomous target-seeking capacity, and they cannot penetrate certain kinds of armour. This is not meant to be a gun for a kill where you sit in a window squinting through the telescopic sight of a high-powered rifle, waiting until your target intersects the crosshairs, their image wavering through kilometres of heat-haze. This is a gun where you walked into the same room and did it with a single bullet at close range, close enough to see the whites of their fear-dilated eyes.

The main story revolves around the general assembly, a diplomatic gathering of governmental bodies, peoples unions, corporations, and organizations to resolve disputes, negotiate trade agreements, create alliances, or formalize processes of feud. Bodies of power that manage to prove themselves to be worthy to be included in the assembly hold vastly more political and economic influence, as it serves as a staging ground - a sort of "elite's club" - for any serious interplanetary matters. The Company is approached by a team, led by 'The Mule', who commissions the player to help them infiltrate the general assembly by posing as a legitimate assembly organization. Although their end goal is unclear, the Company offers you as one of their elite operatives due to the vast sums of money being supplied. 

> She had travelled a long way to make her case. The faint possibility of failure had always been at the back of her mind, but now that her ship had actually delivered her to the interstellar assembly, now that she had actually been launched from Helicon across all those dizzying light-years, the faint possibility had sharpened into a stomach-churning conviction that she was about to suffer imminent and chastening defeat. There had always been people eager to tell her that her proposal was doomed, but for the first time it occurred to her that they could be right. What she had in mind was, even by her own admission, a deeply unorthodox suggestion.
> 
> She was a politician, a constituent from the Congress of the Neume Ring. She spoke for a relatively small grouping of settled worlds: a mere thirty planet-class entities, packed into a volume of space only one light-year across. Without her husband's convincing thirty worlds that this was something they had to support, the plan would have stalled long ago.
> 
> The chamber had been constructed in the early decades of the Assembly, when it had aspirations to expand into territory now occupied by neighbouring politics. Space not being at a premium in the centre of Assembly territory, the thousands of representatives were scattered across a square kilometre of gently sloping floor space, and the ceiling was ten kilometres above their heads. Slowly rotating in the middle of the room, lacking any material suspension, was the display cube in which their enlarged images would appear when they had the floor. While it waited for the session to begin, the cube projected the emblem of the Assembly. 
> 
> It was difficult to judge the mood of the gathering. But her husband's advice had been sound. She held her nerve, and when she had the floor she spoke the words she had already committed to memory before leaving home.
> 
> "Honoured delegates," she began, as her magnified image appeared in the display cube...

Firstly, the player is tasked to intercept a prison transfer from a maximum security prison around a black hole. Due to the proximity of the prison to the event horizon and the accretion disk, it is near impossible for enemy vessels to hijack or attack the prison due to the heat and the effects of time dilation. For the same reason, escort vehicles do not join the transport vessel until a safe distance away. One of the Mule's ships has already been waiting a number of years near the prison, using the heat from the accretion disk as camouflage. (stopped here)

The player travels to the capital planet and seeks out the help of the local underground to break in the necessary office, hack the central database, and forge the documents required. The underground faction firsts directs the player to rescue local gang leader  , who was kidnapped by unknown assailants and held hostage in a spaceship in orbit. The player uses the city's stormdrain system to navigate to Central Assembly Offices undetected, and disguises as a security guard before accessing an administration computer. The operation is a success, and The Mule reveals that they plan to cut off the assembly from the rest of the gateway network while they are in session. (stopped here)

> She glanced outside the viewport as the ship's ring rotated around to face antisunward, and the glow of a thousand lights shone back - a guiding light in a sea of stars. 
> 
> Encircled around a five-kilometre iron core were eight rings five hundred kilometres in diameter. Upon the outward surface of each eight rings lay thirty-one hundred kilometres of fertile land, artificial rivers, valleys, and oceans, teeming with life. Thrusters lined the east walls to rotate the structure to simulate a night cycle. A ninth ring bisected the sphere at its equator perpendicular to the earlier eight, and it was christened The Vale of Babylon. On this ring lay (...)
> 
> Babylon was a monument to human arrogance. It took one hundred and sixty years of uninterrupted construction. Three entire Locals were stripped of resources to manufacture the megastructure. The orbits of the system were permanently altered to support its existence. And she called it home.
