The game starts with Kai in the water, at the bottom of a waterfall. He wakes up next to the broken parts of his car, and he still has the horn. He stands up, walks out of the pool, steps onto the stone path and shakes the water off. Look at his clothes. They are wet, and they stay wet when the fight starts. After about forty seconds they dry. Wet clothes look dark and shiny. Dry clothes look light again.

Kai talks to himself. He thinks nobody is chasing him any more, because nobody would follow him over a waterfall. Now he only needs to take the horn to Baba Zwane, the old man from the fire in the prologue.

*(long pause)*

But Kai is wrong. The Marshal slides down a rope from the top of the waterfall to the stone arch. Then he jumps down behind Kai. The Marshal works for the company. He wears a strong coat and a carved mask. His men slide down the same rope after him, one by one.

They stand face to face and talk. The Marshal says the horn belongs to the company now. Kai does not know who is behind the mask. He says he is taking the horn to Baba Zwane, because Baba Zwane will know what to do. The Marshal only says: "Will he."

Then the screen shows Kai versus the Marshal, and the fight starts.

*(long pause)*

The fight has three parts. In part one, the Marshal does not fight. He stands by the arch and sends his three men first. When they are down, he says, "Fine. I'll do it myself." Then part two starts, and I fight the Marshal.

On this first try, I am still learning how he fights. He has four attacks: a lunge, a sweep, a two-hit combo and a spin kick. Before each attack, a coloured shape shows on the ground. Watch those shapes. They are made by a shader, and I will explain it soon.

*(long pause)*

And I lose. When my health goes down, the edges of the screen turn red. Kai falls, and the DEFEATED card comes up. I can choose TRY AGAIN or MAIN MENU.

*(pause)*

Now a short look at our Level 3 shaders.

*(pause)*

First, the coloured shapes on the ground. They warn you where the next attack will hit. A uniform called u-K goes from zero to one while the Marshal gets ready. As it grows, the shape fills up. When it is full, the attack hits. So you can see how much time you have. Each attack has its own colour.

*(pause)*

Second, the pool water. The waves come from moving noise, not a texture. The shader uses reflect to show the cliffs in the water, and refract to show the bottom of the pool. A Fresnel term mixes the two. Look straight down and you see into the water. Look across it and it looks like a mirror. A uniform called u-Tint can turn the water red. You will see that later.

*(pause)*

We made more shaders for Level 3: the waterfall, the Shadow Stag's glowing cracks, the spirit shrines that fill with light, the grey slow-motion screen, the light trails behind Kai's kicks, the fireflies, and Kai's wet footprints. You can find all of them in our repo.

*(long pause)*

So I press R to try again. This time the game skips the part where Kai wakes up. It goes straight to the Marshal and his men coming down the rope. While they come down, I will explain the screen.

*(pause)*

At the top left is Kai's box. It shows his name, his health bar in red, and a thin green bar for stamina. Punches, kicks and dodges use stamina. If you press too fast, Kai gets tired. Next to his name are three small icons: a heart, a diamond and a star. They light up when you get the spirits' gifts. I will talk about those soon.

In the middle at the top is the enemy's health bar. It shows his name and which phase of the fight he is in.

At the top right is a round camera button. Press Tab, or click it, to change the camera. There are three cameras. Follow stays behind Kai, and you look around with the mouse. Lock-on keeps the camera on your enemy, and Kai can move around him. The 360-degree view lets you turn the camera any way you want.

At the bottom left is the map. It shows the pool, the waterfall, the courtyard and the three spirit shrines in the jungle. Kai is the arrow. Press N to make the map bigger.

On the right are the action buttons. You can use them with touch or with the mouse. Each button also shows its key. PUNCH is Enter or left click. KICK is K. DODGE is C. BLOCK is B or right click. Hold it to block. Tap it just before a hit lands to parry. The blue button, HORN, is V. This is the horn's power. The ring around the button fills up while the power charges. You move Kai with W, A, S and D, or with the joystick on a touch screen.

When the Marshal is not on the screen, an orange arrow at the edge shows where he is. Small markers at the edge, with a distance on them, show where the spirit shrines are.

*(long pause)*

In the jungle around the courtyard there are three spirit shrines. Each one is a stone animal on a round stone circle. When Kai steps onto the circle, the spirit jumps out of the stone and into him.

The Stag Shrine gives back half your health. Then it sleeps for thirty seconds, and after that you can use it again. The Fox Shrine shows the Marshal's next attack under his health bar, and makes parrying easier. The Ember Shrine puts fire in Kai's hands. His punches and kicks become forty percent stronger. The Fox and the Ember last until the end of the fight.

