Courtesy of [DJ Cylob](http://cylob.blogspot.com/)

```
// a = NetAddr("127.0.0.1", 57120);

n = Array.newClear(5);
s = Server.internal;
s.waitForBoot({

	SynthDef("tuiofmtest",
		{
		|freq1 = 400, freq2 = 400, modAmt = 5, amp = 0.4|
		var output;
		
		output = SinOsc.ar(freq1 * SinOsc.ar(freq2, 0, modAmt, 1), 0, amp);
		Out.ar(0, output ! 2);
		
		}
	).send(s);
	
});
// f is the frequency spec
f = [
	[80, 2000, \exponential].asSpec,
	[120, 1400, \exponential].asSpec,
	[200, 5000, \exponential].asSpec,
	[50, 6000, \exponential].asSpec,
	[500, 800, \exponential].asSpec
];
// m is the modAmt spec
m = [0.9, 5, \exponential].asSpec;
// a is the amp spec
a = [0.2, 0.6, \linear].asSpec;

// l is the last x, y, velX, velY values for each finger
l = [
	[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]
];

o = OSCresponderNode(
		nil, 
		'/tuio/2Dcur', 
		{ 
		|t, r, msg|
		//("time:" + t).postln; 
		//msg.postln 
		case
			{msg[1] == 'alive'}
			{
			var alive, dead;
			alive = msg.copyToEnd(2) - 1;
			dead = [0, 1, 2, 3, 4];
			dead.removeAllSuchThat({ |item| alive.includes(item) });
	/*
	["alive ", alive].postln;
	["dead ", dead].postln;
	*/
			// kill any nodes that died
			dead.do { |item|
				if(n[item] != nil)
					{
					s.sendMsg("/n_free", n[item]);
					n[item] = nil;
					};
			};
			// start "alive" nodes if they're not already present
			alive.do { |item|
				if(n[item] == nil)
					{
					n[item] = s.nextNodeID;
					s.sendMsg(
						"/s_new", "tuiofmtest", n[item], 0, 0,
						"freq1", f[item].map(l[item][0]), "freq2", f[item].map(l[item][1]),
						"modAmt", m.map(l[item][2]), "amp", a.map(l[item][3])
					);
					};
			};

			
			}
			{msg[1] == 'set'}
			{
			var setIndex;
	
			// setIndex: which "set" (i.e. finger) is being moved?
			// minus 1 because the fingers are numbered 1 - 5 from the OSC message
			setIndex = (msg[2] - 1).clip(0, 4);
			l[setIndex] = msg.copyRange(3, 6);
			if(n[setIndex] != nil)
				{
				
				s.sendMsg("/n_set", n[setIndex], 
					"freq1", f[setIndex].map(l[setIndex][0]), 
					"freq2", f[setIndex].map(l[setIndex][1]),
					"modAmt", m.map(l[setIndex][2]),
					"amp", a.map(l[setIndex][3])
				);
				
				};
			};
		}
	).add;



// eventually...
/*
o.remove;
*/
```