You can leave the courtyard and run to the shrines, but the Marshal will follow you. This time, I take all three.

*(pause)*

With fire in my hands and the Fox showing his attacks, I beat his men and start to beat the Marshal.

In phase two, his mask comes off. It is Baba Zwane, the man from the fire. The man Kai was taking the horn to. The company paid him to get the horn. But he was too scared to take it himself, because the forest attacks anyone who takes it. So he sent Kai to take it instead. Kai was the bait. From now on, the health bar says BABA ZWANE.

*(pause)*

In phase three, the sun goes down, the torches turn on, a storm starts, and the pool and the waterfall turn red. This is the u-Tint uniform I showed you, going from zero to one.

*(pause)*

When he has only a quarter of his health left, he pulls the horn off Kai and uses it himself. Now he has a horn blast that hits in a ring all around him. But the forest punishes him for holding the horn. Every few seconds, lightning hits him and he is stunned. That is my chance to attack.

The last hit plays in slow motion, and the camera goes around them. He falls, and the horn falls out of his hand.

*(long pause)*

But it is not over. The horn is glowing red now, because his hand made it angry. The stone stag at the gate breaks open and jumps down. This is part three, the last fight: the Shadow Stag, our kudu.

It has three attacks. In the charge, it runs at you in a straight line. In the stomp, it hits the ground in a big circle around it. When it gets angry, thorns come up in a ring around it. Most of the time its skin is hard, and your hits only do forty percent damage. Its cracks glow red when its skin is hard, and blue when you can hurt it.

*(pause)*

This is where I made a mistake. I used everything on the Marshal, even the Stag Shrine's healing. When the kudu came, I had nothing left to help me, and it beat me. That is my second loss.

*(long pause)*

Third try. While they come down the rope, I will explain a few more things on the screen.

On the right side, the big letter is the style meter. When you land hits, do tricks, parry and dodge, it goes up. It starts at D, then C, B and A, and the best is S. If you get hit once, it drops back to nothing.

The numbers that jump off the enemy show your damage. The words in the middle of the screen, like PARRY, DODGE and PERFECT DODGE, tell you what you just did. Trick names, like ONE-TWO KICK or WHIRLWIND, show up when you mix punches, kicks and dodges quickly. If you dodge at the very last moment, you get a perfect dodge. Time slows down for everyone except Kai, and his hits get stronger.

There is also something you cannot see. I have lost two times, so the Marshal now starts with ten percent less health. The first try again is the same fight, so you can learn it. After the second loss, he gets a little weaker each time, but never below seventy percent. Also, the long talk when his mask comes off only plays once. When you try again, it is only two lines.

This time I play differently. I do not use everything on the Marshal. I keep the shrines for the kudu.

*(pause)*

Baba Zwane falls, the horn drops, and the stag comes down again. This time I am ready.

*(pause)*

I still have the shrines, and I have the horn's power. I press V. While the horn plays, the world moves at about one third of its speed for three seconds, but Kai still moves at full speed. After that, it takes nine seconds to charge again. You can see the ring fill up around the HORN button. The whole screen turns grey, and only the horn's blue light keeps its colour.

*(pause)*

I make the stag charge into a tree. When it hits something, it gets stuck. Its cracks turn blue, and now I can hurt it. When it is stuck and I am close, I press E and jump onto its back. It jumps around to throw me off, and I use A and D to stay on.

*(pause)*

The kudu falls and turns back into stone. The cracks and the eyes stop glowing. The horn is clean again.

*(long pause)*

The storm stops, and the fireflies come out. Kai picks up the horn from where it fell. Baba Zwane is beaten. He says the company will send more people. Kai says they will find the horn back on its stone. Then Kai blows the horn. It makes a long, low sound over the waterfall, and the forest answers.

*(pause)*

VICTORY. The card shows how long my fight took and how much health I had left, next to my best scores.

*(long pause)*

I press Continue, and we go to the epilogue. It is the next morning. Kai walks up the old path to the place where the story started. The forest is very quiet. No birds, no wind. It has been like this since he took the horn. He takes the horn and puts it back on its stone, in the same place it was before. A ring of light goes out across the ground, and the forest wakes up. The wind moves the leaves again, the birds sing, birds fly up from the trees, and the mist goes away. Kai turns and walks back down the path.

The end.

*(long pause)*

That was Level 3, The Falls. Three tries, two losses, a Marshal who was really Baba Zwane, and one very angry kudu. Thank you for watching.
